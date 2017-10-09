---
title: "Tutorial: integração do Azure Active Directory ao CloudPassage | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e CloudPassage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 32fb007b90f071626c9b40fb5afc341dd3c1ae99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="fb7c4-103">Tutorial: integração do Active Directory do Azure ao CloudPassage</span><span class="sxs-lookup"><span data-stu-id="fb7c4-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="fb7c4-104">Neste tutorial, você aprenderá como toointegrate CloudPassage com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="fb7c4-104">In this tutorial, you learn how toointegrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb7c4-105">Integrando CloudPassage com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb7c4-105">Integrating CloudPassage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fb7c4-106">Você pode controlar no AD do Azure que tenha acesso tooCloudPassage</span><span class="sxs-lookup"><span data-stu-id="fb7c4-106">You can control in Azure AD who has access tooCloudPassage</span></span>
- <span data-ttu-id="fb7c4-107">Você pode habilitar seu usuários tooautomatically get conectado tooCloudPassage (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fb7c4-107">You can enable your users tooautomatically get signed-on tooCloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fb7c4-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fb7c4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fb7c4-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fb7c4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb7c4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fb7c4-110">Prerequisites</span></span>

<span data-ttu-id="fb7c4-111">tooconfigure integração do AD do Azure com CloudPassage, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb7c4-111">tooconfigure Azure AD integration with CloudPassage, you need hello following items:</span></span>

- <span data-ttu-id="fb7c4-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fb7c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fb7c4-113">Uma assinatura do CloudPassage com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="fb7c4-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fb7c4-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fb7c4-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="fb7c4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb7c4-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb7c4-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb7c4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb7c4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="fb7c4-118">Scenario description</span></span>
<span data-ttu-id="fb7c4-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fb7c4-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="fb7c4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fb7c4-121">Adicionando CloudPassage da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="fb7c4-121">Adding CloudPassage from hello gallery</span></span>
2. <span data-ttu-id="fb7c4-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fb7c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-hello-gallery"></a><span data-ttu-id="fb7c4-123">Adicionando CloudPassage da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="fb7c4-123">Adding CloudPassage from hello gallery</span></span>
<span data-ttu-id="fb7c4-124">integração de saudação tooconfigure de CloudPassage no AD do Azure, você precisa tooadd CloudPassage da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-124">tooconfigure hello integration of CloudPassage into Azure AD, you need tooadd CloudPassage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fb7c4-125">**tooadd CloudPassage da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fb7c4-125">**tooadd CloudPassage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb7c4-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fb7c4-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fb7c4-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="fb7c4-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="fb7c4-133">Na caixa de pesquisa hello, digite **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-133">In hello search box, type **CloudPassage**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="fb7c4-135">No painel de resultados de saudação, selecione **CloudPassage**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-135">In hello results panel, select **CloudPassage**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fb7c4-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fb7c4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fb7c4-138">Nesta seção, você configura e testa o logon único do Azure AD com o CloudPassage com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="fb7c4-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fb7c4-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em CloudPassage é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CloudPassage is tooa user in Azure AD.</span></span> <span data-ttu-id="fb7c4-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em CloudPassage precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-140">In other words, a link relationship between an Azure AD user and hello related user in CloudPassage needs toobe established.</span></span>

<span data-ttu-id="fb7c4-141">CloudPassage, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-141">In CloudPassage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fb7c4-142">tooconfigure e teste de logon único do AD do Azure com CloudPassage, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb7c4-142">tooconfigure and test Azure AD single sign-on with CloudPassage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fb7c4-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fb7c4-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fb7c4-145">**[Criar um usuário de teste CloudPassage](#creating-a-cloudpassage-test-user)**  -toohave um equivalente do Britta Simon em CloudPassage é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - toohave a counterpart of Britta Simon in CloudPassage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fb7c4-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fb7c4-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fb7c4-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb7c4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fb7c4-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="fb7c4-150">**tooconfigure AD do Azure-logon único com CloudPassage, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fb7c4-150">**tooconfigure Azure AD single sign-on with CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb7c4-151">Em Olá portal do Azure, Olá **CloudPassage** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-151">In hello Azure portal, on hello **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="fb7c4-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="fb7c4-155">Em Olá **CloudPassage domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb7c4-155">On hello **CloudPassage Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="fb7c4-157">a.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-157">a.</span></span> <span data-ttu-id="fb7c4-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="fb7c4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="fb7c4-159">b.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-159">b.</span></span> <span data-ttu-id="fb7c4-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir: `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="fb7c4-161">Você pode obter o valor para este atributo clicando **documentação de instalação de SSO** em Olá **configurações de logon único** seção do seu portal CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-161">You can get your value for this attribute by clicking **SSO Setup documentation** in hello **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="fb7c4-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-163">These values are not real.</span></span> <span data-ttu-id="fb7c4-164">Atualize esses valores com URL de resposta real hello e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="fb7c4-165">Entre em contato com [equipe de suporte do cliente CloudPassage](https://www.cloudpassage.com/company/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="fb7c4-166">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="fb7c4-168">Seu aplicativo CloudPassage espera as asserções de SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-168">Your CloudPassage application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span>   
<span data-ttu-id="fb7c4-169">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-169">hello following screenshot shows an example for this.</span></span>
   
   ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="fb7c4-171">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb7c4-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>

    | <span data-ttu-id="fb7c4-172">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="fb7c4-172">Attribute Name</span></span> | <span data-ttu-id="fb7c4-173">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="fb7c4-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="fb7c4-174">nome</span><span class="sxs-lookup"><span data-stu-id="fb7c4-174">firstname</span></span> |<span data-ttu-id="fb7c4-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="fb7c4-175">user.givenname</span></span> |
    | <span data-ttu-id="fb7c4-176">sobrenome</span><span class="sxs-lookup"><span data-stu-id="fb7c4-176">lastname</span></span> |<span data-ttu-id="fb7c4-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="fb7c4-177">user.surname</span></span> |
    | <span data-ttu-id="fb7c4-178">email</span><span class="sxs-lookup"><span data-stu-id="fb7c4-178">email</span></span> |<span data-ttu-id="fb7c4-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="fb7c4-179">user.mail</span></span> |
    
    <span data-ttu-id="fb7c4-180">a.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-180">a.</span></span> <span data-ttu-id="fb7c4-181">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="fb7c4-184">b.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-184">b.</span></span> <span data-ttu-id="fb7c4-185">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="fb7c4-186">c.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-186">c.</span></span> <span data-ttu-id="fb7c4-187">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="fb7c4-188">d.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-188">d.</span></span> <span data-ttu-id="fb7c4-189">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-189">Click **Ok**.</span></span>

7. <span data-ttu-id="fb7c4-190">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="fb7c4-190">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="fb7c4-192">Em Olá **CloudPassage configuração** seção, clique em **configurar CloudPassage** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-192">On hello **CloudPassage Configuration** section, click **Configure CloudPassage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fb7c4-193">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="fb7c4-193">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="fb7c4-195">Em uma janela de navegador diferente, site da empresa CloudPassage tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-195">In a different browser window, sign-on tooyour CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="fb7c4-196">No menu de saudação na parte superior de saudação, clique em **configurações**e, em seguida, clique em **administração de Site**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-196">In hello menu on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Configurar Logon Único][12]

11. <span data-ttu-id="fb7c4-198">Clique em Olá **configurações de autenticação** guia.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-198">Click hello **Authentication Settings** tab.</span></span> 
   
    ![Configurar Logon Único][13]

12. <span data-ttu-id="fb7c4-200">Em Olá **configurações de logon único** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb7c4-200">In hello **Single Sign-on Settings** section, perform hello following steps:</span></span> 
   
    ![Configurar Logon Único][14]

    <span data-ttu-id="fb7c4-202">a.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-202">a.</span></span> <span data-ttu-id="fb7c4-203">Marque a caixa de seleção **Habilitar SSO (Logon Único) (Documentação de instalação de SSO)**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="fb7c4-204">b.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-204">b.</span></span> <span data-ttu-id="fb7c4-205">Colar **ID da entidade SAML** em Olá **URL do emissor SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-205">Paste **SAML Entity ID** into hello **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="fb7c4-206">c.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-206">c.</span></span> <span data-ttu-id="fb7c4-207">Colar **Single Sign-On URL do serviço SAML** em Olá **URL do ponto de extremidade do SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-207">Paste **SAML Single Sign-On Service URL** into hello **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="fb7c4-208">d.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-208">d.</span></span> <span data-ttu-id="fb7c4-209">Colar **URL de logout** em Olá **página de aterrissagem do Logout** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-209">Paste **Sign-Out URL** into hello **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="fb7c4-210">e.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-210">e.</span></span> <span data-ttu-id="fb7c4-211">Abra seu certificado baixado no bloco de notas, Olá de copiar conteúdo de certificado baixado em sua área de transferência e, em seguida, cole-o em Olá **certificado X509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-211">Open your downloaded certificate in notepad, copy hello content of downloaded certificate into your clipboard, and then paste it into hello **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="fb7c4-212">f.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-212">f.</span></span> <span data-ttu-id="fb7c4-213">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="fb7c4-214">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="fb7c4-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fb7c4-215">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fb7c4-216">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fb7c4-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fb7c4-217">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fb7c4-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="fb7c4-218">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="fb7c4-220">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fb7c4-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb7c4-221">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fb7c4-223">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fb7c4-225">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fb7c4-227">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb7c4-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fb7c4-229">a.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-229">a.</span></span> <span data-ttu-id="fb7c4-230">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb7c4-231">b.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-231">b.</span></span> <span data-ttu-id="fb7c4-232">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fb7c4-233">c.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-233">c.</span></span> <span data-ttu-id="fb7c4-234">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fb7c4-235">d.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-235">d.</span></span> <span data-ttu-id="fb7c4-236">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="fb7c4-237">Criar um usuário de teste CloudPassage</span><span class="sxs-lookup"><span data-stu-id="fb7c4-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="fb7c4-238">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-238">hello objective of this section is toocreate a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="fb7c4-239">**toocreate um usuário chamado Britta Simon no CloudPassage, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fb7c4-239">**toocreate a user called Britta Simon in CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb7c4-240">Logon tooyour **CloudPassage** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-240">Sign-on tooyour **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="fb7c4-241">Na barra de ferramentas de saudação na parte superior do hello, clique em **configurações**e, em seguida, clique em **administração de Site**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-241">In hello toolbar on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Criar um usuário de teste CloudPassage][22] 

