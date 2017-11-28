---
title: "Tutorial: integração do Azure Active Directory ao TargetProcess | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e TargetProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 05c574e2c18d7f73edc6c094093a6e59d46b8e6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="aa0be-103">Tutorial: integração do Active Directory do Azure com o TargetProcess</span><span class="sxs-lookup"><span data-stu-id="aa0be-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="aa0be-104">Neste tutorial, você aprenderá como toointegrate TargetProcess com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="aa0be-104">In this tutorial, you learn how toointegrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aa0be-105">Integrando TargetProcess com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa0be-105">Integrating TargetProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aa0be-106">Você pode controlar no AD do Azure que tenha acesso tooTargetProcess</span><span class="sxs-lookup"><span data-stu-id="aa0be-106">You can control in Azure AD who has access tooTargetProcess</span></span>
- <span data-ttu-id="aa0be-107">Você pode habilitar seus usuários tooautomatically get conectado tooTargetProcess (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa0be-107">You can enable your users tooautomatically get signed-on tooTargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa0be-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="aa0be-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="aa0be-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa0be-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa0be-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aa0be-110">Prerequisites</span></span>

<span data-ttu-id="aa0be-111">tooconfigure integração do AD do Azure com TargetProcess, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa0be-111">tooconfigure Azure AD integration with TargetProcess, you need hello following items:</span></span>

- <span data-ttu-id="aa0be-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa0be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aa0be-113">Uma assinatura do TargetProcess habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="aa0be-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa0be-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="aa0be-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aa0be-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="aa0be-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa0be-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="aa0be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aa0be-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa0be-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa0be-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="aa0be-118">Scenario description</span></span>
<span data-ttu-id="aa0be-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="aa0be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aa0be-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="aa0be-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa0be-121">Adicionar TargetProcess da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="aa0be-121">Add TargetProcess from hello gallery</span></span>
2. <span data-ttu-id="aa0be-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa0be-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-hello-gallery"></a><span data-ttu-id="aa0be-123">Adicionar TargetProcess da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="aa0be-123">Add TargetProcess from hello gallery</span></span>
<span data-ttu-id="aa0be-124">integração de saudação tooconfigure de TargetProcess no AD do Azure, você precisa tooadd TargetProcess da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="aa0be-124">tooconfigure hello integration of TargetProcess into Azure AD, you need tooadd TargetProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aa0be-125">**tooadd TargetProcess da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="aa0be-125">**tooadd TargetProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa0be-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="aa0be-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aa0be-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aa0be-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="aa0be-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa0be-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="aa0be-133">Na caixa de pesquisa hello, digite **TargetProcess**, selecione **TargetProcess** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="aa0be-133">In hello search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![ADICIONAR o TargetProcess da galeria](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="aa0be-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa0be-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="aa0be-136">Nesta seção, você configurará e testará o logon único do Azure AD com o TargetProcess com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="aa0be-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aa0be-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em TargetProcess é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa0be-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TargetProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="aa0be-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em TargetProcess precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="aa0be-138">In other words, a link relationship between an Azure AD user and hello related user in TargetProcess needs toobe established.</span></span>

<span data-ttu-id="aa0be-139">TargetProcess, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa0be-139">In TargetProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="aa0be-140">tooconfigure e teste de logon único do AD do Azure com TargetProcess, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa0be-140">tooconfigure and test Azure AD single sign-on with TargetProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aa0be-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="aa0be-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aa0be-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa0be-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa0be-143">**[Criar um usuário de teste TargetProcess](#create-a-targetprocess-test-user)**  -toohave um equivalente do Britta Simon em TargetProcess é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="aa0be-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - toohave a counterpart of Britta Simon in TargetProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="aa0be-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="aa0be-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa0be-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="aa0be-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="aa0be-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa0be-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="aa0be-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="aa0be-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="aa0be-148">**tooconfigure AD do Azure-logon único com TargetProcess, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="aa0be-148">**tooconfigure Azure AD single sign-on with TargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa0be-149">Em Olá portal do Azure, Olá **TargetProcess** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-149">In hello Azure portal, on hello **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="aa0be-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="aa0be-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Logon único baseado em SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="aa0be-153">Em Olá **TargetProcess domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa0be-153">On hello **TargetProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Seção URLs e Domínio do TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="aa0be-155">a.</span><span class="sxs-lookup"><span data-stu-id="aa0be-155">a.</span></span> <span data-ttu-id="aa0be-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="aa0be-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="aa0be-157">b.</span><span class="sxs-lookup"><span data-stu-id="aa0be-157">b.</span></span> <span data-ttu-id="aa0be-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="aa0be-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="aa0be-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="aa0be-159">These values are not real.</span></span> <span data-ttu-id="aa0be-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="aa0be-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="aa0be-161">Entre em contato com [equipe de suporte do cliente TargetProcess](mailto:support@targetprocess.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="aa0be-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="aa0be-162">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="aa0be-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="aa0be-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="aa0be-164">Click **Save** button.</span></span>

    ![Botão Salvar](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aa0be-166">Em Olá **TargetProcess configuração** seção, clique em **configurar TargetProcess** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="aa0be-166">On hello **TargetProcess Configuration** section, click **Configure TargetProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="aa0be-167">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="aa0be-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Seção de configuração do TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="aa0be-169">Logon tooyour TargetProcess aplicativo como um administrador.</span><span class="sxs-lookup"><span data-stu-id="aa0be-169">Sign-on tooyour TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="aa0be-170">No menu de saudação na parte superior de saudação, clique em **instalação**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-170">In hello menu on hello top, click **Setup**.</span></span>
   
    ![Configuração](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="aa0be-172">Clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-172">Click **Settings**.</span></span>
   
    ![Configurações](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="aa0be-174">Clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-174">Click **Single Sign-on**.</span></span>
   
    ![clique em Logon Único](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="aa0be-176">Em Olá logon único na caixa de diálogo Configurações, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa0be-176">On hello Single Sign-on settings dialog, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="aa0be-178">a.</span><span class="sxs-lookup"><span data-stu-id="aa0be-178">a.</span></span> <span data-ttu-id="aa0be-179">Clique em **Habilitar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="aa0be-180">b.</span><span class="sxs-lookup"><span data-stu-id="aa0be-180">b.</span></span> <span data-ttu-id="aa0be-181">Em **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa0be-181">In **Sign-on URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="aa0be-182">c.</span><span class="sxs-lookup"><span data-stu-id="aa0be-182">c.</span></span> <span data-ttu-id="aa0be-183">Abra seu certificado baixado no bloco de notas, Olá de cópia de conteúdo e, em seguida, cole-o em Olá **certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="aa0be-183">Open your downloaded certificate in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="aa0be-184">d.</span><span class="sxs-lookup"><span data-stu-id="aa0be-184">d.</span></span> <span data-ttu-id="aa0be-185">Clique em **Habilitar Provisionamento de JIT**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="aa0be-186">e.</span><span class="sxs-lookup"><span data-stu-id="aa0be-186">e.</span></span> <span data-ttu-id="aa0be-187">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="aa0be-188">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="aa0be-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="aa0be-189">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="aa0be-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="aa0be-190">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aa0be-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="aa0be-191">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa0be-191">Create an Azure AD test user</span></span>
<span data-ttu-id="aa0be-192">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa0be-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="aa0be-194">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="aa0be-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa0be-195">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="aa0be-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa0be-197">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![lista de saudação toodisplay de usuários](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa0be-199">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa0be-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Botão Adicionar](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa0be-201">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa0be-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Seção de usuário](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aa0be-203">a.</span><span class="sxs-lookup"><span data-stu-id="aa0be-203">a.</span></span> <span data-ttu-id="aa0be-204">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aa0be-205">b.</span><span class="sxs-lookup"><span data-stu-id="aa0be-205">b.</span></span> <span data-ttu-id="aa0be-206">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aa0be-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aa0be-207">c.</span><span class="sxs-lookup"><span data-stu-id="aa0be-207">c.</span></span> <span data-ttu-id="aa0be-208">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="aa0be-209">d.</span><span class="sxs-lookup"><span data-stu-id="aa0be-209">d.</span></span> <span data-ttu-id="aa0be-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="aa0be-211">Criar um usuário de teste do TargetProcess</span><span class="sxs-lookup"><span data-stu-id="aa0be-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="aa0be-212">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="aa0be-212">hello objective of this section is toocreate a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="aa0be-213">O TargetProcess dá suporte ao provisionamento de usuário just-in-time.</span><span class="sxs-lookup"><span data-stu-id="aa0be-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="aa0be-214">Você já habilitou isso em [Configurar o logon único do AD do Azure](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="aa0be-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="aa0be-215">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="aa0be-215">There is no action item for you in this section.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="aa0be-216">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa0be-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="aa0be-217">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTargetProcess.</span><span class="sxs-lookup"><span data-stu-id="aa0be-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTargetProcess.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="aa0be-219">**tooassign Britta Simon tooTargetProcess, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="aa0be-219">**tooassign Britta Simon tooTargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa0be-220">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="aa0be-222">Na lista de aplicativos hello, selecione **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-222">In hello applications list, select **TargetProcess**.</span></span>

    ![TargetProcess na lista de aplicativos](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="aa0be-224">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="aa0be-226">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="aa0be-226">Click **Add** button.</span></span> <span data-ttu-id="aa0be-227">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa0be-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="aa0be-229">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa0be-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aa0be-230">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa0be-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa0be-231">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa0be-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="aa0be-232">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="aa0be-232">Test single sign-on</span></span>

<span data-ttu-id="aa0be-233">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="aa0be-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="aa0be-234">Quando você clica em Olá TargetProcess bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour TargetProcess aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aa0be-234">When you click hello TargetProcess tile in hello Access Panel, you should get automatically signed-on tooyour TargetProcess application.</span></span> <span data-ttu-id="aa0be-235">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="aa0be-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aa0be-236">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="aa0be-236">Additional resources</span></span>

* [<span data-ttu-id="aa0be-237">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="aa0be-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa0be-238">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aa0be-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

