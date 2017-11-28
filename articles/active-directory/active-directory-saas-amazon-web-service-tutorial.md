---
title: "Tutorial: Integração do Azure Active Directory com o AWS (Amazon Web Services) | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e serviços AWS (Amazon Web)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="9f6ed-103">Tutorial: Integração do Azure Active Directory com o AWS (Amazon Web Services)</span><span class="sxs-lookup"><span data-stu-id="9f6ed-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="9f6ed-104">Neste tutorial, você aprenderá como toointegrate AWS Amazon Web Services () com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="9f6ed-104">In this tutorial, you learn how toointegrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f6ed-105">Integrando serviços AWS (Amazon Web) com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9f6ed-106">Você pode controlar no AD do Azure que tenha acesso tooAmazon AWS (Web Services)</span><span class="sxs-lookup"><span data-stu-id="9f6ed-106">You can control in Azure AD who has access tooAmazon Web Services (AWS)</span></span>
- <span data-ttu-id="9f6ed-107">Você pode habilitar seu usuários tooautomatically get conectado tooAmazon AWS (Web Services) (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6ed-107">You can enable your users tooautomatically get signed-on tooAmazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f6ed-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6ed-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9f6ed-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f6ed-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="9f6ed-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9f6ed-110">Prerequisites</span></span>

<span data-ttu-id="9f6ed-111">tooconfigure integração do Azure AD com serviços AWS (Amazon Web), você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-111">tooconfigure Azure AD integration with Amazon Web Services (AWS), you need hello following items:</span></span>

- <span data-ttu-id="9f6ed-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6ed-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f6ed-113">Uma assinatura habilitada para logon único do AWS (Amazon Web Services)</span><span class="sxs-lookup"><span data-stu-id="9f6ed-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9f6ed-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9f6ed-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f6ed-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9f6ed-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f6ed-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f6ed-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9f6ed-118">Scenario description</span></span>
<span data-ttu-id="9f6ed-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f6ed-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f6ed-121">Adicionando serviços AWS (Amazon Web) da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9f6ed-121">Adding Amazon Web Services (AWS) from hello gallery</span></span>
2. <span data-ttu-id="9f6ed-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6ed-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a><span data-ttu-id="9f6ed-123">Adicionando serviços AWS (Amazon Web) da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9f6ed-123">Adding Amazon Web Services (AWS) from hello gallery</span></span>
<span data-ttu-id="9f6ed-124">tooconfigure Olá a integração de serviços AWS (Amazon Web) no AD do Azure, você precisa tooadd serviços AWS (Amazon Web) da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-124">tooconfigure hello integration of Amazon Web Services (AWS) into Azure AD, you need tooadd Amazon Web Services (AWS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9f6ed-125">**tooadd serviços AWS (Amazon Web) da Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f6ed-125">**tooadd Amazon Web Services (AWS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f6ed-126">Em Olá  **[Portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9f6ed-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9f6ed-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9f6ed-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9f6ed-133">Na caixa de pesquisa hello, digite **serviços AWS (Amazon Web)**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-133">In hello search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="9f6ed-135">No painel de resultados de saudação, selecione **serviços AWS (Amazon Web)**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-135">In hello results panel, select **Amazon Web Services (AWS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f6ed-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6ed-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9f6ed-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o AWS (Amazon Web Services), com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="9f6ed-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9f6ed-139">Para toowork de logon único, o AD do Azure precisa tooknow que o usuário de contraparte Olá em serviços AWS (Amazon Web) é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Amazon Web Services (AWS) is tooa user in Azure AD.</span></span> <span data-ttu-id="9f6ed-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em serviços AWS (Amazon Web) precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-140">In other words, a link relationship between an Azure AD user and hello related user in Amazon Web Services (AWS) needs toobe established.</span></span>

<span data-ttu-id="9f6ed-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em serviços AWS (Amazon Web).</span><span class="sxs-lookup"><span data-stu-id="9f6ed-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="9f6ed-142">tooconfigure e teste de logon único do AD do Azure com serviços AWS (Amazon Web), você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-142">tooconfigure and test Azure AD single sign-on with Amazon Web Services (AWS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9f6ed-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9f6ed-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f6ed-145">**[Criar um usuário de teste do Amazon Web Services](#creating-an-amazon-web-services-test-user)**  -toohave um equivalente de Britta Simon em serviços AWS (Amazon Web) que é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - toohave a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9f6ed-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f6ed-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f6ed-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f6ed-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9f6ed-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de serviços AWS (Amazon Web).</span><span class="sxs-lookup"><span data-stu-id="9f6ed-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="9f6ed-150">**tooconfigure logon único do AD do Azure com serviços AWS (Amazon Web), execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f6ed-150">**tooconfigure Azure AD single sign-on with Amazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="9f6ed-151">Em Olá Portal do Azure, em Olá **serviços AWS (Amazon Web)** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-151">In hello Azure Portal, on hello **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9f6ed-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="9f6ed-155">Em Olá **serviços AWS (Amazon Web) URLs e domínio** seção, hello usuário não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-155">On hello **Amazon Web Services (AWS) Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="9f6ed-157">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="9f6ed-159">Olá aplicativo AWS Amazon Web Services () espera as asserções de SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-159">hello Amazon Web Services (AWS) Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="9f6ed-160">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-160">Please configure hello following claims for this application.</span></span> <span data-ttu-id="9f6ed-161">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-161">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="9f6ed-162">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-162">hello following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="9f6ed-164">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-164">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="9f6ed-165">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="9f6ed-165">Attribute Name</span></span>  | <span data-ttu-id="9f6ed-166">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="9f6ed-166">Attribute Value</span></span> | <span data-ttu-id="9f6ed-167">Namespace</span><span class="sxs-lookup"><span data-stu-id="9f6ed-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="9f6ed-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="9f6ed-168">RoleSessionName</span></span> | <span data-ttu-id="9f6ed-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="9f6ed-169">user.userprincipalname</span></span> | <span data-ttu-id="9f6ed-170">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="9f6ed-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="9f6ed-171">Função</span><span class="sxs-lookup"><span data-stu-id="9f6ed-171">Role</span></span>            | <span data-ttu-id="9f6ed-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="9f6ed-172">user.assignedroles</span></span> |  <span data-ttu-id="9f6ed-173">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="9f6ed-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="9f6ed-174">É necessário tooconfigure Olá provisionamento de usuário em AD do Azure toofetch todas as funções de saudação do Console do AWS.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-174">You need tooconfigure hello user provisioning in Azure AD toofetch all hello roles from AWS Console.</span></span> <span data-ttu-id="9f6ed-175">Consulte Olá provisionamento etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-175">Please refer hello provisioning steps below.</span></span>

    <span data-ttu-id="9f6ed-176">a.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-176">a.</span></span> <span data-ttu-id="9f6ed-177">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="9f6ed-179">b.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-179">b.</span></span> <span data-ttu-id="9f6ed-180">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="9f6ed-182">c.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-182">c.</span></span> <span data-ttu-id="9f6ed-183">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-183">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="9f6ed-184">Adicione o valor de Namespace de saudação conforme fornecido acima.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-184">Add hello Namespace value as given above.</span></span>
    
    <span data-ttu-id="9f6ed-185">d.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-185">d.</span></span> <span data-ttu-id="9f6ed-186">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-186">Click **Ok**.</span></span>

7. <span data-ttu-id="9f6ed-187">Clique em **salvar** botão Configurações de saudação toosave no Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-187">Click **Save** button toosave hello settings on Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9f6ed-189">Em uma janela de navegador diferente, site da empresa serviços AWS (Amazon Web) tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-189">In a different browser window, sign-on tooyour Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="9f6ed-190">Clique em **página inicial do Console**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-190">Click **Console Home**.</span></span>
   
    ![Configurar Logon Único][11]

10. <span data-ttu-id="9f6ed-192">Clique em **IAM** no serviço **Segurança, Identidade e Conformidade**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Configurar Logon Único][12]

11. <span data-ttu-id="9f6ed-194">Clique em **Provedores de identidade**, e, em seguida, clique em **Criar provedor**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Configurar Logon Único][13]

12. <span data-ttu-id="9f6ed-196">Em Olá **Configurar provedor** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-196">On hello **Configure Provider** dialog page, perform hello following steps:</span></span>
   
    ![Configurar Logon Único][14]
 
    <span data-ttu-id="9f6ed-198">a.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-198">a.</span></span> <span data-ttu-id="9f6ed-199">Como **Tipo de provedor**, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="9f6ed-200">b.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-200">b.</span></span> <span data-ttu-id="9f6ed-201">Em Olá **nome do provedor** caixa de texto, digite um nome de provedor (por exemplo: *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="9f6ed-201">In hello **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="9f6ed-202">c.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-202">c.</span></span> <span data-ttu-id="9f6ed-203">tooupload seu arquivo de metadados baixado, clique em **Escolher arquivo**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-203">tooupload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="9f6ed-204">d.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-204">d.</span></span> <span data-ttu-id="9f6ed-205">Clique em **Próxima etapa**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="9f6ed-206">Em Olá **verificar informações do provedor** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-206">On hello **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Configurar Logon Único][15]

14. <span data-ttu-id="9f6ed-208">Clique em **Funções** e, em seguida, clique em **Criar Nova Função**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Configurar Logon Único][16]

