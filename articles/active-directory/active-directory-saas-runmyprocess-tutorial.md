---
title: "Tutorial: integração do Azure Active Directory ao RunMyProcess | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e RunMyProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="4acc9-103">Tutorial: Integração do Active Directory do Azure com o RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="4acc9-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="4acc9-104">Neste tutorial, você aprenderá como toointegrate RunMyProcess com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="4acc9-104">In this tutorial, you learn how toointegrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4acc9-105">Integrando o RunMyProcess com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="4acc9-105">Integrating RunMyProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4acc9-106">Você pode controlar no AD do Azure que tenha acesso tooRunMyProcess</span><span class="sxs-lookup"><span data-stu-id="4acc9-106">You can control in Azure AD who has access tooRunMyProcess</span></span>
- <span data-ttu-id="4acc9-107">Você pode habilitar seus usuários tooautomatically get conectado tooRunMyProcess (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4acc9-107">You can enable your users tooautomatically get signed-on tooRunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4acc9-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4acc9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4acc9-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4acc9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4acc9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4acc9-110">Prerequisites</span></span>

<span data-ttu-id="4acc9-111">tooconfigure integração do AD do Azure com o RunMyProcess, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="4acc9-111">tooconfigure Azure AD integration with RunMyProcess, you need hello following items:</span></span>

- <span data-ttu-id="4acc9-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4acc9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4acc9-113">Uma assinatura habilitada para logon único do RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="4acc9-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4acc9-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4acc9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4acc9-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4acc9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4acc9-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4acc9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4acc9-117">Caso não tenha um ambiente de avaliação do Azure AD, obtenha uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4acc9-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4acc9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4acc9-118">Scenario description</span></span>
<span data-ttu-id="4acc9-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4acc9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4acc9-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="4acc9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4acc9-121">Adicionando RunMyProcess da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4acc9-121">Adding RunMyProcess from hello gallery</span></span>
2. <span data-ttu-id="4acc9-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4acc9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-hello-gallery"></a><span data-ttu-id="4acc9-123">Adicionando RunMyProcess da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4acc9-123">Adding RunMyProcess from hello gallery</span></span>
<span data-ttu-id="4acc9-124">integração de saudação tooconfigure do RunMyProcess no AD do Azure, você precisa tooadd RunMyProcess da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4acc9-124">tooconfigure hello integration of RunMyProcess into Azure AD, you need tooadd RunMyProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4acc9-125">**tooadd RunMyProcess da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4acc9-125">**tooadd RunMyProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4acc9-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4acc9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4acc9-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4acc9-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4acc9-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4acc9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4acc9-133">Na caixa de pesquisa hello, digite **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-133">In hello search box, type **RunMyProcess**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="4acc9-135">No painel de resultados de saudação, selecione **RunMyProcess**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4acc9-135">In hello results panel, select **RunMyProcess**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4acc9-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4acc9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4acc9-138">Nesta seção, você configura e testa o logon único do Azure AD com o RunMyProcess, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4acc9-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4acc9-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no RunMyProcess é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4acc9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RunMyProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="4acc9-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no RunMyProcess precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4acc9-140">In other words, a link relationship between an Azure AD user and hello related user in RunMyProcess needs toobe established.</span></span>

<span data-ttu-id="4acc9-141">No RunMyProcess, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="4acc9-141">In RunMyProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4acc9-142">tooconfigure e teste de logon único do AD do Azure com o RunMyProcess, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="4acc9-142">tooconfigure and test Azure AD single sign-on with RunMyProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4acc9-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4acc9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4acc9-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4acc9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4acc9-145">**[Criar um usuário de teste do RunMyProcess](#creating-a-runmyprocess-test-user)**  -toohave um equivalente do Britta Simon no RunMyProcess é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="4acc9-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - toohave a counterpart of Britta Simon in RunMyProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4acc9-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="4acc9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4acc9-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="4acc9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4acc9-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4acc9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4acc9-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="4acc9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="4acc9-150">**tooconfigure AD do Azure-logon único com o RunMyProcess, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4acc9-150">**tooconfigure Azure AD single sign-on with RunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="4acc9-151">Em Olá portal do Azure, Olá **RunMyProcess** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-151">In hello Azure portal, on hello **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4acc9-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="4acc9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="4acc9-155">Em Olá **RunMyProcess domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4acc9-155">On hello **RunMyProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="4acc9-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="4acc9-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4acc9-158">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="4acc9-158">hello value is not real.</span></span> <span data-ttu-id="4acc9-159">Valor de saudação de atualização com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="4acc9-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4acc9-160">Entre em contato com [equipe de suporte do cliente do RunMyProcess](mailto:support@runmyprocess.com) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="4acc9-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) tooget hello value.</span></span> 

4. <span data-ttu-id="4acc9-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4acc9-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="4acc9-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4acc9-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4acc9-165">Em Olá **RunMyProcess configuração** seção, clique em **configurar RunMyProcess** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="4acc9-165">On hello **RunMyProcess Configuration** section, click **Configure RunMyProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4acc9-166">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="4acc9-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="4acc9-168">Em uma janela de navegador web diferente, locatário do RunMyProcess tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="4acc9-168">In a different web browser window, sign-on tooyour RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="4acc9-169">No painel de navegação esquerdo, clique em **Conta** e selecione **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="4acc9-171">Vá muito**método de autenticação** seção e executar etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4acc9-171">Go too**Authentication method** section and perform below steps:</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="4acc9-173">a.</span><span class="sxs-lookup"><span data-stu-id="4acc9-173">a.</span></span> <span data-ttu-id="4acc9-174">Em **Método**, selecione **SSO com Samlv2**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="4acc9-175">b.</span><span class="sxs-lookup"><span data-stu-id="4acc9-175">b.</span></span> <span data-ttu-id="4acc9-176">Em Olá **redirecionamento SSO** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4acc9-176">In hello **SSO redirect** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4acc9-177">c.</span><span class="sxs-lookup"><span data-stu-id="4acc9-177">c.</span></span> <span data-ttu-id="4acc9-178">Em Olá **redirecionamento de Logout** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4acc9-178">In hello **Logout redirect** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4acc9-179">d.</span><span class="sxs-lookup"><span data-stu-id="4acc9-179">d.</span></span> <span data-ttu-id="4acc9-180">Em Olá **formato de Id de nome** texto, o valor de saudação do tipo **formato de nome de identificador** como **urn: oasis: nomes: tc: SAML: 1.1 nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-180">In hello **Name Id Format** textbox, type hello value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="4acc9-181">e.</span><span class="sxs-lookup"><span data-stu-id="4acc9-181">e.</span></span> <span data-ttu-id="4acc9-182">Copiar conteúdo Olá Olá baixado do arquivo de certificado e, em seguida, cole-Olá **certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="4acc9-182">Copy hello content of hello downloaded certificate file and then paste it into hello **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="4acc9-183">f.</span><span class="sxs-lookup"><span data-stu-id="4acc9-183">f.</span></span> <span data-ttu-id="4acc9-184">Clique no ícone **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="4acc9-185">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="4acc9-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4acc9-186">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="4acc9-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4acc9-187">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4acc9-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4acc9-188">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4acc9-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="4acc9-189">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4acc9-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4acc9-191">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4acc9-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4acc9-192">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4acc9-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4acc9-194">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4acc9-196">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4acc9-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4acc9-198">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4acc9-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4acc9-200">a.</span><span class="sxs-lookup"><span data-stu-id="4acc9-200">a.</span></span> <span data-ttu-id="4acc9-201">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4acc9-202">b.</span><span class="sxs-lookup"><span data-stu-id="4acc9-202">b.</span></span> <span data-ttu-id="4acc9-203">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4acc9-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4acc9-204">c.</span><span class="sxs-lookup"><span data-stu-id="4acc9-204">c.</span></span> <span data-ttu-id="4acc9-205">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4acc9-206">d.</span><span class="sxs-lookup"><span data-stu-id="4acc9-206">d.</span></span> <span data-ttu-id="4acc9-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="4acc9-208">Criando um usuário de teste no RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="4acc9-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="4acc9-209">Ordem tooenable AD do Azure usuários toolog em tooRunMyProcess, eles devem ser provisionados no RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="4acc9-209">In order tooenable Azure AD users toolog in tooRunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="4acc9-210">No caso de saudação do RunMyProcess, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="4acc9-210">In hello case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="4acc9-211">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4acc9-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4acc9-212">Faça logon em tooyour site da empresa RunMyProcess como um administrador.</span><span class="sxs-lookup"><span data-stu-id="4acc9-212">Log in tooyour RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="4acc9-213">Clique em **Conta** e selecione **Usuários** no painel de navegação esquerdo, clique em **Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="4acc9-214">![Novo Usuário](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="4acc9-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="4acc9-215">Em Olá **as configurações do usuário** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4acc9-215">In hello **User Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="4acc9-216">![Perfil](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Perfil")</span><span class="sxs-lookup"><span data-stu-id="4acc9-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="4acc9-217">a.</span><span class="sxs-lookup"><span data-stu-id="4acc9-217">a.</span></span> <span data-ttu-id="4acc9-218">Saudação de tipo **nome** e **email** de uma válida do Azure relacionados de conta do AD desejados tooprovision para Olá caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="4acc9-218">Type hello **Name** and **E-mail** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="4acc9-219">b.</span><span class="sxs-lookup"><span data-stu-id="4acc9-219">b.</span></span> <span data-ttu-id="4acc9-220">Selecione uma **Linguagem IDE**, um **Idioma** e um **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="4acc9-221">c.</span><span class="sxs-lookup"><span data-stu-id="4acc9-221">c.</span></span> <span data-ttu-id="4acc9-222">Selecione **enviar toome de email de criação de conta**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-222">Select **Send account creation e-mail toome**.</span></span> 

    <span data-ttu-id="4acc9-223">d.</span><span class="sxs-lookup"><span data-stu-id="4acc9-223">d.</span></span> <span data-ttu-id="4acc9-224">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="4acc9-225">Você pode usar qualquer ferramenta de criação outros RunMyProcess usuário conta ou APIs fornecidas pelo RunMyProcess tooprovision Azure Active Directory as contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="4acc9-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess tooprovision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4acc9-226">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4acc9-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4acc9-227">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooRunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="4acc9-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRunMyProcess.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4acc9-229">**tooassign Britta Simon tooRunMyProcess, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4acc9-229">**tooassign Britta Simon tooRunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="4acc9-230">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4acc9-232">Na lista de aplicativos hello, selecione **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-232">In hello applications list, select **RunMyProcess**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="4acc9-234">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4acc9-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4acc9-236">Click **Add** button.</span></span> <span data-ttu-id="4acc9-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4acc9-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4acc9-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="4acc9-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4acc9-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4acc9-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4acc9-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4acc9-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4acc9-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4acc9-242">Testing single sign-on</span></span>

<span data-ttu-id="4acc9-243">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="4acc9-243">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4acc9-244">Quando você clica em Olá RunMyProcess bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo do RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="4acc9-244">When you click hello RunMyProcess tile in hello Access Panel, you should get automatically signed-on tooyour RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4acc9-245">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4acc9-245">Additional resources</span></span>

* [<span data-ttu-id="4acc9-246">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4acc9-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4acc9-247">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4acc9-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

