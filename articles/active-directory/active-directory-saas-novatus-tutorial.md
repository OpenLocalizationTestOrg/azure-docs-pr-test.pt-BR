---
title: "Tutorial: integração do Azure Active Directory com o Novatus | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Novatus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: 7ff13f56f0f47d0c2667c9ca555801a7a06a2fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="52fa2-103">Tutorial: Integração do Active Directory do Azure com o Novatus</span><span class="sxs-lookup"><span data-stu-id="52fa2-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="52fa2-104">Neste tutorial, você aprenderá como toointegrate Novatus com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="52fa2-104">In this tutorial, you learn how toointegrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52fa2-105">Integrando Novatus com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="52fa2-105">Integrating Novatus with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="52fa2-106">Você pode controlar no AD do Azure que tenha acesso tooNovatus</span><span class="sxs-lookup"><span data-stu-id="52fa2-106">You can control in Azure AD who has access tooNovatus</span></span>
- <span data-ttu-id="52fa2-107">Você pode habilitar seus usuários tooautomatically get conectado tooNovatus (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="52fa2-107">You can enable your users tooautomatically get signed-on tooNovatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52fa2-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="52fa2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="52fa2-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52fa2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52fa2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="52fa2-110">Prerequisites</span></span>

<span data-ttu-id="52fa2-111">tooconfigure integração do AD do Azure com Novatus, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="52fa2-111">tooconfigure Azure AD integration with Novatus, you need hello following items:</span></span>

- <span data-ttu-id="52fa2-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="52fa2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52fa2-113">Uma assinatura habilitada para logon único do Novatus</span><span class="sxs-lookup"><span data-stu-id="52fa2-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52fa2-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="52fa2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52fa2-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="52fa2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52fa2-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="52fa2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52fa2-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52fa2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52fa2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="52fa2-118">Scenario description</span></span>
<span data-ttu-id="52fa2-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="52fa2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52fa2-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="52fa2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52fa2-121">Adicionando Novatus da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="52fa2-121">Adding Novatus from hello gallery</span></span>
2. <span data-ttu-id="52fa2-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="52fa2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-hello-gallery"></a><span data-ttu-id="52fa2-123">Adicionando Novatus da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="52fa2-123">Adding Novatus from hello gallery</span></span>
<span data-ttu-id="52fa2-124">integração de saudação tooconfigure de Novatus no AD do Azure, você precisa tooadd Novatus da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="52fa2-124">tooconfigure hello integration of Novatus into Azure AD, you need tooadd Novatus from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="52fa2-125">**tooadd Novatus da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="52fa2-125">**tooadd Novatus from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="52fa2-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="52fa2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="52fa2-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="52fa2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="52fa2-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="52fa2-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="52fa2-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52fa2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="52fa2-133">Na caixa de pesquisa hello, digite **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="52fa2-133">In hello search box, type **Novatus**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_search.png)

5. <span data-ttu-id="52fa2-135">No painel de resultados de saudação, selecione **Novatus**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="52fa2-135">In hello results panel, select **Novatus**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52fa2-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="52fa2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52fa2-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Novatus, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="52fa2-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="52fa2-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Novatus é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="52fa2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Novatus is tooa user in Azure AD.</span></span> <span data-ttu-id="52fa2-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Novatus precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="52fa2-140">In other words, a link relationship between an Azure AD user and hello related user in Novatus needs toobe established.</span></span>

<span data-ttu-id="52fa2-141">Novatus, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="52fa2-141">In Novatus, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="52fa2-142">tooconfigure e teste de logon único do AD do Azure com Novatus, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="52fa2-142">tooconfigure and test Azure AD single sign-on with Novatus, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="52fa2-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="52fa2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="52fa2-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52fa2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52fa2-145">**[Criar um usuário de teste Novatus](#creating-a-novatus-test-user)**  -toohave um equivalente do Britta Simon em Novatus é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="52fa2-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - toohave a counterpart of Britta Simon in Novatus that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="52fa2-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="52fa2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52fa2-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="52fa2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52fa2-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="52fa2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52fa2-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Novatus.</span><span class="sxs-lookup"><span data-stu-id="52fa2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="52fa2-150">**tooconfigure AD do Azure-logon único com Novatus, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="52fa2-150">**tooconfigure Azure AD single sign-on with Novatus, perform hello following steps:**</span></span>

1. <span data-ttu-id="52fa2-151">Em Olá portal do Azure, Olá **Novatus** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="52fa2-151">In hello Azure portal, on hello **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="52fa2-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="52fa2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_samlbase.png)

3. <span data-ttu-id="52fa2-155">Em Olá **Novatus domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="52fa2-155">On hello **Novatus Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="52fa2-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://sso.novatuscontracts.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="52fa2-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="52fa2-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="52fa2-158">This value is not real.</span></span> <span data-ttu-id="52fa2-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="52fa2-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="52fa2-160">Entre em contato com [equipe de suporte do cliente Novatus](mailto:jvinci@novatusinc.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="52fa2-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="52fa2-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="52fa2-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_certificate.png) 

