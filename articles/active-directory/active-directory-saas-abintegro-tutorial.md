---
title: "Tutorial: Integração do Azure Active Directory com Abintegro | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Abintegro."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99287e1f-4189-494a-97c8-e1c03d047fd3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 54e2865860940cab0c0ef31a496f42dd55b0e907
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-abintegro"></a><span data-ttu-id="24087-103">Tutorial: Integração do Active Directory do Azure ao Abintegro</span><span class="sxs-lookup"><span data-stu-id="24087-103">Tutorial: Azure Active Directory integration with Abintegro</span></span>

<span data-ttu-id="24087-104">Neste tutorial, você aprenderá como toointegrate Abintegro com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="24087-104">In this tutorial, you learn how toointegrate Abintegro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24087-105">Integrando Abintegro com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="24087-105">Integrating Abintegro with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="24087-106">Você pode controlar no AD do Azure que tenha acesso tooAbintegro</span><span class="sxs-lookup"><span data-stu-id="24087-106">You can control in Azure AD who has access tooAbintegro</span></span>
- <span data-ttu-id="24087-107">Você pode habilitar seu usuários tooautomatically get conectado tooAbintegro (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24087-107">You can enable your users tooautomatically get signed-on tooAbintegro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24087-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="24087-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="24087-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="24087-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24087-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="24087-110">Prerequisites</span></span>

<span data-ttu-id="24087-111">tooconfigure integração do AD do Azure com Abintegro, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="24087-111">tooconfigure Azure AD integration with Abintegro, you need hello following items:</span></span>

- <span data-ttu-id="24087-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24087-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24087-113">Uma assinatura habilitada para logon único do Abintegro</span><span class="sxs-lookup"><span data-stu-id="24087-113">An Abintegro single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24087-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="24087-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24087-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="24087-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24087-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="24087-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24087-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24087-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24087-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="24087-118">Scenario description</span></span>
<span data-ttu-id="24087-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="24087-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24087-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="24087-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24087-121">Adicionando Abintegro da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="24087-121">Adding Abintegro from hello gallery</span></span>
2. <span data-ttu-id="24087-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24087-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-abintegro-from-hello-gallery"></a><span data-ttu-id="24087-123">Adicionando Abintegro da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="24087-123">Adding Abintegro from hello gallery</span></span>
<span data-ttu-id="24087-124">integração de saudação tooconfigure do Abintegro no AD do Azure, você precisa tooadd Abintegro da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="24087-124">tooconfigure hello integration of Abintegro into Azure AD, you need tooadd Abintegro from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="24087-125">**tooadd Abintegro da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="24087-125">**tooadd Abintegro from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="24087-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="24087-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="24087-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="24087-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="24087-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="24087-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="24087-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24087-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="24087-133">Na caixa de pesquisa hello, digite **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="24087-133">In hello search box, type **Abintegro**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_search.png)

5. <span data-ttu-id="24087-135">No painel de resultados de saudação, selecione **Abintegro**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="24087-135">In hello results panel, select **Abintegro**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="24087-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24087-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="24087-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Abintegro, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="24087-138">In this section, you configure and test Azure AD single sign-on with Abintegro based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="24087-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Abintegro é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="24087-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Abintegro is tooa user in Azure AD.</span></span> <span data-ttu-id="24087-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Abintegro precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="24087-140">In other words, a link relationship between an Azure AD user and hello related user in Abintegro needs toobe established.</span></span>

<span data-ttu-id="24087-141">No Abintegro, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="24087-141">In Abintegro, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="24087-142">tooconfigure e teste de logon único do AD do Azure com Abintegro, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="24087-142">tooconfigure and test Azure AD single sign-on with Abintegro, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="24087-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="24087-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="24087-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="24087-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24087-145">**[Criar um usuário de teste Abintegro](#creating-an-abintegro-test-user)**  -toohave um equivalente do Britta Simon no Abintegro é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="24087-145">**[Creating an Abintegro test user](#creating-an-abintegro-test-user)** - toohave a counterpart of Britta Simon in Abintegro that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="24087-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="24087-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24087-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="24087-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="24087-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="24087-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="24087-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Abintegro.</span><span class="sxs-lookup"><span data-stu-id="24087-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Abintegro application.</span></span>

<span data-ttu-id="24087-150">**tooconfigure AD do Azure-logon único com Abintegro, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="24087-150">**tooconfigure Azure AD single sign-on with Abintegro, perform hello following steps:**</span></span>

1. <span data-ttu-id="24087-151">Em Olá portal do Azure, Olá **Abintegro** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="24087-151">In hello Azure portal, on hello **Abintegro** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="24087-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="24087-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_samlbase.png)

