---
title: "Tutorial: Integração do Azure Active Directory ao Clever | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Clever."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 24430e1e6c750efa5787561aa151201b1fe7d428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="07cb5-103">Tutorial: integração do Active Directory do Azure ao Clever</span><span class="sxs-lookup"><span data-stu-id="07cb5-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="07cb5-104">Neste tutorial, você aprenderá como toointegrate Clever com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="07cb5-104">In this tutorial, you learn how toointegrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07cb5-105">Integrando Clever com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="07cb5-105">Integrating Clever with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="07cb5-106">Você pode controlar no AD do Azure que tenha acesso tooClever.</span><span class="sxs-lookup"><span data-stu-id="07cb5-106">You can control in Azure AD who has access tooClever.</span></span>
- <span data-ttu-id="07cb5-107">Você pode habilitar seu usuários tooautomatically get conectado tooClever (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="07cb5-107">You can enable your users tooautomatically get signed-on tooClever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="07cb5-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="07cb5-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="07cb5-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07cb5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07cb5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="07cb5-110">Prerequisites</span></span>

<span data-ttu-id="07cb5-111">tooconfigure integração do AD do Azure com Clever, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="07cb5-111">tooconfigure Azure AD integration with Clever, you need hello following items:</span></span>

- <span data-ttu-id="07cb5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07cb5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07cb5-113">Uma assinatura do Clever habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="07cb5-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="07cb5-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="07cb5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07cb5-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="07cb5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07cb5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="07cb5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07cb5-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07cb5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07cb5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="07cb5-118">Scenario description</span></span>
<span data-ttu-id="07cb5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="07cb5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07cb5-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="07cb5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07cb5-121">Adicionando Clever da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="07cb5-121">Adding Clever from hello gallery</span></span>
2. <span data-ttu-id="07cb5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07cb5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-hello-gallery"></a><span data-ttu-id="07cb5-123">Adicionando Clever da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="07cb5-123">Adding Clever from hello gallery</span></span>
<span data-ttu-id="07cb5-124">integração de saudação tooconfigure de Clever no AD do Azure, você precisa tooadd Clever da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="07cb5-124">tooconfigure hello integration of Clever into Azure AD, you need tooadd Clever from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="07cb5-125">**tooadd Clever da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="07cb5-125">**tooadd Clever from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="07cb5-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="07cb5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="07cb5-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="07cb5-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="07cb5-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07cb5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="07cb5-133">Na caixa de pesquisa hello, digite **Clever**, selecione **Clever** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="07cb5-133">In hello search box, type **Clever**, select **Clever** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Inteligente na lista de resultados de saudação](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="07cb5-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="07cb5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="07cb5-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Clever, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="07cb5-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="07cb5-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Clever é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="07cb5-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clever is tooa user in Azure AD.</span></span> <span data-ttu-id="07cb5-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Clever precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="07cb5-138">In other words, a link relationship between an Azure AD user and hello related user in Clever needs toobe established.</span></span>

<span data-ttu-id="07cb5-139">Clever, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="07cb5-139">In Clever, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="07cb5-140">tooconfigure e teste de logon único do AD do Azure com Clever, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="07cb5-140">tooconfigure and test Azure AD single sign-on with Clever, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="07cb5-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="07cb5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="07cb5-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07cb5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07cb5-143">**[Criar um usuário de teste inteligente](#create-a-clever-test-user)**  -toohave um equivalente do Britta Simon em Clever é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="07cb5-143">**[Create a Clever test user](#create-a-clever-test-user)** - toohave a counterpart of Britta Simon in Clever that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="07cb5-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="07cb5-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07cb5-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="07cb5-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="07cb5-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="07cb5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="07cb5-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo inteligente.</span><span class="sxs-lookup"><span data-stu-id="07cb5-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="07cb5-148">**tooconfigure AD do Azure-logon único com Clever, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="07cb5-148">**tooconfigure Azure AD single sign-on with Clever, perform hello following steps:**</span></span>

1. <span data-ttu-id="07cb5-149">Em Olá portal do Azure, Olá **Clever** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-149">In hello Azure portal, on hello **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="07cb5-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="07cb5-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="07cb5-153">Em Olá **domínio inteligente e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="07cb5-153">On hello **Clever Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="07cb5-155">a.</span><span class="sxs-lookup"><span data-stu-id="07cb5-155">a.</span></span> <span data-ttu-id="07cb5-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="07cb5-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="07cb5-157">b.</span><span class="sxs-lookup"><span data-stu-id="07cb5-157">b.</span></span> <span data-ttu-id="07cb5-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="07cb5-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="07cb5-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="07cb5-159">These values are not real.</span></span> <span data-ttu-id="07cb5-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="07cb5-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="07cb5-161">Entre em contato com [equipe de suporte de cliente inteligente](https://clever.com/about/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="07cb5-161">Contact [Clever Client support team](https://clever.com/about/contact/) tooget these values.</span></span>

4. <span data-ttu-id="07cb5-162">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="07cb5-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="07cb5-164">Olá aplicativo inteligente espera asserções SAML de saudação em um formato específico, o que exige que você tooyour de mapeamentos de atributo personalizado tooadd **atributos de tokens SAML** configuração.</span><span class="sxs-lookup"><span data-stu-id="07cb5-164">hello Clever application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="07cb5-165">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="07cb5-165">hello following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="07cb5-167">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="07cb5-167">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="07cb5-168">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="07cb5-168">Attribute Name</span></span>  | <span data-ttu-id="07cb5-169">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="07cb5-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="07cb5-170">clever.student.credentials.district\_nome de usuário</span><span class="sxs-lookup"><span data-stu-id="07cb5-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="07cb5-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="07cb5-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="07cb5-172">Firstname</span><span class="sxs-lookup"><span data-stu-id="07cb5-172">Firstname</span></span>  | <span data-ttu-id="07cb5-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="07cb5-173">user.givenname</span></span> |
    | <span data-ttu-id="07cb5-174">Sobrenome</span><span class="sxs-lookup"><span data-stu-id="07cb5-174">Lastname</span></span>  | <span data-ttu-id="07cb5-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="07cb5-175">user.surname</span></span> |    

    <span data-ttu-id="07cb5-176">a.</span><span class="sxs-lookup"><span data-stu-id="07cb5-176">a.</span></span> <span data-ttu-id="07cb5-177">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07cb5-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="07cb5-180">b.</span><span class="sxs-lookup"><span data-stu-id="07cb5-180">b.</span></span> <span data-ttu-id="07cb5-181">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="07cb5-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="07cb5-182">c.</span><span class="sxs-lookup"><span data-stu-id="07cb5-182">c.</span></span> <span data-ttu-id="07cb5-183">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="07cb5-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="07cb5-184">d.</span><span class="sxs-lookup"><span data-stu-id="07cb5-184">d.</span></span> <span data-ttu-id="07cb5-185">Deixe Olá **Namespace** caixa de texto em branco.</span><span class="sxs-lookup"><span data-stu-id="07cb5-185">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="07cb5-186">d.</span><span class="sxs-lookup"><span data-stu-id="07cb5-186">d.</span></span> <span data-ttu-id="07cb5-187">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="07cb5-188">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="07cb5-188">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="07cb5-190">Olá toogenerate **metadados** url, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="07cb5-190">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="07cb5-191">a.</span><span class="sxs-lookup"><span data-stu-id="07cb5-191">a.</span></span> <span data-ttu-id="07cb5-192">Clique em **Registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-192">Click **App registrations**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="07cb5-194">b.</span><span class="sxs-lookup"><span data-stu-id="07cb5-194">b.</span></span> <span data-ttu-id="07cb5-195">Clique em **pontos de extremidade** tooopen **pontos de extremidade** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07cb5-195">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="07cb5-197">c.</span><span class="sxs-lookup"><span data-stu-id="07cb5-197">c.</span></span> <span data-ttu-id="07cb5-198">Clique em Olá cópia botão toocopy **documento de METADADOS de Federação** url e cole-o no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="07cb5-198">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="07cb5-200">d.</span><span class="sxs-lookup"><span data-stu-id="07cb5-200">d.</span></span> <span data-ttu-id="07cb5-201">Agora vá toohello a página de propriedades de **Clever** e cópia hello **Id do aplicativo** usando **cópia** botão e cole-o no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="07cb5-201">Now go toohello property page of **Clever** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="07cb5-203">e.</span><span class="sxs-lookup"><span data-stu-id="07cb5-203">e.</span></span> <span data-ttu-id="07cb5-204">Gerar Olá **URL de metadados** usando saudação padrão a seguir:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="07cb5-204">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="07cb5-205">Em uma janela de navegador web diferente, faça logon no site da empresa inteligentes de tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="07cb5-205">In a different web browser window, log in tooyour Clever company site as an administrator.</span></span>

10. <span data-ttu-id="07cb5-206">Na barra de ferramentas hello, clique em **logon instantâneo**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-206">In hello toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="07cb5-207">![Logon Instantâneo](./media/active-directory-saas-clever-tutorial/ic798984.png "Logon Instantâneo")</span><span class="sxs-lookup"><span data-stu-id="07cb5-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="07cb5-208">Em Olá **logon instantâneo** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="07cb5-208">On hello **Instant Login** page, perform hello following steps:</span></span>
      
      <span data-ttu-id="07cb5-209">![Logon Instantâneo](./media/active-directory-saas-clever-tutorial/ic798985.png "Logon Instantâneo")</span><span class="sxs-lookup"><span data-stu-id="07cb5-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="07cb5-210">a.</span><span class="sxs-lookup"><span data-stu-id="07cb5-210">a.</span></span> <span data-ttu-id="07cb5-211">Saudação de tipo **URL de logon**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-211">Type hello **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="07cb5-212">Olá **URL de logon** é um valor personalizado.</span><span class="sxs-lookup"><span data-stu-id="07cb5-212">hello **Login URL** is a custom value.</span></span> <span data-ttu-id="07cb5-213">Entre em contato com [equipe de suporte de cliente inteligente](https://clever.com/about/contact/) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="07cb5-213">Contact [Clever Client support team](https://clever.com/about/contact/) tooget this value.</span></span>
      
      <span data-ttu-id="07cb5-214">b.</span><span class="sxs-lookup"><span data-stu-id="07cb5-214">b.</span></span> <span data-ttu-id="07cb5-215">Para **Sistema de Identidade**, selecione **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="07cb5-216">c.</span><span class="sxs-lookup"><span data-stu-id="07cb5-216">c.</span></span> <span data-ttu-id="07cb5-217">Saudação de tipo **URL de metadados** em Olá **URL de metadados** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="07cb5-217">Type hello **Metadata URL** in hello **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="07cb5-218">d.</span><span class="sxs-lookup"><span data-stu-id="07cb5-218">d.</span></span> <span data-ttu-id="07cb5-219">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="07cb5-220">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="07cb5-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="07cb5-221">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="07cb5-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="07cb5-222">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="07cb5-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="07cb5-223">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="07cb5-223">Create an Azure AD test user</span></span>

<span data-ttu-id="07cb5-224">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="07cb5-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="07cb5-226">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="07cb5-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="07cb5-227">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="07cb5-227">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="07cb5-229">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-229">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="07cb5-231">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07cb5-231">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="07cb5-233">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="07cb5-233">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="07cb5-235">a.</span><span class="sxs-lookup"><span data-stu-id="07cb5-235">a.</span></span> <span data-ttu-id="07cb5-236">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-236">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07cb5-237">b.</span><span class="sxs-lookup"><span data-stu-id="07cb5-237">b.</span></span> <span data-ttu-id="07cb5-238">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07cb5-238">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="07cb5-239">c.</span><span class="sxs-lookup"><span data-stu-id="07cb5-239">c.</span></span> <span data-ttu-id="07cb5-240">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="07cb5-240">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="07cb5-241">d.</span><span class="sxs-lookup"><span data-stu-id="07cb5-241">d.</span></span> <span data-ttu-id="07cb5-242">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="07cb5-243">Criar um usuário de teste do Clever</span><span class="sxs-lookup"><span data-stu-id="07cb5-243">Create a Clever test user</span></span>

<span data-ttu-id="07cb5-244">tooenable AD do Azure usuários toolog em tooClever, eles devem ser provisionados no Clever.</span><span class="sxs-lookup"><span data-stu-id="07cb5-244">tooenable Azure AD users toolog in tooClever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="07cb5-245">No caso de Clever, trabalhar com [equipe de suporte de cliente inteligente](https://clever.com/about/contact/) para adicionar usuários de saudação na plataforma inteligente hello.</span><span class="sxs-lookup"><span data-stu-id="07cb5-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add hello users in hello Clever platform.</span></span> <span data-ttu-id="07cb5-246">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="07cb5-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="07cb5-247">Você pode usar qualquer outra ferramenta de criação do usuário inteligente conta ou APIs fornecidas pelo tooprovision inteligente contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="07cb5-247">You can use any other Clever user account creation tools or APIs provided by Clever tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="07cb5-248">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="07cb5-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="07cb5-249">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooClever.</span><span class="sxs-lookup"><span data-stu-id="07cb5-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClever.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="07cb5-251">**tooassign Britta Simon tooClever, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="07cb5-251">**tooassign Britta Simon tooClever, perform hello following steps:**</span></span>

1. <span data-ttu-id="07cb5-252">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="07cb5-254">Na lista de aplicativos hello, selecione **Clever**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-254">In hello applications list, select **Clever**.</span></span>

    ![Olá Clever link na lista de aplicativos Olá](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="07cb5-256">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="07cb5-258">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="07cb5-258">Click **Add** button.</span></span> <span data-ttu-id="07cb5-259">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07cb5-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="07cb5-261">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="07cb5-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="07cb5-262">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07cb5-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07cb5-263">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="07cb5-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="07cb5-264">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="07cb5-264">Test single sign-on</span></span>

<span data-ttu-id="07cb5-265">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="07cb5-265">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="07cb5-266">Quando você clica em bloco inteligente Olá no Olá painel de acesso, você deve obter um aplicativo inteligente automaticamente assinado em tooyour.</span><span class="sxs-lookup"><span data-stu-id="07cb5-266">When you click hello Clever tile in hello Access Panel, you should get automatically signed-on tooyour Clever application.</span></span>
<span data-ttu-id="07cb5-267">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="07cb5-267">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="07cb5-268">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="07cb5-268">Additional resources</span></span>

* [<span data-ttu-id="07cb5-269">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="07cb5-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07cb5-270">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="07cb5-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