15. <span data-ttu-id="9f6ed-210">Em Olá **definir nome de função** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-210">On hello **Set Role Name** dialog, perform hello following steps:</span></span> 
    
    ![Configurar Logon Único][17] 

    <span data-ttu-id="9f6ed-212">a.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-212">a.</span></span> <span data-ttu-id="9f6ed-213">Em Olá **nome da função** caixa de texto, digite um nome de função (por exemplo: *TestUser*).</span><span class="sxs-lookup"><span data-stu-id="9f6ed-213">In hello **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="9f6ed-214">b.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-214">b.</span></span> <span data-ttu-id="9f6ed-215">Clique em **Próxima etapa**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="9f6ed-216">Em Olá **Selecionar tipo de função** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-216">On hello **Select Role Type** dialog, perform hello following steps:</span></span> 
    
    ![Configurar Logon Único][18] 

    <span data-ttu-id="9f6ed-218">a.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-218">a.</span></span> <span data-ttu-id="9f6ed-219">Selecione **Função de acesso do provedor de identidade**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="9f6ed-220">b.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-220">b.</span></span> <span data-ttu-id="9f6ed-221">Em Olá **Grant Web Single Sign-On (WebSSO) tooSAML provedores de acesso a** seção, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-221">In hello **Grant Web Single Sign-On (WebSSO) access tooSAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="9f6ed-222">Em Olá **estabelecer confiança** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-222">On hello **Establish Trust** dialog, perform hello following steps:</span></span>  
    
    ![Configurar Logon Único][19] 

    <span data-ttu-id="9f6ed-224">a.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-224">a.</span></span> <span data-ttu-id="9f6ed-225">Como provedor SAML, selecione o provedor SAML de saudação você criou anteriormente (por exemplo: *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="9f6ed-225">As SAML provider, select hello SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="9f6ed-226">b.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-226">b.</span></span> <span data-ttu-id="9f6ed-227">Clique em **Próxima etapa**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="9f6ed-228">Em Olá **verificar função confiança** caixa de diálogo, clique em **próxima etapa**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-228">On hello **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Configurar Logon Único][32]

