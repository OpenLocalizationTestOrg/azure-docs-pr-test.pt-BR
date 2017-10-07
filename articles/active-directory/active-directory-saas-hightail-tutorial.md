---
title: "Tutorial: Integração do Azure Active Directory ao Hightail | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Hightail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="9d79b-103">Tutorial: Integração do Azure Active Directory ao Hightail</span><span class="sxs-lookup"><span data-stu-id="9d79b-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="9d79b-104">Neste tutorial, você aprenderá como toointegrate Hightail com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="9d79b-104">In this tutorial, you learn how toointegrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d79b-105">Integrando Hightail com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d79b-105">Integrating Hightail with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9d79b-106">Você pode controlar no AD do Azure que tenha acesso tooHightail</span><span class="sxs-lookup"><span data-stu-id="9d79b-106">You can control in Azure AD who has access tooHightail</span></span>
- <span data-ttu-id="9d79b-107">Você pode habilitar seu usuários tooautomatically get conectado tooHightail (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9d79b-107">You can enable your users tooautomatically get signed-on tooHightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9d79b-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9d79b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9d79b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d79b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d79b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9d79b-110">Prerequisites</span></span>

<span data-ttu-id="9d79b-111">tooconfigure integração do AD do Azure com Hightail, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d79b-111">tooconfigure Azure AD integration with Hightail, you need hello following items:</span></span>

- <span data-ttu-id="9d79b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9d79b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d79b-113">Uma assinatura habilitada para logon único do Hightail</span><span class="sxs-lookup"><span data-stu-id="9d79b-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d79b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9d79b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d79b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9d79b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d79b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9d79b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d79b-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d79b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d79b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9d79b-118">Scenario description</span></span>
<span data-ttu-id="9d79b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9d79b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d79b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="9d79b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d79b-121">Adicionando Hightail da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9d79b-121">Adding Hightail from hello gallery</span></span>
2. <span data-ttu-id="9d79b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9d79b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-hello-gallery"></a><span data-ttu-id="9d79b-123">Adicionando Hightail da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9d79b-123">Adding Hightail from hello gallery</span></span>
<span data-ttu-id="9d79b-124">integração de saudação tooconfigure de Hightail no AD do Azure, você precisa tooadd Hightail da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9d79b-124">tooconfigure hello integration of Hightail into Azure AD, you need tooadd Hightail from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9d79b-125">**tooadd Hightail da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9d79b-125">**tooadd Hightail from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d79b-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9d79b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9d79b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9d79b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9d79b-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9d79b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9d79b-133">Na caixa de pesquisa hello, digite **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-133">In hello search box, type **Hightail**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="9d79b-135">No painel de resultados de saudação, selecione **Hightail**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9d79b-135">In hello results panel, select **Hightail**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9d79b-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9d79b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9d79b-138">Nesta seção, você configurará e testará o logon único do Azure AD com Hightail com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="9d79b-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9d79b-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Hightail é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d79b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hightail is tooa user in Azure AD.</span></span> <span data-ttu-id="9d79b-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Hightail precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9d79b-140">In other words, a link relationship between an Azure AD user and hello related user in Hightail needs toobe established.</span></span>

<span data-ttu-id="9d79b-141">Hightail, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="9d79b-141">In Hightail, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9d79b-142">tooconfigure e teste de logon único do AD do Azure com Hightail, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d79b-142">tooconfigure and test Azure AD single sign-on with Hightail, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9d79b-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9d79b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9d79b-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d79b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d79b-145">**[Criar um usuário de teste Hightail](#creating-a-hightail-test-user)**  -toohave um equivalente do Britta Simon em Hightail é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="9d79b-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - toohave a counterpart of Britta Simon in Hightail that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d79b-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="9d79b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d79b-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="9d79b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9d79b-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d79b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9d79b-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Hightail.</span><span class="sxs-lookup"><span data-stu-id="9d79b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="9d79b-150">**tooconfigure AD do Azure-logon único com Hightail, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9d79b-150">**tooconfigure Azure AD single sign-on with Hightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d79b-151">Em Olá portal do Azure, Olá **Hightail** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-151">In hello Azure portal, on hello **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9d79b-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="9d79b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="9d79b-155">Em Olá **Hightail domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d79b-155">On hello **Hightail Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="9d79b-157">Em Olá **URL de resposta** caixa de texto, digite a URL hello como:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="9d79b-157">In hello **Reply URL** textbox, type hello URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9d79b-158">Olá valor anterior não é um valor real.</span><span class="sxs-lookup"><span data-stu-id="9d79b-158">hello preceding value is not real value.</span></span> <span data-ttu-id="9d79b-159">Você atualizará o valor de saudação com hello real URL de resposta, que é explicada posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="9d79b-159">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="9d79b-160">Em Olá **Hightail domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d79b-160">On hello **Hightail Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="9d79b-162">a.</span><span class="sxs-lookup"><span data-stu-id="9d79b-162">a.</span></span> <span data-ttu-id="9d79b-163">Clique em Olá **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-163">Click hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="9d79b-164">b.</span><span class="sxs-lookup"><span data-stu-id="9d79b-164">b.</span></span> <span data-ttu-id="9d79b-165">Em Olá **URL de logon** caixa de texto, digite a URL hello como:`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="9d79b-165">In hello **Sign On URL** textbox, type hello URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="9d79b-166">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9d79b-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="9d79b-168">Hightail aplicativo espera as asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="9d79b-168">Hightail application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="9d79b-169">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9d79b-169">Please configure hello following claims for this application.</span></span> <span data-ttu-id="9d79b-170">Você pode gerenciar os valores hello desses atributos de saudação **"Atributo"** guia do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="9d79b-170">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="9d79b-171">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="9d79b-171">hello following screenshot shows an example for this.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="9d79b-173">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d79b-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="9d79b-174">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="9d79b-174">Attribute Name</span></span> | <span data-ttu-id="9d79b-175">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="9d79b-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="9d79b-176">Nome</span><span class="sxs-lookup"><span data-stu-id="9d79b-176">FirstName</span></span> | <span data-ttu-id="9d79b-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="9d79b-177">user.givenname</span></span> |
    | <span data-ttu-id="9d79b-178">Sobrenome</span><span class="sxs-lookup"><span data-stu-id="9d79b-178">LastName</span></span> | <span data-ttu-id="9d79b-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="9d79b-179">user.surname</span></span> |
    | <span data-ttu-id="9d79b-180">Email</span><span class="sxs-lookup"><span data-stu-id="9d79b-180">Email</span></span> | <span data-ttu-id="9d79b-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="9d79b-181">user.mail</span></span> |    
    | <span data-ttu-id="9d79b-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="9d79b-182">UserIdentity</span></span> | <span data-ttu-id="9d79b-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="9d79b-183">user.mail</span></span> |
    
    <span data-ttu-id="9d79b-184">a.</span><span class="sxs-lookup"><span data-stu-id="9d79b-184">a.</span></span> <span data-ttu-id="9d79b-185">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9d79b-185">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="9d79b-188">b.</span><span class="sxs-lookup"><span data-stu-id="9d79b-188">b.</span></span> <span data-ttu-id="9d79b-189">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="9d79b-189">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="9d79b-190">c.</span><span class="sxs-lookup"><span data-stu-id="9d79b-190">c.</span></span> <span data-ttu-id="9d79b-191">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="9d79b-191">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="9d79b-192">d.</span><span class="sxs-lookup"><span data-stu-id="9d79b-192">d.</span></span> <span data-ttu-id="9d79b-193">Deixe Olá **Namespace** em branco.</span><span class="sxs-lookup"><span data-stu-id="9d79b-193">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="9d79b-194">e.</span><span class="sxs-lookup"><span data-stu-id="9d79b-194">e.</span></span> <span data-ttu-id="9d79b-195">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-195">Click **Ok**.</span></span>

7. <span data-ttu-id="9d79b-196">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9d79b-196">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9d79b-198">Em Olá **Hightail configuração** seção, clique em **configurar Hightail** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="9d79b-198">On hello **Hightail Configuration** section, click **Configure Hightail** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9d79b-199">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="9d79b-199">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="9d79b-201">Antes de configurar Olá logon único no aplicativo Hightail, lista de permissões de seu domínio de email com Hightail da equipe para que todos os usuários que estão usando esse domínio de Olá pode use funcionalidade de logon único.</span><span class="sxs-lookup"><span data-stu-id="9d79b-201">Before configuring hello Single Sign On at Hightail app, please white list your email domain with Hightail team so that all hello users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="9d79b-202">tooget SSO configurado para o seu aplicativo, você precisa em toosign tooyour Hightail locatário como um administrador.</span><span class="sxs-lookup"><span data-stu-id="9d79b-202">tooget SSO configured for your application, you need toosign-on tooyour Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="9d79b-203">a.</span><span class="sxs-lookup"><span data-stu-id="9d79b-203">a.</span></span> <span data-ttu-id="9d79b-204">No menu de saudação na parte superior do hello, clique Olá **conta** guia e selecione **configurar SAML**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-204">In hello menu on hello top, click hello **Account** tab and select **Configure SAML**.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="9d79b-206">b.</span><span class="sxs-lookup"><span data-stu-id="9d79b-206">b.</span></span> <span data-ttu-id="9d79b-207">Selecione caixa de seleção de saudação do **Ativar autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-207">Select hello checkbox of **Enable SAML Authentication**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="9d79b-209">c.</span><span class="sxs-lookup"><span data-stu-id="9d79b-209">c.</span></span> <span data-ttu-id="9d79b-210">Abra seu certificado codificado em base 64 no bloco de notas que baixou do portal do Azure, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado de assinatura de Token SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="9d79b-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **SAML Token Signing Certificate** textbox.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="9d79b-212">d.</span><span class="sxs-lookup"><span data-stu-id="9d79b-212">d.</span></span> <span data-ttu-id="9d79b-213">Em Olá **autoridade SAML (provedor de identidade)** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** copiada do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d79b-213">In hello **SAML Authority (Identity Provider)** textbox, paste hello value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="9d79b-215">e.</span><span class="sxs-lookup"><span data-stu-id="9d79b-215">e.</span></span> <span data-ttu-id="9d79b-216">Se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP** selecione **"Provedor de identidade (IdP) iniciada pelo logon"**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-216">If you wish tooconfigure hello application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="9d79b-217">Se você usar o **modo iniciado pelo SP**, selecione **"Logon iniciado pelo SP (Provedor de Serviços)"**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="9d79b-219">f.</span><span class="sxs-lookup"><span data-stu-id="9d79b-219">f.</span></span> <span data-ttu-id="9d79b-220">Copiar URL de consumidor SAML Olá para sua instância e cole-o em **URL de resposta** textbox em **Hightail domínio e URLs** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d79b-220">Copy hello SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="9d79b-221">g.</span><span class="sxs-lookup"><span data-stu-id="9d79b-221">g.</span></span> <span data-ttu-id="9d79b-222">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9d79b-223">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="9d79b-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9d79b-224">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="9d79b-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9d79b-225">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9d79b-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9d79b-226">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9d79b-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="9d79b-227">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d79b-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9d79b-229">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9d79b-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d79b-230">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9d79b-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d79b-232">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-232">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9d79b-234">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9d79b-234">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d79b-236">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d79b-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d79b-238">a.</span><span class="sxs-lookup"><span data-stu-id="9d79b-238">a.</span></span> <span data-ttu-id="9d79b-239">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d79b-240">b.</span><span class="sxs-lookup"><span data-stu-id="9d79b-240">b.</span></span> <span data-ttu-id="9d79b-241">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9d79b-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9d79b-242">c.</span><span class="sxs-lookup"><span data-stu-id="9d79b-242">c.</span></span> <span data-ttu-id="9d79b-243">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9d79b-244">d.</span><span class="sxs-lookup"><span data-stu-id="9d79b-244">d.</span></span> <span data-ttu-id="9d79b-245">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="9d79b-246">Criação de um usuário de teste do Hightail</span><span class="sxs-lookup"><span data-stu-id="9d79b-246">Creating a Hightail test user</span></span>

<span data-ttu-id="9d79b-247">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Hightail.</span><span class="sxs-lookup"><span data-stu-id="9d79b-247">hello objective of this section is toocreate a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="9d79b-248">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="9d79b-248">There is no action item for you in this section.</span></span> <span data-ttu-id="9d79b-249">Hightail dá suporte ao provisionamento de usuário just-in-time baseado em declarações personalizadas de hello.</span><span class="sxs-lookup"><span data-stu-id="9d79b-249">Hightail supports just-in-time user provisioning based on hello custom claims.</span></span> <span data-ttu-id="9d79b-250">Se você tiver configurado as declarações personalizadas Olá conforme mostrado na seção de saudação  **[Configurando o AD do Azure Single Sign-On](#configuring-azure-ad-single-sign-on)**  acima, um usuário é criado automaticamente no aplicativo hello ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="9d79b-250">If you have configured hello custom claims as shown in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in hello application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="9d79b-251">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [a equipe de suporte Hightail](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="9d79b-251">If you need toocreate a user manually, you need toocontact hello [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9d79b-252">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9d79b-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9d79b-253">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHightail.</span><span class="sxs-lookup"><span data-stu-id="9d79b-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHightail.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9d79b-255">**tooassign Britta Simon tooHightail, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9d79b-255">**tooassign Britta Simon tooHightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d79b-256">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9d79b-258">Na lista de aplicativos hello, selecione **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-258">In hello applications list, select **Hightail**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="9d79b-260">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9d79b-262">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9d79b-262">Click **Add** button.</span></span> <span data-ttu-id="9d79b-263">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9d79b-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9d79b-265">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="9d79b-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9d79b-266">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9d79b-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d79b-267">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9d79b-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9d79b-268">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9d79b-268">Testing single sign-on</span></span>

<span data-ttu-id="9d79b-269">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="9d79b-269">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9d79b-270">Quando você clica em bloco Hightail Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Hightail aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9d79b-270">When you click hello Hightail tile in hello Access Panel, you should get automatically signed-on tooyour Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9d79b-271">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9d79b-271">Additional resources</span></span>

* [<span data-ttu-id="9d79b-272">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9d79b-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d79b-273">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d79b-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

