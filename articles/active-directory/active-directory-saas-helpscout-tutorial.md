---
title: "Tutorial: Integração do Azure Active Directory com o Help Scout | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Scout ajuda."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="c9e04-103">Tutorial: integração do Azure Active Directory com o Help Scout</span><span class="sxs-lookup"><span data-stu-id="c9e04-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="c9e04-104">Neste tutorial, você aprenderá como toointegrate ajuda atendente com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c9e04-104">In this tutorial, you learn how toointegrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9e04-105">Você obtém Olá seguindo os benefícios da integração Scout ajudar com o Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c9e04-105">You get hello following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="c9e04-106">No AD do Azure, você pode controlar quem tem acesso tooHelp Scout.</span><span class="sxs-lookup"><span data-stu-id="c9e04-106">In Azure AD, you can control who has access tooHelp Scout.</span></span>
- <span data-ttu-id="c9e04-107">Você pode entrar automaticamente no seu tooHelp usuários Scout usando logon único e uma conta de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e04-107">You can automatically sign in your users tooHelp Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="c9e04-108">Você pode gerenciar suas contas em um local central, Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e04-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="c9e04-109">toolearn mais sobre o software como uma integração de aplicativo de serviço (SaaS) com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c9e04-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9e04-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c9e04-110">Prerequisites</span></span>

<span data-ttu-id="c9e04-111">tooset a integração do AD do Azure com Scout ajuda, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9e04-111">tooset up Azure AD integration with Help Scout, you need hello following items:</span></span>

- <span data-ttu-id="c9e04-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c9e04-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c9e04-113">Uma assinatura do Help Scout, com o logon único ativado</span><span class="sxs-lookup"><span data-stu-id="c9e04-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="c9e04-114">Se você testar etapas Olá neste tutorial, é recomendável que você não testá-las em um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c9e04-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="c9e04-115">Recomendações para testar etapas Olá neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="c9e04-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="c9e04-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c9e04-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="c9e04-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9e04-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9e04-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c9e04-118">Scenario description</span></span>
<span data-ttu-id="c9e04-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c9e04-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="c9e04-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c9e04-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9e04-121">Adicione Scout ajuda da Galeria de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9e04-121">Add Help Scout from hello gallery.</span></span>
2. <span data-ttu-id="c9e04-122">Configurar e testar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9e04-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-hello-gallery"></a><span data-ttu-id="c9e04-123">Adicionar Scout ajuda da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c9e04-123">Add Help Scout from hello gallery</span></span>
<span data-ttu-id="c9e04-124">tooset a integração de saudação do Scout ajudar com o AD do Azure, na Galeria de hello, adicionar lista de tooyour de ajudar Scout de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c9e04-124">tooset up hello integration of Help Scout with Azure AD, in hello gallery, add Help Scout tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c9e04-125">tooadd Scout ajuda da Galeria de saudação:</span><span class="sxs-lookup"><span data-stu-id="c9e04-125">tooadd Help Scout from hello gallery:</span></span>

