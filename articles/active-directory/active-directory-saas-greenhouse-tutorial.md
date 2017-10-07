---
title: "Tutorial: integração do Azure Active Directory com o Greenhouse | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Greenhouse."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 1a7cdd00c4f2b15a1afc89522d79af22f4c5d866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="bce26-103">Tutorial: integração do Active Directory do Azure ao Greenhouse</span><span class="sxs-lookup"><span data-stu-id="bce26-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="bce26-104">Neste tutorial, você aprenderá como toointegrate Greenhouse com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="bce26-104">In this tutorial, you learn how toointegrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bce26-105">Integrando Greenhouse com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="bce26-105">Integrating Greenhouse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bce26-106">Você pode controlar no AD do Azure que tenha acesso tooGreenhouse.</span><span class="sxs-lookup"><span data-stu-id="bce26-106">You can control in Azure AD who has access tooGreenhouse.</span></span>
- <span data-ttu-id="bce26-107">Você pode habilitar seu usuários tooautomatically get conectado tooGreenhouse (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bce26-107">You can enable your users tooautomatically get signed-on tooGreenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="bce26-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bce26-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="bce26-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bce26-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bce26-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bce26-110">Prerequisites</span></span>

<span data-ttu-id="bce26-111">tooconfigure integração do AD do Azure com Greenhouse, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="bce26-111">tooconfigure Azure AD integration with Greenhouse, you need hello following items:</span></span>

- <span data-ttu-id="bce26-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bce26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bce26-113">Uma assinatura do Greenhouse habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="bce26-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bce26-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="bce26-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bce26-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="bce26-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bce26-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="bce26-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bce26-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bce26-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bce26-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="bce26-118">Scenario description</span></span>
<span data-ttu-id="bce26-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="bce26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bce26-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="bce26-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bce26-121">Adicionando Greenhouse da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="bce26-121">Adding Greenhouse from hello gallery</span></span>
2. <span data-ttu-id="bce26-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bce26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-hello-gallery"></a><span data-ttu-id="bce26-123">Adicionando Greenhouse da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="bce26-123">Adding Greenhouse from hello gallery</span></span>
<span data-ttu-id="bce26-124">integração de saudação tooconfigure do Greenhouse no AD do Azure, você precisa tooadd Greenhouse da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="bce26-124">tooconfigure hello integration of Greenhouse into Azure AD, you need tooadd Greenhouse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bce26-125">**tooadd Greenhouse da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bce26-125">**tooadd Greenhouse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bce26-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="bce26-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="bce26-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="bce26-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bce26-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bce26-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="bce26-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bce26-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="bce26-133">Na caixa de pesquisa hello, digite **Greenhouse**, selecione **Greenhouse** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bce26-133">In hello search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Efeito na lista de resultados de saudação](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bce26-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bce26-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bce26-136">Nesta seção, você configura e testa o logon único do Azure AD com o Greenhouse, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="bce26-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bce26-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Greenhouse é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bce26-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Greenhouse is tooa user in Azure AD.</span></span> <span data-ttu-id="bce26-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Greenhouse precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="bce26-138">In other words, a link relationship between an Azure AD user and hello related user in Greenhouse needs toobe established.</span></span>

<span data-ttu-id="bce26-139">No Greenhouse, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="bce26-139">In Greenhouse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bce26-140">tooconfigure e teste de logon único do AD do Azure com Greenhouse, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="bce26-140">tooconfigure and test Azure AD single sign-on with Greenhouse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bce26-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="bce26-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bce26-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bce26-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bce26-143">**[Criar um usuário de teste do Greenhouse](#create-a-greenhouse-test-user)**  -toohave um equivalente do Britta Simon no Greenhouse é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="bce26-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - toohave a counterpart of Britta Simon in Greenhouse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bce26-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="bce26-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bce26-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="bce26-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bce26-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bce26-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bce26-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="bce26-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="bce26-148">**tooconfigure AD do Azure-logon único com Greenhouse, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bce26-148">**tooconfigure Azure AD single sign-on with Greenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="bce26-149">Em Olá portal do Azure, Olá **Greenhouse** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="bce26-149">In hello Azure portal, on hello **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="bce26-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="bce26-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. <span data-ttu-id="bce26-153">Em Olá **Greenhouse domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bce26-153">On hello **Greenhouse Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do Greenhouse](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="bce26-155">a.</span><span class="sxs-lookup"><span data-stu-id="bce26-155">a.</span></span> <span data-ttu-id="bce26-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="bce26-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="bce26-157">b.</span><span class="sxs-lookup"><span data-stu-id="bce26-157">b.</span></span> <span data-ttu-id="bce26-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="bce26-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bce26-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="bce26-159">These values are not real.</span></span> <span data-ttu-id="bce26-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="bce26-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bce26-161">Entre em contato com [equipe de suporte do Greenhouse cliente](https://www.greenhouse.io/contact) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="bce26-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) tooget these values.</span></span> 
 


4. <span data-ttu-id="bce26-162">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="bce26-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. <span data-ttu-id="bce26-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="bce26-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bce26-166">tooconfigure logon único no **Greenhouse** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do Greenhouse](http://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="bce26-166">tooconfigure single sign-on on **Greenhouse** side, you need toosend hello downloaded **Metadata XML** too[Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="bce26-167">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="bce26-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bce26-168">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="bce26-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bce26-169">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bce26-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bce26-170">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bce26-170">Create an Azure AD test user</span></span>

<span data-ttu-id="bce26-171">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bce26-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="bce26-173">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bce26-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bce26-174">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="bce26-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bce26-176">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bce26-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bce26-178">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bce26-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bce26-180">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bce26-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="bce26-182">a.</span><span class="sxs-lookup"><span data-stu-id="bce26-182">a.</span></span> <span data-ttu-id="bce26-183">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bce26-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bce26-184">b.</span><span class="sxs-lookup"><span data-stu-id="bce26-184">b.</span></span> <span data-ttu-id="bce26-185">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bce26-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="bce26-186">c.</span><span class="sxs-lookup"><span data-stu-id="bce26-186">c.</span></span> <span data-ttu-id="bce26-187">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="bce26-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="bce26-188">d.</span><span class="sxs-lookup"><span data-stu-id="bce26-188">d.</span></span> <span data-ttu-id="bce26-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="bce26-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="bce26-190">Criar um usuário de teste do Greenhouse</span><span class="sxs-lookup"><span data-stu-id="bce26-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="bce26-191">Em ordem tooenable AD do Azure usuários toolog no Greenhouse, eles devem ser provisionados no Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="bce26-191">In order tooenable Azure AD users toolog into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="bce26-192">No caso de saudação do Greenhouse, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="bce26-192">In hello case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="bce26-193">Você pode usar qualquer ferramenta de criação outros Greenhouse usuário conta ou APIs fornecidas pelo Greenhouse tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="bce26-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="bce26-194">**tooprovision contas de usuário, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="bce26-194">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="bce26-195">Faça logon no tooyour **Greenhouse** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="bce26-195">Log in tooyour **Greenhouse** company site as an administrator.</span></span>

2. <span data-ttu-id="bce26-196">No menu de saudação na parte superior de saudação, clique em **configurar**e, em seguida, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="bce26-196">In hello menu on hello top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="bce26-197">![Usuários](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="bce26-197">![Users](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Users")</span></span>

3. <span data-ttu-id="bce26-198">Clique em **Novos Usuários**.</span><span class="sxs-lookup"><span data-stu-id="bce26-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="bce26-199">![Novo Usuário](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="bce26-199">![New User](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "New User")</span></span>

4. <span data-ttu-id="bce26-200">Em Olá **adicionar novo usuário** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bce26-200">In hello **Add New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="bce26-201">![Adicionar Novo Usuário](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Adicionar Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="bce26-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="bce26-202">a.</span><span class="sxs-lookup"><span data-stu-id="bce26-202">a.</span></span> <span data-ttu-id="bce26-203">Em Olá **inserir emails do usuário** caixa de texto, endereço de email de saudação do tipo de uma conta válida do Active Directory do Azure você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="bce26-203">In hello **Enter user emails** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision.</span></span>

   <span data-ttu-id="bce26-204">b.</span><span class="sxs-lookup"><span data-stu-id="bce26-204">b.</span></span> <span data-ttu-id="bce26-205">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bce26-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="bce26-206">os proprietários de contas do Active Directory do Azure Olá receberão um email incluindo uma conta de saudação do link tooconfirm antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="bce26-206">hello Azure Active Directory account holders will receive an email including a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="bce26-207">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bce26-207">Assign hello Azure AD test user</span></span>

<span data-ttu-id="bce26-208">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooGreenhouse.</span><span class="sxs-lookup"><span data-stu-id="bce26-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGreenhouse.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="bce26-210">**tooassign Britta Simon tooGreenhouse, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bce26-210">**tooassign Britta Simon tooGreenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="bce26-211">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bce26-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="bce26-213">Na lista de aplicativos hello, selecione **Greenhouse**.</span><span class="sxs-lookup"><span data-stu-id="bce26-213">In hello applications list, select **Greenhouse**.</span></span>

    ![link de emissões Olá na lista de aplicativos Olá](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. <span data-ttu-id="bce26-215">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="bce26-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="bce26-217">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bce26-217">Click **Add** button.</span></span> <span data-ttu-id="bce26-218">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bce26-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="bce26-220">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="bce26-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bce26-221">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bce26-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bce26-222">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bce26-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bce26-223">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="bce26-223">Test single sign-on</span></span>

<span data-ttu-id="bce26-224">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="bce26-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bce26-225">Quando você clica em bloco Greenhouse Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="bce26-225">When you click hello Greenhouse tile in hello Access Panel, you should get automatically signed-on tooyour Greenhouse application.</span></span>
<span data-ttu-id="bce26-226">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bce26-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bce26-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="bce26-227">Additional resources</span></span>

* [<span data-ttu-id="bce26-228">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="bce26-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bce26-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bce26-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png

