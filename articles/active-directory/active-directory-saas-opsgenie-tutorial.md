---
title: "Tutorial: Integração do Azure Active Directory com o OpsGenie | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e OpsGenie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 50d31c234fb9716d05d681b9bc4164740a3a662b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="27f8e-103">Tutorial: Integração do Active Directory do Azure com o OpsGenie</span><span class="sxs-lookup"><span data-stu-id="27f8e-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="27f8e-104">Neste tutorial, você aprenderá como toointegrate OpsGenie com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="27f8e-104">In this tutorial, you learn how toointegrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27f8e-105">Integrando OpsGenie com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="27f8e-105">Integrating OpsGenie with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="27f8e-106">Você pode controlar no AD do Azure que tenha acesso tooOpsGenie</span><span class="sxs-lookup"><span data-stu-id="27f8e-106">You can control in Azure AD who has access tooOpsGenie</span></span>
- <span data-ttu-id="27f8e-107">Você pode habilitar seu usuários tooautomatically get conectado tooOpsGenie (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="27f8e-107">You can enable your users tooautomatically get signed-on tooOpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="27f8e-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="27f8e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="27f8e-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="27f8e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27f8e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="27f8e-110">Prerequisites</span></span>

<span data-ttu-id="27f8e-111">tooconfigure integração do AD do Azure com OpsGenie, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="27f8e-111">tooconfigure Azure AD integration with OpsGenie, you need hello following items:</span></span>

- <span data-ttu-id="27f8e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="27f8e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27f8e-113">Uma assinatura habilitada para logon único do OpsGenie</span><span class="sxs-lookup"><span data-stu-id="27f8e-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27f8e-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="27f8e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27f8e-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="27f8e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27f8e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="27f8e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="27f8e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27f8e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27f8e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="27f8e-118">Scenario description</span></span>
<span data-ttu-id="27f8e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="27f8e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27f8e-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="27f8e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27f8e-121">Adicionando OpsGenie da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="27f8e-121">Adding OpsGenie from hello gallery</span></span>
2. <span data-ttu-id="27f8e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="27f8e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-hello-gallery"></a><span data-ttu-id="27f8e-123">Adicionando OpsGenie da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="27f8e-123">Adding OpsGenie from hello gallery</span></span>
<span data-ttu-id="27f8e-124">integração de saudação tooconfigure de OpsGenie no AD do Azure, você precisa tooadd OpsGenie da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="27f8e-124">tooconfigure hello integration of OpsGenie into Azure AD, you need tooadd OpsGenie from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="27f8e-125">**tooadd OpsGenie da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="27f8e-125">**tooadd OpsGenie from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="27f8e-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="27f8e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="27f8e-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="27f8e-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="27f8e-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27f8e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="27f8e-133">Na caixa de pesquisa hello, digite **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-133">In hello search box, type **OpsGenie**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="27f8e-135">No painel de resultados de saudação, selecione **OpsGenie**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="27f8e-135">In hello results panel, select **OpsGenie**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="27f8e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="27f8e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="27f8e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o OpsGenie, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="27f8e-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27f8e-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em OpsGenie é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="27f8e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OpsGenie is tooa user in Azure AD.</span></span> <span data-ttu-id="27f8e-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em OpsGenie precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="27f8e-140">In other words, a link relationship between an Azure AD user and hello related user in OpsGenie needs toobe established.</span></span>

<span data-ttu-id="27f8e-141">OpsGenie, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f8e-141">In OpsGenie, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="27f8e-142">tooconfigure e teste de logon único do AD do Azure com OpsGenie, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="27f8e-142">tooconfigure and test Azure AD single sign-on with OpsGenie, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="27f8e-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="27f8e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="27f8e-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27f8e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27f8e-145">**[Criar um usuário de teste OpsGenie](#creating-a-opsgenie-test-user)**  -toohave um equivalente do Britta Simon em OpsGenie é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="27f8e-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - toohave a counterpart of Britta Simon in OpsGenie that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="27f8e-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="27f8e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27f8e-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="27f8e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="27f8e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="27f8e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="27f8e-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="27f8e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="27f8e-150">**tooconfigure AD do Azure-logon único com OpsGenie, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="27f8e-150">**tooconfigure Azure AD single sign-on with OpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="27f8e-151">Em Olá portal do Azure, Olá **OpsGenie** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-151">In hello Azure portal, on hello **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="27f8e-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="27f8e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="27f8e-155">Em Olá **OpsGenie domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27f8e-155">On hello **OpsGenie Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="27f8e-157">Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="27f8e-157">In hello **Sign-on URL** textbox, type hello URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="27f8e-158">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="27f8e-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="27f8e-160">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="27f8e-160">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="27f8e-162">Em Olá **OpsGenie configuração** seção, clique em **configurar OpsGenie** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="27f8e-162">On hello **OpsGenie Configuration** section, click **Configure OpsGenie** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="27f8e-163">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="27f8e-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="27f8e-165">Abrir outra instância do navegador e, em seguida, efetue login tooOpsGenie como um administrador.</span><span class="sxs-lookup"><span data-stu-id="27f8e-165">Open another browser instance, and then log-in tooOpsGenie as an administrator.</span></span>

8. <span data-ttu-id="27f8e-166">Clique em **configurações**e, em seguida, clique em Olá **Single Sign On** guia.</span><span class="sxs-lookup"><span data-stu-id="27f8e-166">Click **Settings**, and then click hello **Single Sign On** tab.</span></span>
   
    ![Logon único do OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="27f8e-168">Selecione tooenable SSO, **habilitado**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-168">tooenable SSO, select **Enabled**.</span></span>
   
    ![Configurações do OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="27f8e-170">Em Olá **provedor** seção, clique em Olá **Active Directory do Azure** guia.</span><span class="sxs-lookup"><span data-stu-id="27f8e-170">In hello **Provider** section, click hello **Azure Active Directory** tab.</span></span>
   
    ![Configurações do OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="27f8e-172">Na página de diálogo do Active Directory do Azure hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27f8e-172">On hello Azure Active Directory dialog page, perform hello following steps:</span></span>
   
    ![Configurações do OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="27f8e-174">a.</span><span class="sxs-lookup"><span data-stu-id="27f8e-174">a.</span></span> <span data-ttu-id="27f8e-175">Colar **Service URL de logon único**, que você copiou de saudação portal do Azure em hello **o ponto de extremidade do SAML 2.0** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="27f8e-175">Paste **Single Sign On Service URL**, which you have copied from hello Azure portal into hello **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="27f8e-176">b.</span><span class="sxs-lookup"><span data-stu-id="27f8e-176">b.</span></span> <span data-ttu-id="27f8e-177">Abra seu certificado baixado de codificada de base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-Olá **certificado x. 500** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="27f8e-177">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="27f8e-178">c.</span><span class="sxs-lookup"><span data-stu-id="27f8e-178">c.</span></span> <span data-ttu-id="27f8e-179">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="27f8e-180">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="27f8e-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="27f8e-181">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="27f8e-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="27f8e-182">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="27f8e-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="27f8e-183">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="27f8e-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="27f8e-184">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="27f8e-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="27f8e-186">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="27f8e-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="27f8e-187">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="27f8e-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="27f8e-189">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="27f8e-191">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f8e-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="27f8e-193">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27f8e-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="27f8e-195">a.</span><span class="sxs-lookup"><span data-stu-id="27f8e-195">a.</span></span> <span data-ttu-id="27f8e-196">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27f8e-197">b.</span><span class="sxs-lookup"><span data-stu-id="27f8e-197">b.</span></span> <span data-ttu-id="27f8e-198">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="27f8e-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="27f8e-199">c.</span><span class="sxs-lookup"><span data-stu-id="27f8e-199">c.</span></span> <span data-ttu-id="27f8e-200">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="27f8e-201">d.</span><span class="sxs-lookup"><span data-stu-id="27f8e-201">d.</span></span> <span data-ttu-id="27f8e-202">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="27f8e-203">Criação de um usuário de teste para OpsGenie</span><span class="sxs-lookup"><span data-stu-id="27f8e-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="27f8e-204">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="27f8e-204">hello objective of this section is toocreate a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="27f8e-205">Em uma janela de navegador da Web, faça logon em seu locatário do OpsGenie como administrador.</span><span class="sxs-lookup"><span data-stu-id="27f8e-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="27f8e-206">Navegue tooUsers lista clicando **usuário** no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="27f8e-206">Navigate tooUsers list by clicking **User** in left panel.</span></span>
   
   ![Configurações do OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="27f8e-208">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-208">Click **Add User**.</span></span>

4. <span data-ttu-id="27f8e-209">Em Olá **adicionar usuário** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27f8e-209">On hello **Add User** dialog, perform hello following steps:</span></span>
   
   ![Configurações do OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="27f8e-211">a.</span><span class="sxs-lookup"><span data-stu-id="27f8e-211">a.</span></span> <span data-ttu-id="27f8e-212">Em Olá **Email** caixa de texto, endereço de email de saudação do tipo do BrittaSimon abordada no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="27f8e-212">In hello **Email** textbox, type hello email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="27f8e-213">b.</span><span class="sxs-lookup"><span data-stu-id="27f8e-213">b.</span></span> <span data-ttu-id="27f8e-214">Em Olá **nome completo** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-214">In hello **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="27f8e-215">c.</span><span class="sxs-lookup"><span data-stu-id="27f8e-215">c.</span></span> <span data-ttu-id="27f8e-216">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="27f8e-217">Brenda receberá um email com instruções para configurar o perfil dela.</span><span class="sxs-lookup"><span data-stu-id="27f8e-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="27f8e-218">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="27f8e-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="27f8e-219">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooOpsGenie.</span><span class="sxs-lookup"><span data-stu-id="27f8e-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOpsGenie.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="27f8e-221">**tooassign Britta Simon tooOpsGenie, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="27f8e-221">**tooassign Britta Simon tooOpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="27f8e-222">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="27f8e-224">Na lista de aplicativos hello, selecione **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-224">In hello applications list, select **OpsGenie**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="27f8e-226">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="27f8e-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="27f8e-228">Click **Add** button.</span></span> <span data-ttu-id="27f8e-229">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27f8e-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="27f8e-231">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f8e-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="27f8e-232">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27f8e-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27f8e-233">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27f8e-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="27f8e-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="27f8e-234">Testing single sign-on</span></span>

<span data-ttu-id="27f8e-235">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="27f8e-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="27f8e-236">Quando você clica em bloco OpsGenie Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour OpsGenie aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27f8e-236">When you click hello OpsGenie tile in hello Access Panel, you should get automatically signed-on tooyour OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="27f8e-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="27f8e-237">Additional resources</span></span>

* [<span data-ttu-id="27f8e-238">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="27f8e-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27f8e-239">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="27f8e-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

