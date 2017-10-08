---
title: "Tutorial: Integração do Azure Active Directory com o Allocadia | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Allocadia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: 9a01c232f9dc50e690dd348430899db9c13f1564
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="c66c8-103">Tutorial: Integração do Azure Active Directory ao Allocadia</span><span class="sxs-lookup"><span data-stu-id="c66c8-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="c66c8-104">Neste tutorial, você aprenderá como toointegrate Allocadia com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c66c8-104">In this tutorial, you learn how toointegrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c66c8-105">Integrando Allocadia com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c66c8-105">Integrating Allocadia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c66c8-106">Você pode controlar no AD do Azure que tenha acesso tooAllocadia</span><span class="sxs-lookup"><span data-stu-id="c66c8-106">You can control in Azure AD who has access tooAllocadia</span></span>
- <span data-ttu-id="c66c8-107">Você pode habilitar seu usuários tooautomatically get conectado tooAllocadia (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c66c8-107">You can enable your users tooautomatically get signed-on tooAllocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c66c8-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c66c8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c66c8-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c66c8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c66c8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c66c8-110">Prerequisites</span></span>

<span data-ttu-id="c66c8-111">tooconfigure integração do AD do Azure com Allocadia, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c66c8-111">tooconfigure Azure AD integration with Allocadia, you need hello following items:</span></span>

- <span data-ttu-id="c66c8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c66c8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c66c8-113">Uma assinatura habilitada para logon único do Allocadia</span><span class="sxs-lookup"><span data-stu-id="c66c8-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c66c8-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c66c8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c66c8-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c66c8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c66c8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c66c8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c66c8-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c66c8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c66c8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c66c8-118">Scenario description</span></span>
<span data-ttu-id="c66c8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c66c8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c66c8-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c66c8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c66c8-121">Adicionando Allocadia da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c66c8-121">Adding Allocadia from hello gallery</span></span>
2. <span data-ttu-id="c66c8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c66c8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-hello-gallery"></a><span data-ttu-id="c66c8-123">Adicionando Allocadia da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c66c8-123">Adding Allocadia from hello gallery</span></span>
<span data-ttu-id="c66c8-124">integração de saudação tooconfigure de Allocadia no AD do Azure, você precisa tooadd Allocadia da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c66c8-124">tooconfigure hello integration of Allocadia into Azure AD, you need tooadd Allocadia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c66c8-125">**tooadd Allocadia da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c66c8-125">**tooadd Allocadia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c66c8-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c66c8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c66c8-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c66c8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c66c8-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c66c8-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c66c8-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c66c8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c66c8-133">Na caixa de pesquisa hello, digite **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="c66c8-133">In hello search box, type **Allocadia**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="c66c8-135">No painel de resultados de saudação, selecione **Allocadia**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c66c8-135">In hello results panel, select **Allocadia**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c66c8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c66c8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c66c8-138">Nesta seção, você configura e testa o logon único do Azure AD com o Allocadia, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c66c8-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c66c8-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Allocadia é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c66c8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Allocadia is tooa user in Azure AD.</span></span> <span data-ttu-id="c66c8-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Allocadia precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c66c8-140">In other words, a link relationship between an Azure AD user and hello related user in Allocadia needs toobe established.</span></span>

<span data-ttu-id="c66c8-141">Allocadia, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c66c8-141">In Allocadia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c66c8-142">tooconfigure e teste de logon único do AD do Azure com Allocadia, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c66c8-142">tooconfigure and test Azure AD single sign-on with Allocadia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c66c8-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c66c8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c66c8-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c66c8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c66c8-145">**[Criar um usuário de teste Allocadia](#creating-an-allocadia-test-user)**  -toohave um equivalente do Britta Simon em Allocadia é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c66c8-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - toohave a counterpart of Britta Simon in Allocadia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c66c8-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c66c8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c66c8-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c66c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c66c8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c66c8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c66c8-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Allocadia.</span><span class="sxs-lookup"><span data-stu-id="c66c8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="c66c8-150">**tooconfigure AD do Azure-logon único com Allocadia, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c66c8-150">**tooconfigure Azure AD single sign-on with Allocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="c66c8-151">Em Olá portal do Azure, Olá **Allocadia** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c66c8-151">In hello Azure portal, on hello **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c66c8-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c66c8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="c66c8-155">Em Olá **Allocadia domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c66c8-155">On hello **Allocadia Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="c66c8-157">a.</span><span class="sxs-lookup"><span data-stu-id="c66c8-157">a.</span></span> <span data-ttu-id="c66c8-158">Em Olá **identificador** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="c66c8-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
       
     <span data-ttu-id="c66c8-159">Para o ambiente de teste – `https://na2standby.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="c66c8-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="c66c8-160">Para o ambiente de produção – `https://na2.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="c66c8-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="c66c8-161">b.</span><span class="sxs-lookup"><span data-stu-id="c66c8-161">b.</span></span> <span data-ttu-id="c66c8-162">Em Olá **URL de resposta** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="c66c8-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
     <span data-ttu-id="c66c8-163">Para o ambiente de teste – `https://na2standby.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="c66c8-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="c66c8-164">Para o ambiente de produção – `https://na2.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="c66c8-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c66c8-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c66c8-165">These values are not real.</span></span> <span data-ttu-id="c66c8-166">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="c66c8-166">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c66c8-167">Entre em contato com [Allocadia a equipe de suporte](mailTo:support@allocadia.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="c66c8-167">Contact [Allocadia support team](mailTo:support@allocadia.com) tooget these values.</span></span>

4. <span data-ttu-id="c66c8-168">Aplicativo de Allocadia espera asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="c66c8-168">Allocadia application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="c66c8-169">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c66c8-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="c66c8-170">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c66c8-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="c66c8-171">Olá captura de tela a seguir mostra um exemplo para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="c66c8-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="c66c8-173">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c66c8-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="c66c8-174">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="c66c8-174">Attribute Name</span></span> | <span data-ttu-id="c66c8-175">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="c66c8-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="c66c8-176">nome</span><span class="sxs-lookup"><span data-stu-id="c66c8-176">firstname</span></span> | <span data-ttu-id="c66c8-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="c66c8-177">user.givenname</span></span> |
    | <span data-ttu-id="c66c8-178">sobrenome</span><span class="sxs-lookup"><span data-stu-id="c66c8-178">lastname</span></span> | <span data-ttu-id="c66c8-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="c66c8-179">user.surname</span></span> |
    | <span data-ttu-id="c66c8-180">email</span><span class="sxs-lookup"><span data-stu-id="c66c8-180">email</span></span> | <span data-ttu-id="c66c8-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="c66c8-181">user.mail</span></span> |
    
    <span data-ttu-id="c66c8-182">a.</span><span class="sxs-lookup"><span data-stu-id="c66c8-182">a.</span></span> <span data-ttu-id="c66c8-183">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c66c8-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="c66c8-185">b.</span><span class="sxs-lookup"><span data-stu-id="c66c8-185">b.</span></span> <span data-ttu-id="c66c8-186">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="c66c8-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="c66c8-188">c.</span><span class="sxs-lookup"><span data-stu-id="c66c8-188">c.</span></span> <span data-ttu-id="c66c8-189">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="c66c8-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
 
    <span data-ttu-id="c66c8-190">d.</span><span class="sxs-lookup"><span data-stu-id="c66c8-190">d.</span></span> <span data-ttu-id="c66c8-191">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c66c8-191">Click **Ok**.</span></span>



6. <span data-ttu-id="c66c8-192">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c66c8-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="c66c8-194">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c66c8-194">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c66c8-196">tooconfigure logon único no **Allocadia** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte Allocadia](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="c66c8-196">tooconfigure single sign-on on **Allocadia** side, you need toosend hello downloaded **Metadata XML** too[Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="c66c8-197">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="c66c8-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c66c8-198">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c66c8-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c66c8-199">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c66c8-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c66c8-200">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c66c8-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c66c8-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c66c8-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="c66c8-202">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c66c8-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c66c8-204">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c66c8-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c66c8-205">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c66c8-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c66c8-207">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c66c8-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c66c8-209">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c66c8-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c66c8-211">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c66c8-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c66c8-213">a.</span><span class="sxs-lookup"><span data-stu-id="c66c8-213">a.</span></span> <span data-ttu-id="c66c8-214">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c66c8-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c66c8-215">b.</span><span class="sxs-lookup"><span data-stu-id="c66c8-215">b.</span></span> <span data-ttu-id="c66c8-216">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c66c8-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c66c8-217">c.</span><span class="sxs-lookup"><span data-stu-id="c66c8-217">c.</span></span> <span data-ttu-id="c66c8-218">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c66c8-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c66c8-219">d.</span><span class="sxs-lookup"><span data-stu-id="c66c8-219">d.</span></span> <span data-ttu-id="c66c8-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c66c8-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="c66c8-221">Criação um usuário de teste do Allocadia</span><span class="sxs-lookup"><span data-stu-id="c66c8-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="c66c8-222">O aplicativo dá suporte ao provisionamento de usuário Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="c66c8-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="c66c8-223">Após a autenticação de usuários são criados no aplicativo hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c66c8-223">After authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c66c8-224">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c66c8-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c66c8-225">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAllocadia.</span><span class="sxs-lookup"><span data-stu-id="c66c8-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAllocadia.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c66c8-227">**tooassign Britta Simon tooAllocadia, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c66c8-227">**tooassign Britta Simon tooAllocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="c66c8-228">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c66c8-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c66c8-230">Na lista de aplicativos hello, selecione **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="c66c8-230">In hello applications list, select **Allocadia**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="c66c8-232">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c66c8-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c66c8-234">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c66c8-234">Click **Add** button.</span></span> <span data-ttu-id="c66c8-235">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c66c8-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c66c8-237">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c66c8-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c66c8-238">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c66c8-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c66c8-239">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c66c8-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c66c8-240">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c66c8-240">Testing single sign-on</span></span>

<span data-ttu-id="c66c8-241">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c66c8-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c66c8-242">Quando você clica em bloco Allocadia Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Allocadia aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c66c8-242">When you click hello Allocadia tile in hello Access Panel, you should get automatically signed-on tooyour Allocadia application.</span></span>
<span data-ttu-id="c66c8-243">Para obter mais informações sobre o painel de acesso, consulte [Introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c66c8-243">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c66c8-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c66c8-244">Additional resources</span></span>

* [<span data-ttu-id="c66c8-245">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c66c8-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c66c8-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c66c8-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png