3. <span data-ttu-id="24087-155">Em Olá **Abintegro domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="24087-155">On hello **Abintegro Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_url.png)

    <span data-ttu-id="24087-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span><span class="sxs-lookup"><span data-stu-id="24087-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="24087-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="24087-158">This value is not real.</span></span> <span data-ttu-id="24087-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="24087-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="24087-160">Entre em contato com [a equipe de suporte Abintegro cliente](mailto:support@abintegro.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="24087-160">Contact [Abintegro Client support team](mailto:support@abintegro.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="24087-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="24087-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_certificate.png) 

5. <span data-ttu-id="24087-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="24087-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-abintegro-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="24087-165">tooconfigure logon único no **Abintegro** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte Abintegro](mailto:support@abintegro.com).</span><span class="sxs-lookup"><span data-stu-id="24087-165">tooconfigure single sign-on on **Abintegro** side, you need toosend hello downloaded **Metadata XML** too[Abintegro support team](mailto:support@abintegro.com).</span></span> <span data-ttu-id="24087-166">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="24087-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="24087-167">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="24087-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="24087-168">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="24087-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="24087-169">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24087-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="24087-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24087-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="24087-171">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="24087-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="24087-173">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="24087-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="24087-174">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="24087-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-abintegro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="24087-176">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="24087-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-abintegro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="24087-178">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="24087-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-abintegro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="24087-180">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="24087-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-abintegro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24087-182">a.</span><span class="sxs-lookup"><span data-stu-id="24087-182">a.</span></span> <span data-ttu-id="24087-183">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="24087-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24087-184">b.</span><span class="sxs-lookup"><span data-stu-id="24087-184">b.</span></span> <span data-ttu-id="24087-185">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="24087-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24087-186">c.</span><span class="sxs-lookup"><span data-stu-id="24087-186">c.</span></span> <span data-ttu-id="24087-187">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="24087-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="24087-188">d.</span><span class="sxs-lookup"><span data-stu-id="24087-188">d.</span></span> <span data-ttu-id="24087-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="24087-189">Click **Create**.</span></span>
 
### <a name="creating-an-abintegro-test-user"></a><span data-ttu-id="24087-190">Criação de um usuário de teste Abintegro</span><span class="sxs-lookup"><span data-stu-id="24087-190">Creating an Abintegro test user</span></span>

<span data-ttu-id="24087-191">Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooAbintegro.</span><span class="sxs-lookup"><span data-stu-id="24087-191">There is no action item for you tooconfigure user provisioning tooAbintegro.</span></span> <span data-ttu-id="24087-192">Quando um usuário atribuído tenta toolog no Abintegro usando o painel de acesso hello, Abintegro verifica se o usuário Olá existe.</span><span class="sxs-lookup"><span data-stu-id="24087-192">When an assigned user tries toolog into Abintegro using hello access panel, Abintegro checks whether hello user exists.</span></span>
  
<span data-ttu-id="24087-193">Se ainda não houver conta de usuário disponível, ela será criada automaticamente pelo Abintegro.</span><span class="sxs-lookup"><span data-stu-id="24087-193">If there is no user account available yet, it is automatically created by Abintegro.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="24087-194">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24087-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="24087-195">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAbintegro.</span><span class="sxs-lookup"><span data-stu-id="24087-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbintegro.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="24087-197">**tooassign Britta Simon tooAbintegro, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="24087-197">**tooassign Britta Simon tooAbintegro, perform hello following steps:**</span></span>

1. <span data-ttu-id="24087-198">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="24087-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="24087-200">Na lista de aplicativos hello, selecione **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="24087-200">In hello applications list, select **Abintegro**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_app.png) 

3. <span data-ttu-id="24087-202">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="24087-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="24087-204">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="24087-204">Click **Add** button.</span></span> <span data-ttu-id="24087-205">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24087-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="24087-207">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="24087-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="24087-208">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24087-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24087-209">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24087-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="24087-210">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="24087-210">Testing single sign-on</span></span>

<span data-ttu-id="24087-211">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="24087-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="24087-212">Quando você clica em bloco Abintegro Olá Olá painel de acesso, você deve obter a página de logon do aplicativo Abintegro.</span><span class="sxs-lookup"><span data-stu-id="24087-212">When you click hello Abintegro tile in hello Access Panel, you should get login page of Abintegro application.</span></span>
<span data-ttu-id="24087-213">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="24087-213">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="24087-214">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="24087-214">Additional resources</span></span>

* [<span data-ttu-id="24087-215">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="24087-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24087-216">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="24087-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_203.png

