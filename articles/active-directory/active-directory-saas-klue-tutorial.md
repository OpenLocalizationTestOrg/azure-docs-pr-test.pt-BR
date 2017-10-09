---
title: "Tutorial: Integração do Azure Active Directory ao Klue | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Klue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: bb9134a558d6c050f428690d57a3cea850b7dbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a><span data-ttu-id="77b28-103">Tutorial: Integração do Azure Active Directory ao Klue</span><span class="sxs-lookup"><span data-stu-id="77b28-103">Tutorial: Azure Active Directory integration with Klue</span></span>

<span data-ttu-id="77b28-104">Neste tutorial, você aprenderá como toointegrate Klue com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="77b28-104">In this tutorial, you learn how toointegrate Klue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77b28-105">Integrando Klue com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="77b28-105">Integrating Klue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="77b28-106">Você pode controlar no AD do Azure que tenha acesso tooKlue</span><span class="sxs-lookup"><span data-stu-id="77b28-106">You can control in Azure AD who has access tooKlue</span></span>
- <span data-ttu-id="77b28-107">Você pode habilitar seu usuários tooautomatically get conectado tooKlue (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="77b28-107">You can enable your users tooautomatically get signed-on tooKlue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77b28-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="77b28-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="77b28-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77b28-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77b28-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="77b28-110">Prerequisites</span></span>

<span data-ttu-id="77b28-111">tooconfigure integração do AD do Azure com Klue, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="77b28-111">tooconfigure Azure AD integration with Klue, you need hello following items:</span></span>

- <span data-ttu-id="77b28-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="77b28-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77b28-113">Uma assinatura habilitada para logon único do Klue</span><span class="sxs-lookup"><span data-stu-id="77b28-113">A Klue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77b28-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="77b28-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77b28-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="77b28-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77b28-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="77b28-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77b28-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77b28-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77b28-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="77b28-118">Scenario description</span></span>
<span data-ttu-id="77b28-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="77b28-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77b28-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="77b28-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77b28-121">Adicionando Klue da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="77b28-121">Adding Klue from hello gallery</span></span>
2. <span data-ttu-id="77b28-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="77b28-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-klue-from-hello-gallery"></a><span data-ttu-id="77b28-123">Adicionando Klue da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="77b28-123">Adding Klue from hello gallery</span></span>
<span data-ttu-id="77b28-124">integração de saudação tooconfigure de Klue no AD do Azure, você precisa tooadd Klue da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="77b28-124">tooconfigure hello integration of Klue into Azure AD, you need tooadd Klue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="77b28-125">**tooadd Klue da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="77b28-125">**tooadd Klue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="77b28-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="77b28-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="77b28-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="77b28-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="77b28-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="77b28-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="77b28-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="77b28-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="77b28-133">Na caixa de pesquisa hello, digite **Klue**.</span><span class="sxs-lookup"><span data-stu-id="77b28-133">In hello search box, type **Klue**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-klue-tutorial/tutorial_klue_search.png)

5. <span data-ttu-id="77b28-135">No painel de resultados de saudação, selecione **Klue**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="77b28-135">In hello results panel, select **Klue**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="77b28-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="77b28-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="77b28-138">Nesta seção, você configura e testa o logon único do Azure AD com o Klue, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="77b28-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="77b28-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Klue é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="77b28-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Klue is tooa user in Azure AD.</span></span> <span data-ttu-id="77b28-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Klue precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="77b28-140">In other words, a link relationship between an Azure AD user and hello related user in Klue needs toobe established.</span></span>

<span data-ttu-id="77b28-141">Klue, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="77b28-141">In Klue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="77b28-142">tooconfigure e teste de logon único do AD do Azure com Klue, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="77b28-142">tooconfigure and test Azure AD single sign-on with Klue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="77b28-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="77b28-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="77b28-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77b28-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77b28-145">**[Criar um usuário de teste Klue](#creating-a-klue-test-user)**  -toohave um equivalente do Britta Simon em Klue é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="77b28-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - toohave a counterpart of Britta Simon in Klue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="77b28-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="77b28-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77b28-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="77b28-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="77b28-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="77b28-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="77b28-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Klue.</span><span class="sxs-lookup"><span data-stu-id="77b28-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Klue application.</span></span>

<span data-ttu-id="77b28-150">**tooconfigure AD do Azure-logon único com Klue, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="77b28-150">**tooconfigure Azure AD single sign-on with Klue, perform hello following steps:**</span></span>

1. <span data-ttu-id="77b28-151">Em Olá portal do Azure, Olá **Klue** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="77b28-151">In hello Azure portal, on hello **Klue** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="77b28-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="77b28-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-klue-tutorial/tutorial_klue_samlbase.png)

