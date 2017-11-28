---
title: "Tutorial: integração do Azure Active Directory ao &frankly | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e & francamente."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 92677b6fcd8609ca31f82a30e85c7010b7bb3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="0d23e-103">Tutorial: integração do Azure Active Directory ao &frankly</span><span class="sxs-lookup"><span data-stu-id="0d23e-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="0d23e-104">Neste tutorial, você aprenderá como toointegrate & francamente com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="0d23e-104">In this tutorial, you learn how toointegrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0d23e-105">Integrando & francamente com o Azure AD fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d23e-105">Integrating &frankly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0d23e-106">Você pode controlar no AD do Azure que tenha acesso muito & francamente</span><span class="sxs-lookup"><span data-stu-id="0d23e-106">You can control in Azure AD who has access too&frankly</span></span>
- <span data-ttu-id="0d23e-107">Você pode permitir que os usuários tooautomatically obter conectado muito & francamente (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0d23e-107">You can enable your users tooautomatically get signed-on too&frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0d23e-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0d23e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0d23e-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0d23e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d23e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0d23e-110">Prerequisites</span></span>

<span data-ttu-id="0d23e-111">integração do AD do Azure tooconfigure com & Francamente, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d23e-111">tooconfigure Azure AD integration with &frankly, you need hello following items:</span></span>

- <span data-ttu-id="0d23e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0d23e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0d23e-113">Uma assinatura do &frankly habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="0d23e-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0d23e-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0d23e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0d23e-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0d23e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0d23e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0d23e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0d23e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d23e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0d23e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0d23e-118">Scenario description</span></span>
<span data-ttu-id="0d23e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0d23e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0d23e-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="0d23e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0d23e-121">Adicionar & francamente da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0d23e-121">Adding &frankly from hello gallery</span></span>
2. <span data-ttu-id="0d23e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0d23e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-hello-gallery"></a><span data-ttu-id="0d23e-123">Adicionar & francamente da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0d23e-123">Adding &frankly from hello gallery</span></span>
<span data-ttu-id="0d23e-124">integração de saudação tooconfigure de & francamente no AD do Azure, você precisa tooadd & francamente da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0d23e-124">tooconfigure hello integration of &frankly into Azure AD, you need tooadd &frankly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0d23e-125">**tooadd & francamente da Galeria de hello, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0d23e-125">**tooadd &frankly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d23e-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0d23e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0d23e-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0d23e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0d23e-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0d23e-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="0d23e-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0d23e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="0d23e-133">Na caixa de pesquisa hello, digite **& francamente**.</span><span class="sxs-lookup"><span data-stu-id="0d23e-133">In hello search box, type **&frankly**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="0d23e-135">No painel de resultados de saudação, selecione **& francamente**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0d23e-135">In hello results panel, select **&frankly**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0d23e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0d23e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0d23e-138">Nesta seção, você configura e testa o logon único do Azure AD com o &frankly, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="0d23e-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0d23e-139">Para toowork de logon único, o AD do Azure precisa tooknow qual Olá usuário correspondente no & francamente é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d23e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in &frankly is tooa user in Azure AD.</span></span> <span data-ttu-id="0d23e-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e Olá relacionados no & usuário francamente necessidades toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="0d23e-140">In other words, a link relationship between an Azure AD user and hello related user in &frankly needs toobe established.</span></span>

<span data-ttu-id="0d23e-141">No & Francamente, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d23e-141">In &frankly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0d23e-142">tooconfigure e teste de logon único do AD do Azure com & Francamente, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d23e-142">tooconfigure and test Azure AD single sign-on with &frankly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0d23e-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0d23e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0d23e-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d23e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0d23e-145">**[Criar um & francamente usuário de teste](#creating-a-frankly-test-user)**  -toohave um equivalente de Britta Simon no & francamente que é vinculado toohello representação do AD do Azure do usuário.</span><span class="sxs-lookup"><span data-stu-id="0d23e-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - toohave a counterpart of Britta Simon in &frankly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0d23e-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="0d23e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0d23e-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="0d23e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0d23e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d23e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0d23e-149">Nesta seção, você pode habilitar AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu & francamente aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d23e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="0d23e-150">**tooconfigure AD do Azure único logon com & Francamente, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0d23e-150">**tooconfigure Azure AD single sign-on with &frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d23e-151">Em Olá portal do Azure, Olá **& francamente** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="0d23e-151">In hello Azure portal, on hello **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="0d23e-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="0d23e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="0d23e-155">Em Olá **& francamente URLs e domínio** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="0d23e-155">On hello **&frankly Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="0d23e-157">a.</span><span class="sxs-lookup"><span data-stu-id="0d23e-157">a.</span></span> <span data-ttu-id="0d23e-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="0d23e-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="0d23e-159">b.</span><span class="sxs-lookup"><span data-stu-id="0d23e-159">b.</span></span> <span data-ttu-id="0d23e-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="0d23e-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="0d23e-161">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="0d23e-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="0d23e-162">Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="0d23e-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="0d23e-164">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="0d23e-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="0d23e-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="0d23e-165">These values are not real.</span></span> <span data-ttu-id="0d23e-166">Atualizar esses valores com hello identificador real, logon e a URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="0d23e-166">Update these values with hello actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="0d23e-167">Entre em contato com [andfrankly a equipe de suporte](mailto:help@andfrankly.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="0d23e-167">Contact [andfrankly support team](mailto:help@andfrankly.com) tooget these values.</span></span>

5. <span data-ttu-id="0d23e-168">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0d23e-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="0d23e-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0d23e-170">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0d23e-172">tooconfigure logon único no **& francamente** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte andfrankly](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="0d23e-172">tooconfigure single sign-on on **&frankly** side, you need toosend hello downloaded **Metadata XML** too[andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="0d23e-173">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="0d23e-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0d23e-174">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="0d23e-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0d23e-175">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0d23e-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0d23e-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0d23e-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="0d23e-177">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d23e-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="0d23e-179">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0d23e-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d23e-180">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0d23e-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0d23e-182">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="0d23e-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0d23e-184">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d23e-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0d23e-186">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d23e-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0d23e-188">a.</span><span class="sxs-lookup"><span data-stu-id="0d23e-188">a.</span></span> <span data-ttu-id="0d23e-189">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0d23e-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0d23e-190">b.</span><span class="sxs-lookup"><span data-stu-id="0d23e-190">b.</span></span> <span data-ttu-id="0d23e-191">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0d23e-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0d23e-192">c.</span><span class="sxs-lookup"><span data-stu-id="0d23e-192">c.</span></span> <span data-ttu-id="0d23e-193">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="0d23e-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0d23e-194">d.</span><span class="sxs-lookup"><span data-stu-id="0d23e-194">d.</span></span> <span data-ttu-id="0d23e-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0d23e-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="0d23e-196">Criar um usuário de teste do &frankly</span><span class="sxs-lookup"><span data-stu-id="0d23e-196">Creating a &frankly test user</span></span>

<span data-ttu-id="0d23e-197">Nesta seção, você criará uma usuária chamado Brenda Fernandes no &frankly.</span><span class="sxs-lookup"><span data-stu-id="0d23e-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="0d23e-198">Trabalhar com [andfrankly a equipe de suporte](mailto:help@andfrankly.com) tooadd usuários de Olá Olá & francamente plataforma.</span><span class="sxs-lookup"><span data-stu-id="0d23e-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) tooadd hello users in hello &frankly platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0d23e-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0d23e-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0d23e-200">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso muito & francamente.</span><span class="sxs-lookup"><span data-stu-id="0d23e-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too&frankly.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="0d23e-202">**tooassign Britta Simon muito & Francamente, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0d23e-202">**tooassign Britta Simon too&frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d23e-203">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0d23e-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0d23e-205">Na lista de aplicativos hello, selecione **& francamente**.</span><span class="sxs-lookup"><span data-stu-id="0d23e-205">In hello applications list, select **&frankly**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="0d23e-207">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0d23e-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="0d23e-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0d23e-209">Click **Add** button.</span></span> <span data-ttu-id="0d23e-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0d23e-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="0d23e-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d23e-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0d23e-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0d23e-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0d23e-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0d23e-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0d23e-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="0d23e-215">Testing single sign-on</span></span>

<span data-ttu-id="0d23e-216">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="0d23e-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="0d23e-217">Quando você clique Olá & francamente bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour & francamente aplicativo</span><span class="sxs-lookup"><span data-stu-id="0d23e-217">When you click hello &frankly tile in hello Access Panel, you should get automatically signed-on tooyour &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0d23e-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0d23e-218">Additional resources</span></span>

* [<span data-ttu-id="0d23e-219">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0d23e-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d23e-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0d23e-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png