5. <span data-ttu-id="52fa2-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="52fa2-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-novatus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="52fa2-165">Em Olá **Novatus configuração** seção, clique em **configurar Novatus** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="52fa2-165">On hello **Novatus Configuration** section, click **Configure Novatus** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="52fa2-166">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="52fa2-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_configure.png) 

7. <span data-ttu-id="52fa2-168">tooget SSO configurado para o seu aplicativo, entre em contato com seu [equipe de suporte do Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="52fa2-168">tooget SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="52fa2-169">Anexar Olá **baixado certificado** Olá de email e compartilhamento de arquivo tooyour **urls de metadados** (**URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML**) com Novatus tooset o logon único no seu lado da equipe.</span><span class="sxs-lookup"><span data-stu-id="52fa2-169">Attach hello **downloaded certificate** file tooyour mail and share hello **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team tooset up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="52fa2-170">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="52fa2-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="52fa2-171">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="52fa2-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="52fa2-172">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="52fa2-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52fa2-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="52fa2-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="52fa2-174">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="52fa2-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="52fa2-176">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="52fa2-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="52fa2-177">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="52fa2-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-novatus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="52fa2-179">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="52fa2-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-novatus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="52fa2-181">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="52fa2-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52fa2-183">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="52fa2-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52fa2-185">a.</span><span class="sxs-lookup"><span data-stu-id="52fa2-185">a.</span></span> <span data-ttu-id="52fa2-186">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52fa2-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52fa2-187">b.</span><span class="sxs-lookup"><span data-stu-id="52fa2-187">b.</span></span> <span data-ttu-id="52fa2-188">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="52fa2-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52fa2-189">c.</span><span class="sxs-lookup"><span data-stu-id="52fa2-189">c.</span></span> <span data-ttu-id="52fa2-190">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="52fa2-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="52fa2-191">d.</span><span class="sxs-lookup"><span data-stu-id="52fa2-191">d.</span></span> <span data-ttu-id="52fa2-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="52fa2-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="52fa2-193">Criar um usuário de teste do Novatus</span><span class="sxs-lookup"><span data-stu-id="52fa2-193">Creating a Novatus test user</span></span>

<span data-ttu-id="52fa2-194">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Novatus.</span><span class="sxs-lookup"><span data-stu-id="52fa2-194">hello objective of this section is toocreate a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="52fa2-195">O Novatus dá suporte ao provisionamento just-in-time, que é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="52fa2-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="52fa2-196">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="52fa2-196">There is no action item for you in this section.</span></span> <span data-ttu-id="52fa2-197">Será criado um novo usuário durante uma tentativa tooaccess Novatus se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="52fa2-197">A new user will be created during an attempt tooaccess Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="52fa2-198">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [equipe de suporte do Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="52fa2-198">If you need toocreate an user manually, you need toocontact hello [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="52fa2-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="52fa2-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="52fa2-200">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooNovatus.</span><span class="sxs-lookup"><span data-stu-id="52fa2-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNovatus.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="52fa2-202">**tooassign Britta Simon tooNovatus, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="52fa2-202">**tooassign Britta Simon tooNovatus, perform hello following steps:**</span></span>

1. <span data-ttu-id="52fa2-203">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="52fa2-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="52fa2-205">Na lista de aplicativos hello, selecione **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="52fa2-205">In hello applications list, select **Novatus**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_app.png) 

3. <span data-ttu-id="52fa2-207">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="52fa2-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="52fa2-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="52fa2-209">Click **Add** button.</span></span> <span data-ttu-id="52fa2-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52fa2-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="52fa2-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="52fa2-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="52fa2-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52fa2-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52fa2-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52fa2-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="52fa2-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="52fa2-215">Testing single sign-on</span></span>

<span data-ttu-id="52fa2-216">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="52fa2-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="52fa2-217">Quando você clica em Olá Novatus bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Novatus aplicativo.</span><span class="sxs-lookup"><span data-stu-id="52fa2-217">When you click hello Novatus tile in hello Access Panel, you should get automatically signed-on tooyour Novatus application.</span></span> <span data-ttu-id="52fa2-218">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="52fa2-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="52fa2-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="52fa2-219">Additional resources</span></span>

* [<span data-ttu-id="52fa2-220">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="52fa2-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52fa2-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52fa2-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png

