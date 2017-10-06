---
title: "Tutorial: Integração do Azure Active Directory ao 123ContactForm | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e 123ContactForm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 931255887845edd1aa7f53b9051a82a2f898e055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="4e8c0-103">Tutorial: Integração do Azure Active Directory ao 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="4e8c0-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="4e8c0-104">Neste tutorial, você aprenderá como 123ContactForm toointegrate com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="4e8c0-104">In this tutorial, you learn how toointegrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4e8c0-105">Integrando 123ContactForm com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e8c0-105">Integrating 123ContactForm with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4e8c0-106">Você pode controlar no AD do Azure que tenha acesso too123ContactForm</span><span class="sxs-lookup"><span data-stu-id="4e8c0-106">You can control in Azure AD who has access too123ContactForm</span></span>
- <span data-ttu-id="4e8c0-107">Você pode habilitar seus usuários tooautomatically get conectado too123ContactForm (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4e8c0-107">You can enable your users tooautomatically get signed-on too123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4e8c0-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4e8c0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4e8c0-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4e8c0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e8c0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4e8c0-110">Prerequisites</span></span>

<span data-ttu-id="4e8c0-111">tooconfigure integração do AD do Azure com 123ContactForm, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e8c0-111">tooconfigure Azure AD integration with 123ContactForm, you need hello following items:</span></span>

- <span data-ttu-id="4e8c0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4e8c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4e8c0-113">Uma assinatura habilitada para logon único do 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="4e8c0-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4e8c0-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4e8c0-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4e8c0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4e8c0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4e8c0-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4e8c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4e8c0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4e8c0-118">Scenario description</span></span>
<span data-ttu-id="4e8c0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4e8c0-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="4e8c0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4e8c0-121">Adicionando 123ContactForm da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4e8c0-121">Adding 123ContactForm from hello gallery</span></span>
2. <span data-ttu-id="4e8c0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4e8c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-hello-gallery"></a><span data-ttu-id="4e8c0-123">Adicionando 123ContactForm da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4e8c0-123">Adding 123ContactForm from hello gallery</span></span>
<span data-ttu-id="4e8c0-124">integração de saudação tooconfigure de 123ContactForm no AD do Azure, você precisa 123ContactForm tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-124">tooconfigure hello integration of 123ContactForm into Azure AD, you need tooadd 123ContactForm from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4e8c0-125">**123ContactForm tooadd da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4e8c0-125">**tooadd 123ContactForm from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e8c0-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4e8c0-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4e8c0-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4e8c0-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4e8c0-133">Na caixa de pesquisa hello, digite **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-133">In hello search box, type **123ContactForm**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="4e8c0-135">No painel de resultados de saudação, selecione **123ContactForm**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-135">In hello results panel, select **123ContactForm**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4e8c0-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4e8c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4e8c0-138">Nesta seção, você configura e testa o logon único do Azure AD com o 123ContactForm, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4e8c0-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em 123ContactForm é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 123ContactForm is tooa user in Azure AD.</span></span> <span data-ttu-id="4e8c0-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em 123ContactForm precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-140">In other words, a link relationship between an Azure AD user and hello related user in 123ContactForm needs toobe established.</span></span>

<span data-ttu-id="4e8c0-141">123ContactForm, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-141">In 123ContactForm, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4e8c0-142">tooconfigure e teste de logon único do AD do Azure com 123ContactForm, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e8c0-142">tooconfigure and test Azure AD single sign-on with 123ContactForm, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4e8c0-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4e8c0-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4e8c0-145">**[Criar um usuário de teste 123ContactForm](#creating-a-123contactform-test-user)**  -toohave um equivalente do Britta Simon em 123ContactForm é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - toohave a counterpart of Britta Simon in 123ContactForm that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4e8c0-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4e8c0-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4e8c0-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e8c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4e8c0-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="4e8c0-150">**tooconfigure AD do Azure-logon único com 123ContactForm, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4e8c0-150">**tooconfigure Azure AD single sign-on with 123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e8c0-151">Em Olá portal do Azure, Olá **123ContactForm** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-151">In hello Azure portal, on hello **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4e8c0-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="4e8c0-155">Em Olá **123ContactForm domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e8c0-155">On hello **123ContactForm Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="4e8c0-157">a.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-157">a.</span></span> <span data-ttu-id="4e8c0-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="4e8c0-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="4e8c0-159">b.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-159">b.</span></span> <span data-ttu-id="4e8c0-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="4e8c0-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="4e8c0-161">Se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e8c0-161">If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="4e8c0-163">a.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-163">a.</span></span> <span data-ttu-id="4e8c0-164">Clique em Olá **Mostrar configurações de URL avançadas** opção</span><span class="sxs-lookup"><span data-stu-id="4e8c0-164">Click hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="4e8c0-165">b.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-165">b.</span></span> <span data-ttu-id="4e8c0-166">Em Olá **URL de logon** caixa de texto, digite um URL como:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="4e8c0-166">In hello **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4e8c0-167">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-167">These values are not real.</span></span> <span data-ttu-id="4e8c0-168">Você precisará tooupdate esses valor de real URLs e identificador que é explicada posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-168">You'll need tooupdate these value from actual URLs and Identifier which is explained later in hello tutorial.</span></span>
    
5. <span data-ttu-id="4e8c0-169">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="4e8c0-171">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4e8c0-171">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4e8c0-173">tooconfigure logon único no **123ContactForm** lado, vá muito[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e8c0-173">tooconfigure single sign-on on **123ContactForm** side, go too[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="4e8c0-175">a.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-175">a.</span></span> <span data-ttu-id="4e8c0-176">Em Olá **Email** caixa de texto, tipo hello email ou de usuário seja Olá</span><span class="sxs-lookup"><span data-stu-id="4e8c0-176">In hello **Email** textbox, type hello email of hello user i.e</span></span> <span data-ttu-id="4e8c0-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="4e8c0-178">b.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-178">b.</span></span> <span data-ttu-id="4e8c0-179">Clique em **carregar** e procurar Olá arquivo XML de Metadata, que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-179">Click **Upload** and browse hello Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="4e8c0-180">c.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-180">c.</span></span> <span data-ttu-id="4e8c0-181">Clique em **ENVIAR FORMULÁRIO**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="4e8c0-182">Em Olá **configurações do Microsoft Azure AD-Single sign on - configurar aplicativo** executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e8c0-182">On hello **Microsoft Azure AD - Single sign-on - Configure App Settings** perform hello following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="4e8c0-184">a.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-184">a.</span></span> <span data-ttu-id="4e8c0-185">Se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**, Olá cópia **identificador** para sua instância de valor e cole-o na **identificador** textbox em **123ContactForm domínio e URLs** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-185">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="4e8c0-186">b.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-186">b.</span></span> <span data-ttu-id="4e8c0-187">Se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**, Olá cópia **URL de resposta** para sua instância de valor e cole-o na **URL de resposta** textbox em **123ContactForm domínio e URLs** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-187">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="4e8c0-188">c.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-188">c.</span></span> <span data-ttu-id="4e8c0-189">Se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, Olá cópia **SIGN ON URL** para sua instância de valor e cole-o na **URL de logon** textbox em **123ContactForm domínio e URLs** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-189">If you wish tooconfigure hello application in **SP initiated mode**, copy hello **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="4e8c0-190">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="4e8c0-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4e8c0-191">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4e8c0-192">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4e8c0-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4e8c0-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4e8c0-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="4e8c0-194">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4e8c0-196">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4e8c0-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e8c0-197">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4e8c0-199">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4e8c0-201">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4e8c0-203">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e8c0-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4e8c0-205">a.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-205">a.</span></span> <span data-ttu-id="4e8c0-206">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4e8c0-207">b.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-207">b.</span></span> <span data-ttu-id="4e8c0-208">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4e8c0-209">c.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-209">c.</span></span> <span data-ttu-id="4e8c0-210">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4e8c0-211">d.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-211">d.</span></span> <span data-ttu-id="4e8c0-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="4e8c0-213">Criando um usuário de teste do 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="4e8c0-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="4e8c0-214">Aplicativo dá suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação serão criados no aplicativo hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-214">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4e8c0-215">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4e8c0-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4e8c0-216">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso too123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too123ContactForm.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4e8c0-218">**tooassign Britta Simon too123ContactForm, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4e8c0-218">**tooassign Britta Simon too123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e8c0-219">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4e8c0-221">Na lista de aplicativos hello, selecione **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-221">In hello applications list, select **123ContactForm**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="4e8c0-223">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4e8c0-225">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-225">Click **Add** button.</span></span> <span data-ttu-id="4e8c0-226">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4e8c0-228">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4e8c0-229">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4e8c0-230">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4e8c0-231">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4e8c0-231">Testing single sign-on</span></span>

<span data-ttu-id="4e8c0-232">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4e8c0-233">Quando você clica em bloco 123ContactForm Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour 123ContactForm aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4e8c0-233">When you click hello 123ContactForm tile in hello Access Panel, you should get automatically signed-on tooyour 123ContactForm application.</span></span>
<span data-ttu-id="4e8c0-234">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4e8c0-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4e8c0-235">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4e8c0-235">Additional resources</span></span>

* [<span data-ttu-id="4e8c0-236">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4e8c0-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4e8c0-237">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4e8c0-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

