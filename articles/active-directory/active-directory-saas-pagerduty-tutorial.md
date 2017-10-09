---
title: "Tutorial: integração do Azure Active Directory com o PagerDuty | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e PagerDuty."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="ee3c8-103">Tutorial: integração do Azure Active Directory com o PagerDuty</span><span class="sxs-lookup"><span data-stu-id="ee3c8-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="ee3c8-104">Neste tutorial, você aprenderá como toointegrate PagerDuty com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="ee3c8-104">In this tutorial, you learn how toointegrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ee3c8-105">Integrando PagerDuty com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee3c8-105">Integrating PagerDuty with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ee3c8-106">Você pode controlar no AD do Azure que tenha acesso tooPagerDuty</span><span class="sxs-lookup"><span data-stu-id="ee3c8-106">You can control in Azure AD who has access tooPagerDuty</span></span>
- <span data-ttu-id="ee3c8-107">Você pode habilitar seu usuários tooautomatically get conectado tooPagerDuty (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ee3c8-107">You can enable your users tooautomatically get signed-on tooPagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ee3c8-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ee3c8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ee3c8-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ee3c8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee3c8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ee3c8-110">Prerequisites</span></span>

<span data-ttu-id="ee3c8-111">tooconfigure integração do Azure AD com PagerDuty, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee3c8-111">tooconfigure Azure AD integration with PagerDuty, you need hello following items:</span></span>

- <span data-ttu-id="ee3c8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ee3c8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ee3c8-113">Uma assinatura do PagerDuty habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="ee3c8-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee3c8-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee3c8-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ee3c8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee3c8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee3c8-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee3c8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ee3c8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ee3c8-118">Scenario description</span></span>
<span data-ttu-id="ee3c8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ee3c8-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="ee3c8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ee3c8-121">Adicionando PagerDuty da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ee3c8-121">Adding PagerDuty from hello gallery</span></span>
2. <span data-ttu-id="ee3c8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ee3c8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-hello-gallery"></a><span data-ttu-id="ee3c8-123">Adicionando PagerDuty da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ee3c8-123">Adding PagerDuty from hello gallery</span></span>
<span data-ttu-id="ee3c8-124">integração de saudação tooconfigure do PagerDuty no AD do Azure, você precisa tooadd PagerDuty da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-124">tooconfigure hello integration of PagerDuty into Azure AD, you need tooadd PagerDuty from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ee3c8-125">**tooadd PagerDuty da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ee3c8-125">**tooadd PagerDuty from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee3c8-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="ee3c8-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ee3c8-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="ee3c8-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="ee3c8-133">Na caixa de pesquisa hello, digite **PagerDuty**, selecione **PagerDuty** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-133">In hello search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ee3c8-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee3c8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ee3c8-136">Nesta seção, você configurará e testará o logon único do Azure AD com o PagerDuty, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ee3c8-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no PagerDuty é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PagerDuty is tooa user in Azure AD.</span></span> <span data-ttu-id="ee3c8-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no PagerDuty precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-138">In other words, a link relationship between an Azure AD user and hello related user in PagerDuty needs toobe established.</span></span>

<span data-ttu-id="ee3c8-139">No PagerDuty, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-139">In PagerDuty, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ee3c8-140">tooconfigure e teste de logon único do Azure AD com PagerDuty, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee3c8-140">tooconfigure and test Azure AD single sign-on with PagerDuty, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ee3c8-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ee3c8-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ee3c8-143">**[Criar um usuário de teste do PagerDuty](#create-a-pagerduty-test-user)**  -toohave um equivalente do Britta Simon no PagerDuty é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - toohave a counterpart of Britta Simon in PagerDuty that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ee3c8-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ee3c8-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ee3c8-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee3c8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ee3c8-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="ee3c8-148">**tooconfigure AD do Azure-logon único com o PagerDuty, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ee3c8-148">**tooconfigure Azure AD single sign-on with PagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee3c8-149">Em Olá portal do Azure, Olá **PagerDuty** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-149">In hello Azure portal, on hello **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="ee3c8-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="ee3c8-153">Em Olá **PagerDuty domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee3c8-153">On hello **PagerDuty Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="ee3c8-155">a.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-155">a.</span></span> <span data-ttu-id="ee3c8-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="ee3c8-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="ee3c8-157">b.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-157">b.</span></span> <span data-ttu-id="ee3c8-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="ee3c8-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ee3c8-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-159">These values are not real.</span></span> <span data-ttu-id="ee3c8-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ee3c8-161">Entre em contato com [equipe de suporte do cliente PagerDuty](https://www.pagerduty.com/support/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="ee3c8-162">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="ee3c8-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ee3c8-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ee3c8-166">Em Olá **PagerDuty configuração** seção, clique em **configurar PagerDuty** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-166">On hello **PagerDuty Configuration** section, click **Configure PagerDuty** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ee3c8-167">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="ee3c8-167">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="ee3c8-169">Em outra janela do navegador da Web, faça logon em seu site de empresa do Pagerduty como administrador.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="ee3c8-170">No menu de saudação na parte superior de saudação, clique em **configurações de conta**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-170">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="ee3c8-171">![Configurações de Conta](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Configurações de Conta")</span><span class="sxs-lookup"><span data-stu-id="ee3c8-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="ee3c8-172">Clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="ee3c8-173">![Logon Único](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="ee3c8-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="ee3c8-174">Em Olá **habilitar-logon único (SSO)** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee3c8-174">On hello **Enable Single Sign-on (SSO)** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="ee3c8-175">![Habilitar logon único](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Habilitar logon único")</span><span class="sxs-lookup"><span data-stu-id="ee3c8-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="ee3c8-176">a.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-176">a.</span></span> <span data-ttu-id="ee3c8-177">Abra seu certificado codificado em base 64 baixado do portal do Azure no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509** caixa de texto</span><span class="sxs-lookup"><span data-stu-id="ee3c8-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="ee3c8-178">b.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-178">b.</span></span> <span data-ttu-id="ee3c8-179">Em Olá **URL de logon** caixa de texto, colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-179">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="ee3c8-180">c.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-180">c.</span></span> <span data-ttu-id="ee3c8-181">Em Olá **URL de Logout** caixa de texto, colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-181">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="ee3c8-182">d.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-182">d.</span></span> <span data-ttu-id="ee3c8-183">Selecione **Ativar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="ee3c8-184">e.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-184">e.</span></span> <span data-ttu-id="ee3c8-185">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="ee3c8-186">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="ee3c8-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ee3c8-187">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ee3c8-188">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ee3c8-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ee3c8-189">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee3c8-189">Create an Azure AD test user</span></span>

<span data-ttu-id="ee3c8-190">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="ee3c8-192">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ee3c8-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee3c8-193">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ee3c8-195">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ee3c8-197">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botão Adicionar de saudação](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ee3c8-199">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee3c8-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ee3c8-201">a.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-201">a.</span></span> <span data-ttu-id="ee3c8-202">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ee3c8-203">b.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-203">b.</span></span> <span data-ttu-id="ee3c8-204">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ee3c8-205">c.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-205">c.</span></span> <span data-ttu-id="ee3c8-206">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ee3c8-207">d.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-207">d.</span></span> <span data-ttu-id="ee3c8-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="ee3c8-209">Criar um usuário de teste do PagerDuty</span><span class="sxs-lookup"><span data-stu-id="ee3c8-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="ee3c8-210">tooenable AD do Azure usuários toolog em tooPagerDuty, eles devem ser provisionados no PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-210">tooenable Azure AD users toolog in tooPagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="ee3c8-211">No caso de saudação do PagerDuty, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-211">In hello case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="ee3c8-212">Você pode usar qualquer ferramenta de criação outros Pagerduty usuário conta ou APIs fornecidas pelo Pagerduty tooprovision Azure Active Directory as contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="ee3c8-213">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ee3c8-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee3c8-214">Faça logon no tooyour **Pagerduty** locatário.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-214">Log in tooyour **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="ee3c8-215">No menu de saudação na parte superior de saudação, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-215">In hello menu on hello top, click **Users**.</span></span>

3. <span data-ttu-id="ee3c8-216">Clique em **Adicionar Usuários**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="ee3c8-217">![Adicionar Usuários](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Adicionar Usuários")</span><span class="sxs-lookup"><span data-stu-id="ee3c8-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="ee3c8-218">Em Olá **convidar sua equipe** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee3c8-218">On hello **Invite your team** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="ee3c8-219">![Convidar suas equipe](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Convidar suas equipe")</span><span class="sxs-lookup"><span data-stu-id="ee3c8-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="ee3c8-220">a.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-220">a.</span></span> <span data-ttu-id="ee3c8-221">Saudação de tipo **nome e Sobrenome** do usuário como **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-221">Type hello **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="ee3c8-222">b.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-222">b.</span></span> <span data-ttu-id="ee3c8-223">Digite o endereço de **Email** do usuário, por exemplo, **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="ee3c8-224">c.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-224">c.</span></span> <span data-ttu-id="ee3c8-225">Clique em **Adicionar** e depois em **Enviar Convites**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="ee3c8-226">Todos os usuários adicionados receberão um convite toocreate uma conta no PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-226">All added users will receive an invite toocreate a PagerDuty account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ee3c8-227">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ee3c8-227">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ee3c8-228">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPagerDuty.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPagerDuty.</span></span>

![Atribuir função de usuário Olá][200]

<span data-ttu-id="ee3c8-230">**tooassign Britta Simon tooPagerDuty, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ee3c8-230">**tooassign Britta Simon tooPagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee3c8-231">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ee3c8-233">Na lista de aplicativos hello, selecione **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-233">In hello applications list, select **PagerDuty**.</span></span>

    ![link do PagerDuty Olá na lista de aplicativos Olá](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="ee3c8-235">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="ee3c8-237">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-237">Click **Add** button.</span></span> <span data-ttu-id="ee3c8-238">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="ee3c8-240">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ee3c8-241">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ee3c8-242">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ee3c8-243">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="ee3c8-243">Test single sign-on</span></span>

<span data-ttu-id="ee3c8-244">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ee3c8-245">Quando você clica em bloco PagerDuty Olá Olá acesso Panelyou deve obter automaticamente assinado em tooyour PagerDuty aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee3c8-245">When you click hello PagerDuty tile in hello Access Panelyou should get automatically signed-on tooyour PagerDuty application.</span></span>

<span data-ttu-id="ee3c8-246">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ee3c8-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ee3c8-247">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ee3c8-247">Additional resources</span></span>

* [<span data-ttu-id="ee3c8-248">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ee3c8-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee3c8-249">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ee3c8-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