1. <span data-ttu-id="c9e04-126">Em Olá [portal do Azure](https://portal.azure.com), no hello menu à esquerda, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="c9e04-128">Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![página de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="c9e04-130">tooadd um novo aplicativo, selecione **novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-130">tooadd a new application, select **New application**.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="c9e04-132">Na caixa de pesquisa hello, digite **Scout ajuda**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-132">In hello search box, enter **Help Scout**.</span></span> <span data-ttu-id="c9e04-133">Nos resultados da pesquisa hello, selecione **ajuda Scout**e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-133">In hello search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Ajuda Scout na lista de resultados de saudação](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c9e04-135">Configurar e testar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9e04-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="c9e04-136">Nesta seção, você vai configurar e testar o logon único do Azure AD com o Help Scout, com base em uma usuária de teste chamada *Brenda Fernandes*.</span><span class="sxs-lookup"><span data-stu-id="c9e04-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="c9e04-137">Para toowork de logon único, o AD do Azure precisa tooknow Olá AD do Azure contraparte usuário Scout ajuda.</span><span class="sxs-lookup"><span data-stu-id="c9e04-137">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="c9e04-138">Uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Scout ajuda deve ser estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c9e04-138">A link relationship between an Azure AD user and hello related user in Help Scout must be established.</span></span>

<span data-ttu-id="c9e04-139">Olá tooestablish referente à relação, na Ajuda Scout, **Username**, atribuir valor Olá Olá **nome de usuário** no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e04-139">tooestablish hello link relationship, in Help Scout, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="c9e04-140">tooconfigure e teste de logon único do AD do Azure com Scout ajudar, Olá concluir tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9e04-140">tooconfigure and test Azure AD single sign-on with Help Scout, complete hello following tasks:</span></span>

1. <span data-ttu-id="c9e04-141">[Configurar o logon único do Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="c9e04-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="c9e04-142">Configura um usuário toouse esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c9e04-142">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="c9e04-143">[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="c9e04-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="c9e04-144">Testes do AD do Azure-logon único com o usuário Olá Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9e04-144">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="c9e04-145">[Criar um usuário de teste do Help Scout](#create-a-help-scout-test-user).</span><span class="sxs-lookup"><span data-stu-id="c9e04-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="c9e04-146">Cria um equivalente de Britta Simon Scout ajuda que é vinculado toohello representação do AD do Azure do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="c9e04-146">Creates a counterpart of Britta Simon in Help Scout that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="c9e04-147">[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="c9e04-147">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="c9e04-148">Define o Britta Simon toouse logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e04-148">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9e04-149">[Testar o logon único](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="c9e04-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="c9e04-150">Verifica que se a configuração de saudação funciona.</span><span class="sxs-lookup"><span data-stu-id="c9e04-150">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="c9e04-151">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9e04-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="c9e04-152">Nesta seção, você deve configurar o AD do Azure-logon único no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9e04-152">In this section, you set up Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="c9e04-153">Em seguida, define o logon único no aplicativo Help Scout.</span><span class="sxs-lookup"><span data-stu-id="c9e04-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="c9e04-154">tooset o AD do Azure-logon único com Scout ajuda:</span><span class="sxs-lookup"><span data-stu-id="c9e04-154">tooset up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="c9e04-155">Em Olá portal do Azure, Olá **ajuda Scout** página de integração de aplicativos, selecione **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-155">In hello Azure portal, on hello **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Link Configurar logon único][4]

2. <span data-ttu-id="c9e04-157">Em Olá **o logon único** página, para **modo**, selecione **baseado no SAML logon**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-157">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="c9e04-159">Em **ajuda Scout domínio e URLs**, se você quiser tooset o aplicativo hello no modo iniciado pelo IDP, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9e04-159">Under **Help Scout Domain and URLs**, if you want tooset up hello application in IDP-initiated mode, complete hello following steps:</span></span>

    1. <span data-ttu-id="c9e04-160">Em Olá **identificador** caixa, digite uma URL que tenha o saudação padrão a seguir:`urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="c9e04-160">In hello **Identifier** box, enter a URL that has hello following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="c9e04-161">Em Olá **URL de resposta** caixa, digite uma URL que tenha o saudação padrão a seguir:`https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="c9e04-161">In hello **Reply URL** box, enter a URL that has hello following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Informações de logon único de Domínio e URLs do Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="c9e04-163">Se você quiser tooset o aplicativo hello no modo iniciado pelo SP, selecione Olá **Mostrar configurações de URL avançadas** caixa de seleção e, em seguida, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9e04-163">If you want tooset up hello application in SP-initiated mode, select hello **Show advanced URL settings** check box, and then do hello following:</span></span>

    * <span data-ttu-id="c9e04-164">Em Olá **URL de logon** , digite uma URL com hello formato a seguir:`https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="c9e04-164">In hello **Sign on URL** box, enter a URL that has hello following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Informações de logon único de Domínio e URLs do Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="c9e04-166">valores Hello essas URLs são apenas para demonstração.</span><span class="sxs-lookup"><span data-stu-id="c9e04-166">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="c9e04-167">Atualize valores de saudação com URL de identificador real de saudação e a URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="c9e04-167">Update hello values with hello actual identifier URL and reply URL.</span></span> <span data-ttu-id="c9e04-168">entre em contato com tooget esses valores, [a equipe de suporte Scout ajuda](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="c9e04-168">tooget these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="c9e04-169">Em **o certificado de autenticação SAML**, selecione **Metadata XML**e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c9e04-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="c9e04-171">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-171">Select **Save**.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c9e04-173">tooset backup único logon no lado de ajuda Scout hello, enviar Olá baixado metadados XML arquivo toohello [a equipe de suporte Scout ajuda](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="c9e04-173">tooset up single sign-on on hello Help Scout side, send hello downloaded metadata XML file toohello [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="c9e04-174">a equipe de suporte de ajuda Scout Olá aplica essa configuração para que Olá SAML único logon conexão está definida corretamente nos dois lados.</span><span class="sxs-lookup"><span data-stu-id="c9e04-174">hello Help Scout support team applies this setting so that hello SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c9e04-175">Você pode ler uma versão concisa essas instruções Olá [portal do Azure](https://portal.azure.com), enquanto você estiver configurando seu aplicativo!</span><span class="sxs-lookup"><span data-stu-id="c9e04-175">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="c9e04-176">Depois de adicionar o aplicativo hello selecionando **do Active Directory** > **aplicativos empresariais**, selecione Olá **Single Sign-On** guia. Você pode acessar a documentação Olá inserido em Olá **configuração** seção final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="c9e04-176">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="c9e04-177">Para saber mais, confira a [documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c9e04-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c9e04-178">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9e04-178">Create an Azure AD test user</span></span>

<span data-ttu-id="c9e04-179">Nesta seção, no hello portal do Azure, você deve criar um usuário de teste chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9e04-179">In this section, in hello Azure portal, you create a test user named Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="c9e04-181">toocreate um usuário de teste no AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="c9e04-181">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="c9e04-182">No hello portal do Azure, no menu da esquerda hello, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-182">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c9e04-184">lista de saudação do toodisplay de usuários, selecionados **usuários e grupos**e, em seguida, selecione **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-184">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Selecionar Usuários e grupos e depois Todos os usuários](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c9e04-186">Olá tooopen **usuário** caixa de diálogo, na parte superior de saudação do hello **todos os usuários** página, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-186">tooopen hello **User** dialog box, at hello top of hello **All Users** page, select **Add**.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c9e04-188">Em Olá **usuário** caixa de diálogo, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9e04-188">In hello **User** dialog box, complete hello following steps:</span></span>

    1. <span data-ttu-id="c9e04-189">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-189">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="c9e04-190">Em Olá **nome de usuário** , digite o endereço de email de saudação do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9e04-190">In hello **User name** box, enter hello email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="c9e04-191">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="c9e04-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="c9e04-192">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-192">Select **Create**.</span></span>

        ![caixa de diálogo de usuário Olá](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="c9e04-194">Criar um usuário de teste do Help Scout</span><span class="sxs-lookup"><span data-stu-id="c9e04-194">Create a Help Scout test user</span></span>

<span data-ttu-id="c9e04-195">objeto Olá desta seção é toocreate um usuário chamado Britta Simon em Scout ajuda.</span><span class="sxs-lookup"><span data-stu-id="c9e04-195">hello object of this section is toocreate a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="c9e04-196">O Help Scout dá suporte ao provisionamento JIT (Just-In-Time), que é ativado por padrão.</span><span class="sxs-lookup"><span data-stu-id="c9e04-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="c9e04-197">Nesta seção, não há nenhum toocomplete de ação ou tarefa.</span><span class="sxs-lookup"><span data-stu-id="c9e04-197">In this section, there's no action or task toocomplete.</span></span> <span data-ttu-id="c9e04-198">Se um usuário não existir no Scout ajudar, um novo é criado quando você tenta tooaccess Scout ajuda.</span><span class="sxs-lookup"><span data-stu-id="c9e04-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt tooaccess Help Scout.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c9e04-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c9e04-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c9e04-200">Nesta seção, você permitir que usuário Olá Britta Simon toouse AD do Azure-logon único concedendo Olá usuário conta acesso tooHelp Scout.</span><span class="sxs-lookup"><span data-stu-id="c9e04-200">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooHelp Scout.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="c9e04-202">tooassign Britta Simon tooHelp Scout:</span><span class="sxs-lookup"><span data-stu-id="c9e04-202">tooassign Britta Simon tooHelp Scout:</span></span>

1. <span data-ttu-id="c9e04-203">No portal do Azure de Olá, abrir modo de exibição de aplicativos hello e vá toohello exibição de diretório.</span><span class="sxs-lookup"><span data-stu-id="c9e04-203">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="c9e04-204">Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c9e04-206">Na lista de aplicativos hello, selecione **Scout ajuda**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-206">In hello applications list, select **Help Scout**.</span></span>

    ![link de ajuda Scout Olá na lista de aplicativos Olá](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="c9e04-208">No menu à esquerda do hello, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-208">In hello left menu, select **Users and groups**.</span></span>

    ![Olá usuários e grupos de link][202]

4. <span data-ttu-id="c9e04-210">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-210">Select **Add**.</span></span> <span data-ttu-id="c9e04-211">Em seguida, na Olá **Adicionar atribuição** página, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-211">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="c9e04-213">Em Olá **usuários e grupos** página, na lista de saudação de usuários, selecionados **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-213">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="c9e04-214">Em Olá **usuários e grupos** página, selecione **selecione**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-214">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="c9e04-215">Em Olá **Adicionar atribuição** página, selecione **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="c9e04-215">On hello **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c9e04-216">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="c9e04-216">Test single sign-on</span></span>

<span data-ttu-id="c9e04-217">Nesta seção, você pode testar a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9e04-217">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="c9e04-218">Quando você seleciona lado a lado Olá Scout ajuda no painel de acesso hello, você deve ser conectado automaticamente tooyour aplicativo Scout ajuda.</span><span class="sxs-lookup"><span data-stu-id="c9e04-218">When you select hello Help Scout tile in hello access panel, you should be automatically signed in tooyour Help Scout application.</span></span>

<span data-ttu-id="c9e04-219">Para obter mais informações sobre o painel de acesso, consulte [painel de acesso Introdução toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c9e04-219">For more information about the access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c9e04-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c9e04-220">Additional resources</span></span>

* [<span data-ttu-id="c9e04-221">Lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c9e04-221">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9e04-222">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c9e04-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