19. <span data-ttu-id="9f6ed-230">Em Olá **anexar política** caixa de diálogo, clique em **próxima etapa**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-230">On hello **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Configurar Logon Único][33]

20. <span data-ttu-id="9f6ed-232">Em Olá **revisão** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-232">On hello **Review** dialog, perform hello following steps:</span></span>
    
    ![Configurar Logon Único][34]
 
    <span data-ttu-id="9f6ed-234">a.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-234">a.</span></span> <span data-ttu-id="9f6ed-235">Clique em **Criar função**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-235">Click **Create Role**.</span></span>

    <span data-ttu-id="9f6ed-236">b.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-236">b.</span></span> <span data-ttu-id="9f6ed-237">Criar funções necessárias e mapeá-los toohello provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-237">Create as many roles as needed and map them toohello Identity Provider.</span></span>

21. <span data-ttu-id="9f6ed-238">Configurar usuário Olá provisionamento toofetch todas as funções de saudação do AWS</span><span class="sxs-lookup"><span data-stu-id="9f6ed-238">Now configure hello user provisioning toofetch all hello roles from AWS</span></span>

    <span data-ttu-id="9f6ed-239">a.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-239">a.</span></span> <span data-ttu-id="9f6ed-240">No logon do Console do AWS Olá com sua conta raiz</span><span class="sxs-lookup"><span data-stu-id="9f6ed-240">In hello AWS Console login with your root account</span></span>

    <span data-ttu-id="9f6ed-241">b.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-241">b.</span></span> <span data-ttu-id="9f6ed-242">No canto direito superior de saudação clique em seu nome e clique em Olá **minhas credenciais de segurança** opção.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-242">In hello top right corner click your name and then click hello **My Security Credentials** option.</span></span> <span data-ttu-id="9f6ed-243">Isso abrirá uma tela como uma mensagem de aviso.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="9f6ed-244">Botão Olá **as credenciais de segurança** toopass botão Olá tela.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-244">Click hello button **Security Credentials** button toopass hello screen.</span></span>
        
       ![Configurar Logon Único][36]

       ![Configurar Logon Único][37]

    <span data-ttu-id="9f6ed-247">c.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-247">c.</span></span> <span data-ttu-id="9f6ed-248">Em Olá chaves de acesso clique Olá **criar nova chave de acesso** botão.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-248">In hello Access Keys section click hello **Create New Access Key** button.</span></span> <span data-ttu-id="9f6ed-249">Isso gera hello ID da chave de acesso e um valor de token.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-249">This generates hello Access Key ID and a token value.</span></span>
    
       ![Configurar Logon Único][38]

    <span data-ttu-id="9f6ed-251">d.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-251">d.</span></span> <span data-ttu-id="9f6ed-252">Copie esses dois valores e baixe-os também para não perdê-los.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="9f6ed-253">e.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-253">e.</span></span> <span data-ttu-id="9f6ed-254">No hello Portal do Azure, na página de integração de aplicativos do hello serviços AWS (Amazon Web), clique em **provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-254">In hello Azure Portal, on hello Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Configurar Logon Único][35]

    <span data-ttu-id="9f6ed-256">f.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-256">f.</span></span> <span data-ttu-id="9f6ed-257">Definir o modo de provisionamento de saudação muito**automática**</span><span class="sxs-lookup"><span data-stu-id="9f6ed-257">Set hello Provisioning mode too**Automatic**</span></span>
        
       ![Configurar Logon Único][39]

    <span data-ttu-id="9f6ed-259">g.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-259">g.</span></span> <span data-ttu-id="9f6ed-260">Agora em Olá **clientsecret** e **segredo do Token** colar valores correspondentes hello, que você copiou do Console do AWS.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-260">Now in hello **clientsecret** and **Secret Token** paste hello corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="9f6ed-261">h.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-261">h.</span></span> <span data-ttu-id="9f6ed-262">Você pode clicar em Olá **Conexão de teste** botão tootest conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-262">You can click hello **Test Connection** button tootest hello connectivity.</span></span> <span data-ttu-id="9f6ed-263">Depois que for bem-sucedida, em seguida, você pode iniciar Olá provisionamento conector.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-263">Once that is successful then you can start hello provisioning connector.</span></span>
       
       ![Configurar Logon Único][40]

    <span data-ttu-id="9f6ed-265">i.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-265">i.</span></span> <span data-ttu-id="9f6ed-266">Habilitar Olá Status de provisionamento muito**em**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-266">Now enable hello Provisioning Status too**On**.</span></span> <span data-ttu-id="9f6ed-267">Isso inicia a busca de funções de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-267">This starts fetching hello roles from hello application.</span></span>

       ![Configurar Logon Único][41]

    > [!NOTE]
    > <span data-ttu-id="9f6ed-269">Serviço de provisionamento do AD do Azure é executado após algumas funções do tempo toosync saudação do AWS cada.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-269">Azure AD Provisioning service runs every after some time toosync hello roles from AWS.</span></span> <span data-ttu-id="9f6ed-270">Você deve ver todos os Olá provedor de identidade anexado funções AWS no AD do Azure e você pode usá-los durante a atribuição de saudação aplicativo toousers ou grupos.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-270">You should see all hello Identity Provider attached AWS roles into Azure AD and you can use them while assigning hello application toousers or groups.</span></span>

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f6ed-271">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6ed-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f6ed-272">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-272">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9f6ed-274">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f6ed-274">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f6ed-275">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-275">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f6ed-277">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-277">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f6ed-279">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-279">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f6ed-281">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-281">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f6ed-283">a.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-283">a.</span></span> <span data-ttu-id="9f6ed-284">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-284">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f6ed-285">b.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-285">b.</span></span> <span data-ttu-id="9f6ed-286">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-286">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9f6ed-287">c.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-287">c.</span></span> <span data-ttu-id="9f6ed-288">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-288">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9f6ed-289">d.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-289">d.</span></span> <span data-ttu-id="9f6ed-290">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="9f6ed-291">Criação de um usuário de teste do Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="9f6ed-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="9f6ed-292">Em ordem tooenable AD do Azure usuários toolog em tooAmazon AWS (Web Services), eles devem ser provisionados em serviços AWS (Amazon Web).</span><span class="sxs-lookup"><span data-stu-id="9f6ed-292">In order tooenable Azure AD users toolog in tooAmazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="9f6ed-293">No caso de saudação do Amazon Web Services AWS (), o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-293">In hello case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="9f6ed-294">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f6ed-294">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f6ed-295">Faça logon no tooyour **serviços AWS (Amazon Web)** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-295">Log in tooyour **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="9f6ed-296">Clique em Olá **página inicial do Console** ícone.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-296">Click hello **Console Home** icon.</span></span> 
   
    ![Configurar Logon Único][11]

