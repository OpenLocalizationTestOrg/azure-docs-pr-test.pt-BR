---
title: "Tutorial: integração do Azure Active Directory com o SCC LifeCycle | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SCC LifeCycle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 63623c5bd2d951612040f0121615a406bf83e890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="9f9cf-103">Tutorial: Integração do Active Directory do Azure com o SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="9f9cf-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>

<span data-ttu-id="9f9cf-104">Neste tutorial, você aprenderá como toointegrate SCC LifeCycle com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="9f9cf-104">In this tutorial, you learn how toointegrate SCC LifeCycle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f9cf-105">Integração do SCC LifeCycle com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f9cf-105">Integrating SCC LifeCycle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9f9cf-106">Você pode controlar no AD do Azure que tenha acesso tooSCC ciclo de vida</span><span class="sxs-lookup"><span data-stu-id="9f9cf-106">You can control in Azure AD who has access tooSCC LifeCycle</span></span>
- <span data-ttu-id="9f9cf-107">Você pode habilitar seu usuários tooautomatically get conectado tooSCC ciclo de vida (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f9cf-107">You can enable your users tooautomatically get signed-on tooSCC LifeCycle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f9cf-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9f9cf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9f9cf-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f9cf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f9cf-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9f9cf-110">Prerequisites</span></span>

<span data-ttu-id="9f9cf-111">tooconfigure integração do AD do Azure com o ciclo de vida de SCC, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f9cf-111">tooconfigure Azure AD integration with SCC LifeCycle, you need hello following items:</span></span>

- <span data-ttu-id="9f9cf-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f9cf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f9cf-113">Uma assinatura habilitada para logon único do SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="9f9cf-113">An SCC LifeCycle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9f9cf-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9f9cf-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9f9cf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f9cf-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9f9cf-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f9cf-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f9cf-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9f9cf-118">Scenario description</span></span>
<span data-ttu-id="9f9cf-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f9cf-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="9f9cf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f9cf-121">Adicionando o ciclo de vida de SCC da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9f9cf-121">Adding SCC LifeCycle from hello gallery</span></span>
2. <span data-ttu-id="9f9cf-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f9cf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scc-lifecycle-from-hello-gallery"></a><span data-ttu-id="9f9cf-123">Adicionando o ciclo de vida de SCC da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9f9cf-123">Adding SCC LifeCycle from hello gallery</span></span>
<span data-ttu-id="9f9cf-124">integração de saudação tooconfigure do ciclo de vida de SCC no AD do Azure, você precisa tooadd SCC LifeCycle na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-124">tooconfigure hello integration of SCC LifeCycle into Azure AD, you need tooadd SCC LifeCycle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9f9cf-125">**tooadd SCC LifeCycle da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f9cf-125">**tooadd SCC LifeCycle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f9cf-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9f9cf-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9f9cf-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9f9cf-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9f9cf-133">Na caixa de pesquisa hello, digite **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-133">In hello search box, type **SCC LifeCycle**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_search.png)

5. <span data-ttu-id="9f9cf-135">No painel de resultados de saudação, selecione **SCC LifeCycle**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-135">In hello results panel, select **SCC LifeCycle**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f9cf-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f9cf-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="9f9cf-138">Nesta seção, você configura e testa o logon único do Azure AD com o SCC LifeCycle, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-138">In this section, you configure and test Azure AD single sign-on with SCC LifeCycle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9f9cf-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ciclo de vida de SCC é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SCC LifeCycle is tooa user in Azure AD.</span></span> <span data-ttu-id="9f9cf-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação do ciclo de vida de SCC precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-140">In other words, a link relationship between an Azure AD user and hello related user in SCC LifeCycle needs toobe established.</span></span>

<span data-ttu-id="9f9cf-141">No ciclo de vida de SCC, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-141">In SCC LifeCycle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9f9cf-142">tooconfigure e teste de logon único do AD do Azure com o ciclo de vida de SCC, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f9cf-142">tooconfigure and test Azure AD single sign-on with SCC LifeCycle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9f9cf-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9f9cf-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f9cf-145">**[Criar um usuário de teste do ciclo de vida de SCC](#creating-an-scc-lifecycle-test-user)**  -toohave um equivalente do Britta Simon no ciclo de vida de SCC é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-145">**[Creating an SCC LifeCycle test user](#creating-an-scc-lifecycle-test-user)** - toohave a counterpart of Britta Simon in SCC LifeCycle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9f9cf-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f9cf-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f9cf-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f9cf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9f9cf-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SCC LifeCycle application.</span></span>

<span data-ttu-id="9f9cf-150">**tooconfigure AD do Azure-logon único com SCC LifeCycle, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f9cf-150">**tooconfigure Azure AD single sign-on with SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f9cf-151">Em Olá portal do Azure, Olá **SCC LifeCycle** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-151">In hello Azure portal, on hello **SCC LifeCycle** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9f9cf-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_samlbase.png)

3. <span data-ttu-id="9f9cf-155">Em Olá **domínio de ciclo de vida de SCC e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f9cf-155">On hello **SCC LifeCycle Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_url.png)

    <span data-ttu-id="9f9cf-157">a.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-157">a.</span></span> <span data-ttu-id="9f9cf-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span><span class="sxs-lookup"><span data-stu-id="9f9cf-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span></span>

    <span data-ttu-id="9f9cf-159">b.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-159">b.</span></span> <span data-ttu-id="9f9cf-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f9cf-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|--|
    | `https://bs1.scc.com/<entity>`|
    | `https://lifecycle.scc.com/<entity>`|
    
    > [!NOTE] 
    > <span data-ttu-id="9f9cf-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-161">These values are not real.</span></span> <span data-ttu-id="9f9cf-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9f9cf-163">Entre em contato com [equipe de suporte do cliente do ciclo de vida de SCC](mailto:lifecycle.support@scc.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-163">Contact [SCC LifeCycle Client support team](mailto:lifecycle.support@scc.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="9f9cf-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_certificate.png) 

5. <span data-ttu-id="9f9cf-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9f9cf-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9f9cf-168">tooconfigure logon único no **SCC LifeCycle** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do SCC LifeCycle](mailto:lifecycle.support@scc.com).</span><span class="sxs-lookup"><span data-stu-id="9f9cf-168">tooconfigure single sign-on on **SCC LifeCycle** side, you need toosend hello downloaded **Metadata XML** too[SCC LifeCycle support team](mailto:lifecycle.support@scc.com).</span></span> <span data-ttu-id="9f9cf-169">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

     >[!NOTE]
   ><span data-ttu-id="9f9cf-170">O logon único tem toobe habilitado por Olá, equipe de suporte do SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-170">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

> [!TIP]
> <span data-ttu-id="9f9cf-171">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="9f9cf-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9f9cf-172">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9f9cf-173">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9f9cf-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f9cf-174">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f9cf-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f9cf-175">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9f9cf-177">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f9cf-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f9cf-178">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f9cf-180">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f9cf-182">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f9cf-184">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f9cf-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f9cf-186">a.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-186">a.</span></span> <span data-ttu-id="9f9cf-187">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f9cf-188">b.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-188">b.</span></span> <span data-ttu-id="9f9cf-189">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9f9cf-190">c.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-190">c.</span></span> <span data-ttu-id="9f9cf-191">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9f9cf-192">d.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-192">d.</span></span> <span data-ttu-id="9f9cf-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-193">Click **Create**.</span></span>
 
### <a name="creating-an-scc-lifecycle-test-user"></a><span data-ttu-id="9f9cf-194">Criando um usuário de teste do SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="9f9cf-194">Creating an SCC LifeCycle test user</span></span>

<span data-ttu-id="9f9cf-195">Ordem tooenable AD do Azure usuários toolog no SCC LifeCycle, eles devem ser provisionados no SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-195">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="9f9cf-196">Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooSCC ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-196">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="9f9cf-197">Quando um toolog de tentativas de usuário atribuído no SCC LifeCycle, uma conta do SCC LifeCycle é criada automaticamente, se necessário.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-197">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

> [!NOTE]
    > <span data-ttu-id="9f9cf-198">proprietário de conta do Active Directory do Azure Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-198">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9f9cf-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f9cf-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9f9cf-200">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSCC ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSCC LifeCycle.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9f9cf-202">**tooassign Britta Simon tooSCC ciclo de vida, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f9cf-202">**tooassign Britta Simon tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f9cf-203">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="9f9cf-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications.**</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9f9cf-205">Na lista de aplicativos hello, selecione **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-205">In hello applications list, select **SCC LifeCycle**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_app.png) 

3. <span data-ttu-id="9f9cf-207">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9f9cf-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-209">Click **Add** button.</span></span> <span data-ttu-id="9f9cf-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9f9cf-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9f9cf-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f9cf-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9f9cf-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9f9cf-215">Testing single sign-on</span></span>

<span data-ttu-id="9f9cf-216">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9f9cf-217">Quando você clica em Olá SCC LifeCycle bloco no painel de acesso de saudação, você deve obter tooSCC automaticamente conectado no ciclo de vida de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f9cf-217">When you click hello SCC LifeCycle tile in hello Access Panel, you should get automatically signed-on tooSCC LifeCycle application.</span></span>
<span data-ttu-id="9f9cf-218">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9f9cf-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9f9cf-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9f9cf-219">Additional resources</span></span>

* [<span data-ttu-id="9f9cf-220">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9f9cf-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f9cf-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9f9cf-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_203.png

