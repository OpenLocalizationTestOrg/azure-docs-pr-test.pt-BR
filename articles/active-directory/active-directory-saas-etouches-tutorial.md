---
title: "Tutorial: integração do Azure Active Directory com o etouches | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e etouches."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="32db2-103">Tutorial: integração do Azure Active Directory com o etouches</span><span class="sxs-lookup"><span data-stu-id="32db2-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="32db2-104">Neste tutorial, você aprenderá como etouches toointegrate com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="32db2-104">In this tutorial, you learn how toointegrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32db2-105">Integrando etouches com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="32db2-105">Integrating etouches with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="32db2-106">Você pode controlar no AD do Azure que tenha acesso tooetouches</span><span class="sxs-lookup"><span data-stu-id="32db2-106">You can control in Azure AD who has access tooetouches</span></span>
- <span data-ttu-id="32db2-107">Você pode habilitar seus usuários tooautomatically get conectado tooetouches (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32db2-107">You can enable your users tooautomatically get signed-on tooetouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32db2-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="32db2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="32db2-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32db2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32db2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="32db2-110">Prerequisites</span></span>

<span data-ttu-id="32db2-111">tooconfigure integração do AD do Azure com etouches, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="32db2-111">tooconfigure Azure AD integration with etouches, you need hello following items:</span></span>

- <span data-ttu-id="32db2-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32db2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32db2-113">Uma assinatura do etouches habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="32db2-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32db2-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="32db2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32db2-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="32db2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32db2-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="32db2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32db2-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32db2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32db2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="32db2-118">Scenario description</span></span>
<span data-ttu-id="32db2-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="32db2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32db2-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="32db2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32db2-121">Adicionando etouches da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="32db2-121">Adding etouches from hello gallery</span></span>
2. <span data-ttu-id="32db2-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32db2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-hello-gallery"></a><span data-ttu-id="32db2-123">Adicionando etouches da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="32db2-123">Adding etouches from hello gallery</span></span>
<span data-ttu-id="32db2-124">integração de saudação tooconfigure de etouches no AD do Azure, você precisa etouches tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="32db2-124">tooconfigure hello integration of etouches into Azure AD, you need tooadd etouches from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="32db2-125">**etouches tooadd da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="32db2-125">**tooadd etouches from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="32db2-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="32db2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="32db2-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="32db2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="32db2-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="32db2-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="32db2-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32db2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="32db2-133">Na caixa de pesquisa hello, digite **etouches**, selecione **etouches** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="32db2-133">In hello search box, type **etouches**, select **etouches** from result panel then click **Add** button tooadd hello application.</span></span>

    ![etouches na lista de resultados de saudação](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="32db2-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="32db2-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="32db2-136">Nesta seção, você configurará e testará o logon único do Azure AD com o etouches, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="32db2-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="32db2-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em etouches é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="32db2-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in etouches is tooa user in Azure AD.</span></span> <span data-ttu-id="32db2-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em etouches precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="32db2-138">In other words, a link relationship between an Azure AD user and hello related user in etouches needs toobe established.</span></span>

<span data-ttu-id="32db2-139">Etouches, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="32db2-139">In etouches, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="32db2-140">tooconfigure e teste de logon único do AD do Azure com etouches, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="32db2-140">tooconfigure and test Azure AD single sign-on with etouches, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="32db2-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="32db2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="32db2-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32db2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32db2-143">**[Criar um usuário de teste etouches](#create-an-etouches-test-user)**  -toohave um equivalente do Britta Simon em etouches é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="32db2-143">**[Create an etouches test user](#create-an-etouches-test-user)** - toohave a counterpart of Britta Simon in etouches that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="32db2-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="32db2-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32db2-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="32db2-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="32db2-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="32db2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="32db2-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo etouches.</span><span class="sxs-lookup"><span data-stu-id="32db2-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="32db2-148">**tooconfigure AD do Azure-logon único com etouches, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="32db2-148">**tooconfigure Azure AD single sign-on with etouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="32db2-149">Em Olá portal do Azure, Olá **etouches** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="32db2-149">In hello Azure portal, on hello **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="32db2-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="32db2-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="32db2-153">Em Olá **etouches domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="32db2-153">On hello **etouches Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="32db2-155">a.</span><span class="sxs-lookup"><span data-stu-id="32db2-155">a.</span></span> <span data-ttu-id="32db2-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="32db2-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="32db2-157">b.</span><span class="sxs-lookup"><span data-stu-id="32db2-157">b.</span></span> <span data-ttu-id="32db2-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="32db2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32db2-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="32db2-159">These values are not real.</span></span> <span data-ttu-id="32db2-160">Atualizar o valor Olá com hello real entrar na URL e o identificador, que é explicada posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="32db2-160">You update hello value with hello actual Sign on URL and Identifier, which is explained later in hello tutorial.</span></span>
    > 

4. <span data-ttu-id="32db2-161">aplicativo de etouches espera asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="32db2-161">etouches application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="32db2-162">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="32db2-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="32db2-163">Você pode gerenciar os valores hello desses atributos de saudação **usuário atributo** do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="32db2-163">You can manage hello values of these attributes from hello **User Attribute** of hello application.</span></span> <span data-ttu-id="32db2-164">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="32db2-164">hello following screenshot shows an example for this.</span></span> 

    ![Atributo de Usuário](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="32db2-166">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="32db2-166">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="32db2-167">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="32db2-167">Attribute Name</span></span> | <span data-ttu-id="32db2-168">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="32db2-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="32db2-169">Email</span><span class="sxs-lookup"><span data-stu-id="32db2-169">Email</span></span> | <span data-ttu-id="32db2-170">user.mail</span><span class="sxs-lookup"><span data-stu-id="32db2-170">user.mail</span></span> |    
    
    <span data-ttu-id="32db2-171">a.</span><span class="sxs-lookup"><span data-stu-id="32db2-171">a.</span></span> <span data-ttu-id="32db2-172">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32db2-172">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Adicionar Atributo](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Caixa de diálogo Adicionar Atributo](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="32db2-175">b.</span><span class="sxs-lookup"><span data-stu-id="32db2-175">b.</span></span> <span data-ttu-id="32db2-176">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="32db2-176">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="32db2-177">c.</span><span class="sxs-lookup"><span data-stu-id="32db2-177">c.</span></span> <span data-ttu-id="32db2-178">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="32db2-178">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="32db2-179">d.</span><span class="sxs-lookup"><span data-stu-id="32db2-179">d.</span></span> <span data-ttu-id="32db2-180">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="32db2-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="32db2-181">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="32db2-181">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="32db2-183">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="32db2-183">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="32db2-185">tooget SSO configurado para o seu aplicativo executar Olá seguindo as etapas no aplicativo de etouches hello:</span><span class="sxs-lookup"><span data-stu-id="32db2-185">tooget SSO configured for your application, perform hello following steps in hello etouches application:</span></span> 

    ![configuração do etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="32db2-187">a.</span><span class="sxs-lookup"><span data-stu-id="32db2-187">a.</span></span> <span data-ttu-id="32db2-188">Logon muito**etouches** usando os direitos de administrador de saudação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32db2-188">Login too**etouches** application using hello Admin rights.</span></span>
   
    <span data-ttu-id="32db2-189">b.</span><span class="sxs-lookup"><span data-stu-id="32db2-189">b.</span></span> <span data-ttu-id="32db2-190">Vá toohello **SAML** configuração.</span><span class="sxs-lookup"><span data-stu-id="32db2-190">Go toohello **SAML** Configuration.</span></span>

    <span data-ttu-id="32db2-191">c.</span><span class="sxs-lookup"><span data-stu-id="32db2-191">c.</span></span> <span data-ttu-id="32db2-192">Em Olá **configurações gerais** seção, abra seu certificado baixado do portal do Azure no bloco de notas, Olá de cópia de conteúdo e, em seguida, cole-o na caixa de texto Olá IDP metadados.</span><span class="sxs-lookup"><span data-stu-id="32db2-192">In hello **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy hello content, and then paste it into hello IDP metadata textbox.</span></span> 

    <span data-ttu-id="32db2-193">d.</span><span class="sxs-lookup"><span data-stu-id="32db2-193">d.</span></span> <span data-ttu-id="32db2-194">Clique em Olá **Salvar & permanecer** botão.</span><span class="sxs-lookup"><span data-stu-id="32db2-194">Click on hello **Save & Stay** button.</span></span>
  
    <span data-ttu-id="32db2-195">e.</span><span class="sxs-lookup"><span data-stu-id="32db2-195">e.</span></span> <span data-ttu-id="32db2-196">Clique em Olá **metadados de atualização** botão Olá seção de metadados de SAML.</span><span class="sxs-lookup"><span data-stu-id="32db2-196">Click on hello **Update Metadata** button in hello SAML Metadata section.</span></span> 

    <span data-ttu-id="32db2-197">f.</span><span class="sxs-lookup"><span data-stu-id="32db2-197">f.</span></span> <span data-ttu-id="32db2-198">Isso abre Olá página e executar o SSO.</span><span class="sxs-lookup"><span data-stu-id="32db2-198">This opens hello page and perform SSO.</span></span> <span data-ttu-id="32db2-199">Uma vez Olá SSO está funcionando, em seguida, você pode configurar o nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="32db2-199">Once hello SSO is working then you can set up hello username.</span></span>

    <span data-ttu-id="32db2-200">g.</span><span class="sxs-lookup"><span data-stu-id="32db2-200">g.</span></span> <span data-ttu-id="32db2-201">No campo de nome de usuário de saudação, selecione Olá **emailaddress** conforme mostrado na imagem de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="32db2-201">In hello Username field, select hello **emailaddress** as shown in hello image below.</span></span> 

    <span data-ttu-id="32db2-202">h.</span><span class="sxs-lookup"><span data-stu-id="32db2-202">h.</span></span> <span data-ttu-id="32db2-203">Saudação de cópia **ID da entidade SP** valor e cole-a saudação **identificador** caixa de texto, que está em **etouches domínio e URLs** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="32db2-203">Copy hello **SP entity ID** value and paste it into hello **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="32db2-204">i.</span><span class="sxs-lookup"><span data-stu-id="32db2-204">i.</span></span> <span data-ttu-id="32db2-205">Saudação de cópia **URL SSO / ACS** valor e cole-a saudação **URL de logon** caixa de texto, que está em **etouches domínio e URLs** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="32db2-205">Copy hello **SSO URL / ACS** value and paste it into hello **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="32db2-206">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="32db2-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="32db2-207">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="32db2-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="32db2-208">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32db2-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="32db2-209">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="32db2-209">Create an Azure AD test user</span></span>
<span data-ttu-id="32db2-210">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="32db2-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="32db2-212">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="32db2-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="32db2-213">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="32db2-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32db2-215">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="32db2-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32db2-217">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="32db2-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botão Adicionar de saudação](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32db2-219">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="32db2-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32db2-221">a.</span><span class="sxs-lookup"><span data-stu-id="32db2-221">a.</span></span> <span data-ttu-id="32db2-222">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32db2-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32db2-223">b.</span><span class="sxs-lookup"><span data-stu-id="32db2-223">b.</span></span> <span data-ttu-id="32db2-224">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="32db2-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32db2-225">c.</span><span class="sxs-lookup"><span data-stu-id="32db2-225">c.</span></span> <span data-ttu-id="32db2-226">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="32db2-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="32db2-227">d.</span><span class="sxs-lookup"><span data-stu-id="32db2-227">d.</span></span> <span data-ttu-id="32db2-228">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="32db2-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="32db2-229">Criar um usuário de teste no etouches</span><span class="sxs-lookup"><span data-stu-id="32db2-229">Create an etouches test user</span></span>

<span data-ttu-id="32db2-230">Nesta seção, você criará um usuário chamado Brenda Fernandes no etouches.</span><span class="sxs-lookup"><span data-stu-id="32db2-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="32db2-231">Trabalhar com [etouches cliente equipe de suporte](https://www.etouches.com/event-software/support/customer-support/) tooadd usuários de saudação na plataforma de etouches hello.</span><span class="sxs-lookup"><span data-stu-id="32db2-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) tooadd hello users in hello etouches platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="32db2-232">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32db2-232">Assign hello Azure AD test user</span></span>

<span data-ttu-id="32db2-233">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooetouches.</span><span class="sxs-lookup"><span data-stu-id="32db2-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooetouches.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="32db2-235">**tooassign Britta Simon tooetouches, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="32db2-235">**tooassign Britta Simon tooetouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="32db2-236">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="32db2-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="32db2-238">Na lista de aplicativos hello, selecione **etouches**.</span><span class="sxs-lookup"><span data-stu-id="32db2-238">In hello applications list, select **etouches**.</span></span>

    ![Olá etouches link na lista de aplicativos Olá](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="32db2-240">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="32db2-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202] 

4. <span data-ttu-id="32db2-242">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="32db2-242">Click **Add** button.</span></span> <span data-ttu-id="32db2-243">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32db2-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="32db2-245">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="32db2-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="32db2-246">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32db2-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32db2-247">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32db2-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="32db2-248">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="32db2-248">Test single sign-on</span></span>


<span data-ttu-id="32db2-249">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="32db2-249">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="32db2-250">Quando você clica em Olá etouches bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour etouches aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32db2-250">When you click hello etouches tile in hello Access Panel, you should get automatically signed-on tooyour etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32db2-251">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="32db2-251">Additional resources</span></span>

* [<span data-ttu-id="32db2-252">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="32db2-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32db2-253">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="32db2-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