3. <span data-ttu-id="9f6ed-298">Clique em Gerenciamento de identidades e acesso.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-298">Click Identity and Access Management.</span></span> 
   
    ![Configurar Logon Único][28]

4. <span data-ttu-id="9f6ed-300">No painel de Olá, clique em **usuários**e, em seguida, clique em **criar novos usuários**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-300">In hello Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Configurar Logon Único][29]

5. <span data-ttu-id="9f6ed-302">Na caixa de diálogo de Create User hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f6ed-302">On hello Create User dialog, perform hello following steps:</span></span> 
   
    ![Configurar Logon Único][30]   
    
    <span data-ttu-id="9f6ed-304">a.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-304">a.</span></span> <span data-ttu-id="9f6ed-305">Em Olá **Insira nomes de usuário** caixas de texto, digite o nome de usuário de Brita Simon (userprincipalname) no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-305">In hello **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="9f6ed-306">b.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-306">b.</span></span> <span data-ttu-id="9f6ed-307">Clicar em **Criar.**</span><span class="sxs-lookup"><span data-stu-id="9f6ed-307">Click **Create.**</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9f6ed-308">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6ed-308">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9f6ed-309">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooAmazon seu acesso AWS (Web Services).</span><span class="sxs-lookup"><span data-stu-id="9f6ed-309">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAmazon Web Services (AWS).</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9f6ed-311">**tooassign Britta Simon tooAmazon AWS (Web Services), execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f6ed-311">**tooassign Britta Simon tooAmazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="9f6ed-312">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-312">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9f6ed-314">Na lista de aplicativos hello, selecione **serviços AWS (Amazon Web)**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-314">In hello applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="9f6ed-316">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-316">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9f6ed-318">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-318">Click **Add** button.</span></span> <span data-ttu-id="9f6ed-319">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9f6ed-321">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-321">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9f6ed-322">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f6ed-323">Em **Selecionar função** guia, a função apropriada Olá Selecione usuário hello.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-323">On **Select Role** tab, select hello appropriate role for hello user.</span></span> <span data-ttu-id="9f6ed-324">Todas essas funções são mostradas com o nome da função hello e o nome do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-324">All these roles are shown with hello role name and identity provider name.</span></span> <span data-ttu-id="9f6ed-325">Dessa forma, que você pode identificar facilmente as funções de saudação do AWS.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-325">This way you can easily identify hello roles from AWS.</span></span>

8. <span data-ttu-id="9f6ed-326">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9f6ed-327">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9f6ed-327">Testing single sign-on</span></span>

<span data-ttu-id="9f6ed-328">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f6ed-328">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9f6ed-329">Quando você clica em Olá serviços AWS (Amazon Web) lado a lado no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de serviços AWS (Amazon Web).</span><span class="sxs-lookup"><span data-stu-id="9f6ed-329">When you click hello Amazon Web Services (AWS) tile in hello Access Panel, you should get automatically signed-on tooyour Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9f6ed-330">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9f6ed-330">Additional resources</span></span>

* [<span data-ttu-id="9f6ed-331">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9f6ed-331">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f6ed-332">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9f6ed-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