3. <span data-ttu-id="77b28-155">Em Olá **Klue domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="77b28-155">On hello **Klue Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-klue-tutorial/tutorial_klue_url1.png)

    <span data-ttu-id="77b28-157">a.</span><span class="sxs-lookup"><span data-stu-id="77b28-157">a.</span></span> <span data-ttu-id="77b28-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`urn:klue:<Customer ID>`</span><span class="sxs-lookup"><span data-stu-id="77b28-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:klue:<Customer ID>`</span></span>

    <span data-ttu-id="77b28-159">b.</span><span class="sxs-lookup"><span data-stu-id="77b28-159">b.</span></span> <span data-ttu-id="77b28-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span><span class="sxs-lookup"><span data-stu-id="77b28-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span></span>

4. <span data-ttu-id="77b28-161">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="77b28-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="77b28-162">Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="77b28-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-klue-tutorial/tutorial_klue_url2.png)

    <span data-ttu-id="77b28-164">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://app.klue.com/account/auth/saml/<Customer UUID>/`</span><span class="sxs-lookup"><span data-stu-id="77b28-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="77b28-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="77b28-165">These values are not real.</span></span> <span data-ttu-id="77b28-166">Atualize esses valores com URL de resposta real hello, identificador e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="77b28-166">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="77b28-167">Entre em contato com [equipe de suporte do cliente Klue](mailto:support@klue.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="77b28-167">Contact [Klue Client support team](mailto:support@klue.com) tooget these values.</span></span>

5. <span data-ttu-id="77b28-168">Olá Klue aplicativo espera as asserções de SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML.</span><span class="sxs-lookup"><span data-stu-id="77b28-168">hello Klue application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="77b28-169">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77b28-169">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-klue-tutorial/attribute.png)

6. <span data-ttu-id="77b28-171">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, como mostrado no hello anterior a imagem e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="77b28-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="77b28-172">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="77b28-172">Attribute Name</span></span>      | <span data-ttu-id="77b28-173">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="77b28-173">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="77b28-174">first_name</span><span class="sxs-lookup"><span data-stu-id="77b28-174">first_name</span></span>          | <span data-ttu-id="77b28-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="77b28-175">user.givenname</span></span> |
    | <span data-ttu-id="77b28-176">last_name</span><span class="sxs-lookup"><span data-stu-id="77b28-176">last_name</span></span>           | <span data-ttu-id="77b28-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="77b28-177">user.surname</span></span> |
    | <span data-ttu-id="77b28-178">email</span><span class="sxs-lookup"><span data-stu-id="77b28-178">email</span></span>               | <span data-ttu-id="77b28-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="77b28-179">user.userprincipalname</span></span>|
    
    <span data-ttu-id="77b28-180">a.</span><span class="sxs-lookup"><span data-stu-id="77b28-180">a.</span></span> <span data-ttu-id="77b28-181">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="77b28-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-klue-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-klue-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="77b28-184">b.</span><span class="sxs-lookup"><span data-stu-id="77b28-184">b.</span></span> <span data-ttu-id="77b28-185">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="77b28-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="77b28-186">c.</span><span class="sxs-lookup"><span data-stu-id="77b28-186">c.</span></span> <span data-ttu-id="77b28-187">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="77b28-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="77b28-188">d.</span><span class="sxs-lookup"><span data-stu-id="77b28-188">d.</span></span> <span data-ttu-id="77b28-189">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="77b28-189">Click **Ok**.</span></span>

7. <span data-ttu-id="77b28-190">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="77b28-190">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-klue-tutorial/tutorial_klue_certificate.png) 

8. <span data-ttu-id="77b28-192">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="77b28-192">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-klue-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="77b28-194">Em Olá **Klue configuração** seção, clique em **configurar Klue** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="77b28-194">On hello **Klue Configuration** section, click **Configure Klue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="77b28-195">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="77b28-195">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-klue-tutorial/tutorial_klue_configure.png) 