3. <span data-ttu-id="fb7c4-243">Clique em Olá **usuários** guia e, em seguida, clique em **adicionar novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-243">Click hello **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Criar um usuário de teste CloudPassage][23]

4. <span data-ttu-id="fb7c4-245">Em Olá **adicionar novo usuário** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb7c4-245">In hello **Add New User** section, perform hello following steps:</span></span> 
   
   ![Criar um usuário de teste CloudPassage][24]
    
    <span data-ttu-id="fb7c4-247">a.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-247">a.</span></span> <span data-ttu-id="fb7c4-248">Em Olá **nome** caixa de texto, digite Britta.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-248">In hello **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="fb7c4-249">b.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-249">b.</span></span> <span data-ttu-id="fb7c4-250">Em Olá **Sobrenome** caixa de texto, digite Simon.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-250">In hello **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="fb7c4-251">c.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-251">c.</span></span> <span data-ttu-id="fb7c4-252">Em Olá **Username** caixa de texto, Olá **Email** caixa de texto e hello **Email novamente** caixa de texto, digite o nome de usuário de Britta no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-252">In hello **Username** textbox, hello **Email** textbox and hello **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="fb7c4-253">d.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-253">d.</span></span> <span data-ttu-id="fb7c4-254">Como **Tipo de acesso**, selecione **Habilitar acesso do Portal de Halo**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="fb7c4-255">e.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-255">e.</span></span> <span data-ttu-id="fb7c4-256">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fb7c4-257">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fb7c4-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fb7c4-258">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCloudPassage.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloudPassage.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="fb7c4-260">**tooassign Britta Simon tooCloudPassage, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fb7c4-260">**tooassign Britta Simon tooCloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb7c4-261">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="fb7c4-263">Na lista de aplicativos hello, selecione **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-263">In hello applications list, select **CloudPassage**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="fb7c4-265">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="fb7c4-267">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-267">Click **Add** button.</span></span> <span data-ttu-id="fb7c4-268">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="fb7c4-270">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fb7c4-271">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fb7c4-272">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fb7c4-273">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="fb7c4-273">Testing single sign-on</span></span>

<span data-ttu-id="fb7c4-274">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-274">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="fb7c4-275">Quando você clica em bloco CloudPassage Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour CloudPassage aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fb7c4-275">When you click hello CloudPassage tile in hello Access Panel, you should get automatically signed-on tooyour CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fb7c4-276">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="fb7c4-276">Additional resources</span></span>

* [<span data-ttu-id="fb7c4-277">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="fb7c4-277">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb7c4-278">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fb7c4-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

