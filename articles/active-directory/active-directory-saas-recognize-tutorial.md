---
title: "Tutorial: Integração do Azure Active Directory com o Recognize | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e reconhecer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="c7973-103">Tutorial: integração do Azure Active Directory com o Recognize</span><span class="sxs-lookup"><span data-stu-id="c7973-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="c7973-104">Neste tutorial, você aprenderá como toointegrate reconhece com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c7973-104">In this tutorial, you learn how toointegrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7973-105">Integrando reconhecer o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7973-105">Integrating Recognize with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c7973-106">Você pode controlar no AD do Azure que tenha acesso tooRecognize</span><span class="sxs-lookup"><span data-stu-id="c7973-106">You can control in Azure AD who has access tooRecognize</span></span>
- <span data-ttu-id="c7973-107">Você pode habilitar seu usuários tooautomatically get conectado tooRecognize (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7973-107">You can enable your users tooautomatically get signed-on tooRecognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7973-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c7973-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c7973-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7973-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7973-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c7973-110">Prerequisites</span></span>

<span data-ttu-id="c7973-111">integração tooconfigure AD do Azure com reconhecer, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7973-111">tooconfigure Azure AD integration with Recognize, you need hello following items:</span></span>

- <span data-ttu-id="c7973-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7973-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7973-113">Uma assinatura habilitada para logon único do Recognize</span><span class="sxs-lookup"><span data-stu-id="c7973-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7973-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c7973-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7973-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c7973-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7973-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c7973-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7973-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7973-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7973-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c7973-118">Scenario description</span></span>
<span data-ttu-id="c7973-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c7973-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7973-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c7973-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7973-121">Adicionando reconhecer da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c7973-121">Adding Recognize from hello gallery</span></span>
2. <span data-ttu-id="c7973-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7973-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-hello-gallery"></a><span data-ttu-id="c7973-123">Adicionando reconhecer da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c7973-123">Adding Recognize from hello gallery</span></span>
<span data-ttu-id="c7973-124">integração de saudação tooconfigure de reconhecer no AD do Azure, você precisa tooadd reconhecer da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c7973-124">tooconfigure hello integration of Recognize into Azure AD, you need tooadd Recognize from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c7973-125">**tooadd reconhecer da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7973-125">**tooadd Recognize from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7973-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c7973-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7973-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c7973-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c7973-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7973-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c7973-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7973-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c7973-133">Na caixa de pesquisa hello, digite **reconhecer**.</span><span class="sxs-lookup"><span data-stu-id="c7973-133">In hello search box, type **Recognize**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="c7973-135">No painel de resultados de saudação, selecione **reconhecer**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c7973-135">In hello results panel, select **Recognize**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7973-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7973-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7973-138">Nesta seção, você configura e testa o logon único do Azure AD com o Recognize, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c7973-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c7973-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em reconhecer é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7973-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Recognize is tooa user in Azure AD.</span></span> <span data-ttu-id="c7973-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em reconhecer precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c7973-140">In other words, a link relationship between an Azure AD user and hello related user in Recognize needs toobe established.</span></span>

<span data-ttu-id="c7973-141">Reconhecer, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7973-141">In Recognize, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c7973-142">teste do AD do Azure e tooconfigure o logon único com reconhecer, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7973-142">tooconfigure and test Azure AD single sign-on with Recognize, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c7973-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c7973-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c7973-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7973-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7973-145">**[Criar um usuário de teste de reconhecer](#creating-a-recognize-test-user)**  -toohave um equivalente do Britta Simon em reconhecer que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c7973-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - toohave a counterpart of Britta Simon in Recognize that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7973-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c7973-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7973-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c7973-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7973-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7973-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7973-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de reconhecer.</span><span class="sxs-lookup"><span data-stu-id="c7973-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="c7973-150">**tooconfigure AD do Azure-logon único com reconhecer, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7973-150">**tooconfigure Azure AD single sign-on with Recognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7973-151">Em Olá portal do Azure, Olá **reconhecer** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c7973-151">In hello Azure portal, on hello **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c7973-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c7973-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="c7973-155">Em Olá **domínio reconhecer e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7973-155">On hello **Recognize Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="c7973-157">a.</span><span class="sxs-lookup"><span data-stu-id="c7973-157">a.</span></span> <span data-ttu-id="c7973-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="c7973-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="c7973-159">b.</span><span class="sxs-lookup"><span data-stu-id="c7973-159">b.</span></span> <span data-ttu-id="c7973-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="c7973-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7973-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c7973-161">These values are not real.</span></span> <span data-ttu-id="c7973-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="c7973-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c7973-163">Entre em contato com [equipe de suporte do cliente reconhece](mailto:support@recognizeapp.com) obter a URL de logon e você pode obter o valor de identificador abrindo Olá URL de metadados do provedor de serviço de saudação seção de configurações de SSO é explicada posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7973-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening hello Service Provider Metadata URL from hello SSO Settings section that is explained later in hello tutorial.</span></span> <span data-ttu-id="c7973-164">.</span><span class="sxs-lookup"><span data-stu-id="c7973-164">.</span></span> 
 
4. <span data-ttu-id="c7973-165">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c7973-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="c7973-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c7973-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7973-169">Em Olá **configuração reconhecer** seção, clique em **configurar reconhecer** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="c7973-169">On hello **Recognize Configuration** section, click **Configure Recognize** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c7973-170">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="c7973-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="c7973-172">Em uma janela de navegador web diferente, logon tooyour reconhecer locatário como um administrador.</span><span class="sxs-lookup"><span data-stu-id="c7973-172">In a different web browser window, sign-on tooyour Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="c7973-173">Olá canto superior direito, clique em **Menu**.</span><span class="sxs-lookup"><span data-stu-id="c7973-173">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="c7973-174">Vá muito**administrador da empresa**.</span><span class="sxs-lookup"><span data-stu-id="c7973-174">Go too**Company Admin**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="c7973-176">No painel de navegação esquerdo hello, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="c7973-176">On hello left navigation pane, click **Settings**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="c7973-178">Executar Olá seguindo as etapas na **configurações de SSO** seção.</span><span class="sxs-lookup"><span data-stu-id="c7973-178">Perform hello following steps on **SSO Settings** section.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="c7973-180">a.</span><span class="sxs-lookup"><span data-stu-id="c7973-180">a.</span></span> <span data-ttu-id="c7973-181">Em **Habilitar SSO**, selecione **ATIVADO**.</span><span class="sxs-lookup"><span data-stu-id="c7973-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="c7973-182">b.</span><span class="sxs-lookup"><span data-stu-id="c7973-182">b.</span></span> <span data-ttu-id="c7973-183">Em hello **ID da entidade IDP** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7973-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="c7973-184">c.</span><span class="sxs-lookup"><span data-stu-id="c7973-184">c.</span></span> <span data-ttu-id="c7973-185">Em hello **url de destino Sso** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7973-185">In hello **Sso target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="c7973-186">d.</span><span class="sxs-lookup"><span data-stu-id="c7973-186">d.</span></span> <span data-ttu-id="c7973-187">Em Olá **url de destino Slo** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7973-187">In hello **Slo target url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="c7973-188">e.</span><span class="sxs-lookup"><span data-stu-id="c7973-188">e.</span></span> <span data-ttu-id="c7973-189">Abra seu baixado **certificado (Base64)** no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="c7973-189">Open your downloaded **Certificate (Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="c7973-190">f.</span><span class="sxs-lookup"><span data-stu-id="c7973-190">f.</span></span> <span data-ttu-id="c7973-191">Clique em Olá **salvar configurações** botão.</span><span class="sxs-lookup"><span data-stu-id="c7973-191">Click hello **Save settings** button.</span></span> 

11. <span data-ttu-id="c7973-192">Ao lado de saudação **configurações de SSO** seção, copie a URL de saudação em **url de metadados de provedor de serviço**.</span><span class="sxs-lookup"><span data-stu-id="c7973-192">Beside hello **SSO Settings** section, copy hello URL under **Service Provider Metadata url**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="c7973-194">Olá abrir **link de URL de metadados** em um documento de metadados do navegador em branco toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="c7973-194">Open hello **Metadata URL link** under a blank browser toodownload hello metadata document.</span></span> <span data-ttu-id="c7973-195">Copie Olá EntityDescriptor value(entityID) do arquivo hello e cole-o na **identificador** textbox em **seção domínio reconhecer e URLs** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7973-195">Then copy hello EntityDescriptor value(entityID) from hello file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="c7973-197">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c7973-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c7973-198">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c7973-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c7973-199">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7973-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7973-200">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7973-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7973-201">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7973-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c7973-203">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7973-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7973-204">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c7973-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7973-206">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c7973-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7973-208">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7973-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7973-210">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7973-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7973-212">a.</span><span class="sxs-lookup"><span data-stu-id="c7973-212">a.</span></span> <span data-ttu-id="c7973-213">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7973-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7973-214">b.</span><span class="sxs-lookup"><span data-stu-id="c7973-214">b.</span></span> <span data-ttu-id="c7973-215">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c7973-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7973-216">c.</span><span class="sxs-lookup"><span data-stu-id="c7973-216">c.</span></span> <span data-ttu-id="c7973-217">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c7973-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c7973-218">d.</span><span class="sxs-lookup"><span data-stu-id="c7973-218">d.</span></span> <span data-ttu-id="c7973-219">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c7973-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="c7973-220">Criando um usuário de teste do Recognize</span><span class="sxs-lookup"><span data-stu-id="c7973-220">Creating a Recognize test user</span></span>

<span data-ttu-id="c7973-221">Em ordem tooenable AD do Azure usuários toolog em reconhecer, eles devem ser provisionados no reconhecer.</span><span class="sxs-lookup"><span data-stu-id="c7973-221">In order tooenable Azure AD users toolog into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="c7973-222">No caso de saudação de reconhecer, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="c7973-222">In hello case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="c7973-223">Este aplicativo não dá suporte ao provisionamento de SCIM, mas tem uma sincronização de usuário alternativa que provisiona usuários.</span><span class="sxs-lookup"><span data-stu-id="c7973-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="c7973-224">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7973-224">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7973-225">Faça logon em seu site de empresa Recognize como um administrador.</span><span class="sxs-lookup"><span data-stu-id="c7973-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="c7973-226">Olá canto superior direito, clique em **Menu**.</span><span class="sxs-lookup"><span data-stu-id="c7973-226">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="c7973-227">Vá muito**administrador da empresa**.</span><span class="sxs-lookup"><span data-stu-id="c7973-227">Go too**Company Admin**.</span></span>

3. <span data-ttu-id="c7973-228">No painel de navegação esquerdo hello, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="c7973-228">On hello left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="c7973-229">Executar Olá seguindo as etapas na **usuário sincronização** seção.</span><span class="sxs-lookup"><span data-stu-id="c7973-229">Perform hello following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="c7973-230">![Novo Usuário](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="c7973-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="c7973-231">a.</span><span class="sxs-lookup"><span data-stu-id="c7973-231">a.</span></span> <span data-ttu-id="c7973-232">Em **Sincronização habilitada**, selecione **ATIVADO**.</span><span class="sxs-lookup"><span data-stu-id="c7973-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="c7973-233">b.</span><span class="sxs-lookup"><span data-stu-id="c7973-233">b.</span></span> <span data-ttu-id="c7973-234">Em **Escolher o provedor de sincronização**, selecione **Microsoft / Office 365**.</span><span class="sxs-lookup"><span data-stu-id="c7973-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="c7973-235">c.</span><span class="sxs-lookup"><span data-stu-id="c7973-235">c.</span></span> <span data-ttu-id="c7973-236">Clique em **Executar Sincronização de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="c7973-236">Click **Run User Sync**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c7973-237">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7973-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c7973-238">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooRecognize.</span><span class="sxs-lookup"><span data-stu-id="c7973-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRecognize.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c7973-240">**tooassign Britta Simon tooRecognize, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7973-240">**tooassign Britta Simon tooRecognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7973-241">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7973-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c7973-243">Na lista de aplicativos hello, selecione **reconhecer**.</span><span class="sxs-lookup"><span data-stu-id="c7973-243">In hello applications list, select **Recognize**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="c7973-245">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c7973-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c7973-247">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c7973-247">Click **Add** button.</span></span> <span data-ttu-id="c7973-248">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7973-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c7973-250">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7973-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c7973-251">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7973-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7973-252">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7973-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7973-253">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c7973-253">Testing single sign-on</span></span>

<span data-ttu-id="c7973-254">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="c7973-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c7973-255">Quando você clica em um bloco de reconhecer Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour reconhecer aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c7973-255">When you click hello Recognize tile in hello Access Panel, you should get automatically signed-on tooyour Recognize application.</span></span> <span data-ttu-id="c7973-256">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7973-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c7973-257">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c7973-257">Additional resources</span></span>

* [<span data-ttu-id="c7973-258">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c7973-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7973-259">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7973-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