10. <span data-ttu-id="77b28-197">tooconfigure logon único no **Klue** lado, você precisa toosend Olá baixado **Certificate(Base64), Single Sign-On URL do serviço SAML e ID de entidade de SAML** muito[Klue a equipe de suporte](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="77b28-197">tooconfigure single sign-on on **Klue** side, you need toosend hello downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** too[Klue support team](mailto:support@klue.com).</span></span>

> [!TIP]
> <span data-ttu-id="77b28-198">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="77b28-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="77b28-199">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="77b28-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="77b28-200">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77b28-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="77b28-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="77b28-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="77b28-202">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="77b28-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="77b28-204">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="77b28-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="77b28-205">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="77b28-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-klue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77b28-207">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="77b28-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-klue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77b28-209">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="77b28-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-klue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77b28-211">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="77b28-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-klue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77b28-213">a.</span><span class="sxs-lookup"><span data-stu-id="77b28-213">a.</span></span> <span data-ttu-id="77b28-214">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77b28-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77b28-215">b.</span><span class="sxs-lookup"><span data-stu-id="77b28-215">b.</span></span> <span data-ttu-id="77b28-216">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="77b28-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77b28-217">c.</span><span class="sxs-lookup"><span data-stu-id="77b28-217">c.</span></span> <span data-ttu-id="77b28-218">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="77b28-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="77b28-219">d.</span><span class="sxs-lookup"><span data-stu-id="77b28-219">d.</span></span> <span data-ttu-id="77b28-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="77b28-220">Click **Create**.</span></span>
 
### <a name="creating-a-klue-test-user"></a><span data-ttu-id="77b28-221">Criando um usuário de teste do Klue</span><span class="sxs-lookup"><span data-stu-id="77b28-221">Creating a Klue test user</span></span>

<span data-ttu-id="77b28-222">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Klue.</span><span class="sxs-lookup"><span data-stu-id="77b28-222">hello objective of this section is toocreate a user called Britta Simon in Klue.</span></span> <span data-ttu-id="77b28-223">O Klue dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="77b28-223">Klue supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="77b28-224">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="77b28-224">There is no action item for you in this section.</span></span> <span data-ttu-id="77b28-225">Um novo usuário é criado durante uma tentativa tooaccess Klue se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="77b28-225">A new user is created during an attempt tooaccess Klue if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="77b28-226">Se você precisar toocreate um usuário manualmente, entre em contato com [a equipe de suporte Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="77b28-226">If you need toocreate a user manually, Contact [Klue support team](mailto:support@klue.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="77b28-227">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="77b28-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="77b28-228">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooKlue.</span><span class="sxs-lookup"><span data-stu-id="77b28-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKlue.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="77b28-230">**tooassign Britta Simon tooKlue, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="77b28-230">**tooassign Britta Simon tooKlue, perform hello following steps:**</span></span>

1. <span data-ttu-id="77b28-231">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="77b28-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="77b28-233">Na lista de aplicativos hello, selecione **Klue**.</span><span class="sxs-lookup"><span data-stu-id="77b28-233">In hello applications list, select **Klue**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-klue-tutorial/tutorial_klue_app.png) 

3. <span data-ttu-id="77b28-235">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="77b28-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="77b28-237">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="77b28-237">Click **Add** button.</span></span> <span data-ttu-id="77b28-238">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="77b28-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="77b28-240">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="77b28-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="77b28-241">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="77b28-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77b28-242">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="77b28-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="77b28-243">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="77b28-243">Testing single sign-on</span></span>

<span data-ttu-id="77b28-244">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="77b28-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="77b28-245">Quando você clica em bloco Klue Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Klue aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77b28-245">When you click hello Klue tile in hello Access Panel, you should get automatically signed-on tooyour Klue application.</span></span>
<span data-ttu-id="77b28-246">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="77b28-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="77b28-247">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="77b28-247">Additional resources</span></span>

* [<span data-ttu-id="77b28-248">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="77b28-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77b28-249">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="77b28-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-klue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-klue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-klue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-klue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-klue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-klue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-klue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-klue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-klue-tutorial/tutorial_general_203.png

