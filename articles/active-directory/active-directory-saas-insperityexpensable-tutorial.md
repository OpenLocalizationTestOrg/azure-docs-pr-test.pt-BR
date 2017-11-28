---
title: "Tutorial: integração do Azure Active Directory com o Insperity ExpensAble | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Insperity ExpensAble."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c579c453-580e-417d-8a5e-9b6b352795c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 204d5435c6ba1f23bb98701381e165a9a66add62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insperity-expensable"></a><span data-ttu-id="3cc5a-103">Tutorial: integração do Azure Active Directory com o Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="3cc5a-103">Tutorial: Azure Active Directory integration with Insperity ExpensAble</span></span>

<span data-ttu-id="3cc5a-104">Neste tutorial, você aprenderá como toointegrate Insperity ExpensAble com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="3cc5a-104">In this tutorial, you learn how toointegrate Insperity ExpensAble with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3cc5a-105">Integrando Insperity ExpensAble com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cc5a-105">Integrating Insperity ExpensAble with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3cc5a-106">Você pode controlar no AD do Azure que tenha acesso tooInsperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="3cc5a-106">You can control in Azure AD who has access tooInsperity ExpensAble</span></span>
- <span data-ttu-id="3cc5a-107">Você pode habilitar seu usuários tooautomatically get conectado tooInsperity ExpensAble (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3cc5a-107">You can enable your users tooautomatically get signed-on tooInsperity ExpensAble (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3cc5a-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3cc5a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3cc5a-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3cc5a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cc5a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3cc5a-110">Prerequisites</span></span>

<span data-ttu-id="3cc5a-111">integração do AD do Azure com Insperity ExpensAble de tooconfigure, é necessário Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cc5a-111">tooconfigure Azure AD integration with Insperity ExpensAble, you need hello following items:</span></span>

- <span data-ttu-id="3cc5a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3cc5a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3cc5a-113">Uma assinatura do Insperity ExpensAble com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="3cc5a-113">An Insperity ExpensAble single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3cc5a-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3cc5a-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3cc5a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3cc5a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3cc5a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3cc5a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3cc5a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3cc5a-118">Scenario description</span></span>
<span data-ttu-id="3cc5a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3cc5a-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="3cc5a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3cc5a-121">Adicionando Insperity ExpensAble da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3cc5a-121">Adding Insperity ExpensAble from hello gallery</span></span>
2. <span data-ttu-id="3cc5a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3cc5a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insperity-expensable-from-hello-gallery"></a><span data-ttu-id="3cc5a-123">Adicionando Insperity ExpensAble da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3cc5a-123">Adding Insperity ExpensAble from hello gallery</span></span>
<span data-ttu-id="3cc5a-124">integração de Olá tooconfigure de Insperity ExpensAble no AD do Azure, você precisa tooadd Insperity ExpensAble na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-124">tooconfigure hello integration of Insperity ExpensAble into Azure AD, you need tooadd Insperity ExpensAble from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3cc5a-125">**tooadd Insperity ExpensAble da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3cc5a-125">**tooadd Insperity ExpensAble from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3cc5a-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3cc5a-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3cc5a-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3cc5a-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3cc5a-133">Na caixa de pesquisa hello, digite **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-133">In hello search box, type **Insperity ExpensAble**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_search.png)

5. <span data-ttu-id="3cc5a-135">No painel de resultados de saudação, selecione **Insperity ExpensAble**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-135">In hello results panel, select **Insperity ExpensAble**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3cc5a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3cc5a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3cc5a-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Insperity ExpensAble com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-138">In this section, you configure and test Azure AD single sign-on with Insperity ExpensAble based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3cc5a-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Insperity ExpensAble é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Insperity ExpensAble is tooa user in Azure AD.</span></span> <span data-ttu-id="3cc5a-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Insperity ExpensAble precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-140">In other words, a link relationship between an Azure AD user and hello related user in Insperity ExpensAble needs toobe established.</span></span>

<span data-ttu-id="3cc5a-141">Insperity ExpensAble, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-141">In Insperity ExpensAble, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3cc5a-142">tooconfigure e teste de logon único do AD do Azure com Insperity ExpensAble, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cc5a-142">tooconfigure and test Azure AD single sign-on with Insperity ExpensAble, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3cc5a-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3cc5a-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3cc5a-145">**[Criar um usuário de teste Insperity ExpensAble](#creating-an-insperity-expensable-test-user)**  -toohave um equivalente do Britta Simon em Insperity ExpensAble que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-145">**[Creating an Insperity ExpensAble test user](#creating-an-insperity-expensable-test-user)** - toohave a counterpart of Britta Simon in Insperity ExpensAble that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3cc5a-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3cc5a-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3cc5a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cc5a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3cc5a-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Insperity ExpensAble application.</span></span>

<span data-ttu-id="3cc5a-150">**tooconfigure AD do Azure-logon único com Insperity ExpensAble, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3cc5a-150">**tooconfigure Azure AD single sign-on with Insperity ExpensAble, perform hello following steps:**</span></span>

1. <span data-ttu-id="3cc5a-151">Em Olá portal do Azure, Olá **Insperity ExpensAble** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-151">In hello Azure portal, on hello **Insperity ExpensAble** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3cc5a-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_samlbase.png)

3. <span data-ttu-id="3cc5a-155">Em Olá **URLs e domínio ExpensAble Insperity** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cc5a-155">On hello **Insperity ExpensAble Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_url.png)

    <span data-ttu-id="3cc5a-157">a.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-157">a.</span></span> <span data-ttu-id="3cc5a-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span><span class="sxs-lookup"><span data-stu-id="3cc5a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3cc5a-159">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-159">This value is not real.</span></span> <span data-ttu-id="3cc5a-160">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="3cc5a-161">Entre em contato com [equipe de suporte do cliente ExpensAble Insperity](http://expensable.com/support/support-overview) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-161">Contact [Insperity ExpensAble Client support team](http://expensable.com/support/support-overview) tooget this value.</span></span> 
 
4. <span data-ttu-id="3cc5a-162">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_certificate.png) 

5. <span data-ttu-id="3cc5a-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3cc5a-164">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3cc5a-166">Em Olá **configuração ExpensAble Insperity** seção, clique em **configurar Insperity ExpensAble** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-166">On hello **Insperity ExpensAble Configuration** section, click **Configure Insperity ExpensAble** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3cc5a-167">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="3cc5a-167">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_configure.png) 

7. <span data-ttu-id="3cc5a-169">tooconfigure logon único no **Insperity ExpensAble** lado, você precisa toosend Olá baixado **Metadata XML**, **Single Sign-On URL do serviço SAML** e **ID da entidade SAML** muito[a equipe de suporte Insperity ExpensAble](http://expensable.com/support/support-overview).</span><span class="sxs-lookup"><span data-stu-id="3cc5a-169">tooconfigure single sign-on on **Insperity ExpensAble** side, you need toosend hello downloaded **Metadata XML**, **SAML Single Sign-On Service URL** and **SAML Entity ID** too[Insperity ExpensAble support team](http://expensable.com/support/support-overview).</span></span> <span data-ttu-id="3cc5a-170">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3cc5a-171">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="3cc5a-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3cc5a-172">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3cc5a-173">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3cc5a-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3cc5a-174">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3cc5a-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="3cc5a-175">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3cc5a-177">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3cc5a-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3cc5a-178">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3cc5a-180">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3cc5a-182">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3cc5a-184">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cc5a-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3cc5a-186">a.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-186">a.</span></span> <span data-ttu-id="3cc5a-187">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3cc5a-188">b.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-188">b.</span></span> <span data-ttu-id="3cc5a-189">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3cc5a-190">c.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-190">c.</span></span> <span data-ttu-id="3cc5a-191">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3cc5a-192">d.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-192">d.</span></span> <span data-ttu-id="3cc5a-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-193">Click **Create**.</span></span>
 
### <a name="creating-an-insperity-expensable-test-user"></a><span data-ttu-id="3cc5a-194">Como criar um usuário de teste do Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="3cc5a-194">Creating an Insperity ExpensAble test user</span></span>

<span data-ttu-id="3cc5a-195">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-195">hello objective of this section is toocreate a user called Britta Simon in Insperity ExpensAble.</span></span> <span data-ttu-id="3cc5a-196">Trabalhe com [a equipe de suporte Insperity ExpensAble](http://expensable.com/support/support-overview) tooadd usuários Olá Olá Insperity ExpensAble conta.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-196">Please work with [Insperity ExpensAble support team](http://expensable.com/support/support-overview) tooadd hello users in hello Insperity ExpensAble account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3cc5a-197">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3cc5a-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3cc5a-198">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooInsperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInsperity ExpensAble.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3cc5a-200">**tooassign tooInsperity Britta Simon ExpensAble, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3cc5a-200">**tooassign Britta Simon tooInsperity ExpensAble, perform hello following steps:**</span></span>

1. <span data-ttu-id="3cc5a-201">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3cc5a-203">Na lista de aplicativos hello, selecione **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-203">In hello applications list, select **Insperity ExpensAble**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_app.png) 

3. <span data-ttu-id="3cc5a-205">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3cc5a-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-207">Click **Add** button.</span></span> <span data-ttu-id="3cc5a-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3cc5a-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3cc5a-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3cc5a-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3cc5a-213">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3cc5a-213">Testing single sign-on</span></span>

<span data-ttu-id="3cc5a-214">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3cc5a-215">Quando você clica em bloco Insperity ExpensAble Olá Olá painel de acesso, você deve obter um aplicativo Insperity ExpensAble tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="3cc5a-215">When you click hello Insperity ExpensAble tile in hello Access Panel, you should get automatically signed-on tooyour Insperity ExpensAble application.</span></span>
<span data-ttu-id="3cc5a-216">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3cc5a-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3cc5a-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3cc5a-217">Additional resources</span></span>

* [<span data-ttu-id="3cc5a-218">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3cc5a-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3cc5a-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3cc5a-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_203.png

