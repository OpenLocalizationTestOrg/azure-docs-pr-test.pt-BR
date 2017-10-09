---
title: "Tutorial: integração do Azure Active Directory ao TimeOffManager | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="29c1d-103">Tutorial: Integração do Active Directory do Azure ao TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="29c1d-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="29c1d-104">Neste tutorial, você aprenderá como toointegrate TimeOffManager com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="29c1d-104">In this tutorial, you learn how toointegrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29c1d-105">Integrando o TimeOffManager com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="29c1d-105">Integrating TimeOffManager with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="29c1d-106">Você pode controlar no AD do Azure que tenha acesso tooTimeOffManager</span><span class="sxs-lookup"><span data-stu-id="29c1d-106">You can control in Azure AD who has access tooTimeOffManager</span></span>
- <span data-ttu-id="29c1d-107">Você pode habilitar seu usuários tooautomatically get conectado tooTimeOffManager (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="29c1d-107">You can enable your users tooautomatically get signed-on tooTimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="29c1d-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="29c1d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="29c1d-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29c1d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29c1d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="29c1d-110">Prerequisites</span></span>

<span data-ttu-id="29c1d-111">tooconfigure integração do AD do Azure com o TimeOffManager, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="29c1d-111">tooconfigure Azure AD integration with TimeOffManager, you need hello following items:</span></span>

- <span data-ttu-id="29c1d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="29c1d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29c1d-113">Uma assinatura habilitada para logon único do TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="29c1d-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29c1d-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="29c1d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29c1d-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="29c1d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29c1d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="29c1d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="29c1d-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29c1d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29c1d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="29c1d-118">Scenario description</span></span>
<span data-ttu-id="29c1d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="29c1d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29c1d-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="29c1d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29c1d-121">Adicionar TimeOffManager da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="29c1d-121">Add TimeOffManager from hello gallery</span></span>
2. <span data-ttu-id="29c1d-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="29c1d-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-hello-gallery"></a><span data-ttu-id="29c1d-123">Adicionar TimeOffManager da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="29c1d-123">Add TimeOffManager from hello gallery</span></span>
<span data-ttu-id="29c1d-124">integração de saudação tooconfigure do TimeOffManager no AD do Azure, você precisa tooadd TimeOffManager na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="29c1d-124">tooconfigure hello integration of TimeOffManager into Azure AD, you need tooadd TimeOffManager from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="29c1d-125">**tooadd TimeOffManager da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="29c1d-125">**tooadd TimeOffManager from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="29c1d-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="29c1d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="29c1d-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="29c1d-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="29c1d-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="29c1d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="29c1d-133">Na caixa de pesquisa hello, digite **TimeOffManager**, selecione **TimeOffManager** do painel de resultados e clique **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="29c1d-133">In hello search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button tooadd hello application.</span></span>

    ![Adicionar da galeria](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="29c1d-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="29c1d-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="29c1d-136">Nesta seção, você configurará e testará o logon único do Azure AD com o TimeOffManager, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="29c1d-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="29c1d-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no TimeOffManager é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="29c1d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TimeOffManager is tooa user in Azure AD.</span></span> <span data-ttu-id="29c1d-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no TimeOffManager precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="29c1d-138">In other words, a link relationship between an Azure AD user and hello related user in TimeOffManager needs toobe established.</span></span>

<span data-ttu-id="29c1d-139">No TimeOffManager, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="29c1d-139">In TimeOffManager, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="29c1d-140">tooconfigure e teste de logon único do AD do Azure com o TimeOffManager, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="29c1d-140">tooconfigure and test Azure AD single sign-on with TimeOffManager, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="29c1d-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="29c1d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="29c1d-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29c1d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29c1d-143">**[Criar um usuário de teste do TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave um equivalente do Britta Simon no TimeOffManager é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="29c1d-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - toohave a counterpart of Britta Simon in TimeOffManager that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="29c1d-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="29c1d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29c1d-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="29c1d-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="29c1d-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="29c1d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="29c1d-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="29c1d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="29c1d-148">**tooconfigure AD do Azure-logon único com o TimeOffManager, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="29c1d-148">**tooconfigure Azure AD single sign-on with TimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="29c1d-149">Em Olá portal do Azure, Olá **TimeOffManager** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-149">In hello Azure portal, on hello **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="29c1d-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="29c1d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Logon baseado em SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="29c1d-153">Em Olá **TimeOffManager domínio e URLs** , execute o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="29c1d-153">On hello **TimeOffManager Domain and URLs** section, perform hello following:</span></span>

     ![Seção Domínio e URLs do TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="29c1d-155">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="29c1d-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="29c1d-156">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="29c1d-156">This value is not real.</span></span> <span data-ttu-id="29c1d-157">Atualize esse valor com hello URL de resposta real.</span><span class="sxs-lookup"><span data-stu-id="29c1d-157">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="29c1d-158">Você pode obter esse valor de **página Configurações de logon único** que é explicado posteriormente no tutorial de saudação ou entre em contato com [equipe de suporte do TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="29c1d-158">You can get this value from **Single Sign on settings page** which is explained later in hello tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="29c1d-159">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="29c1d-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="29c1d-161">Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooTimeOffManger com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="29c1d-161">hello objective of this section is toooutline how tooenable users tooauthenticate tooTimeOffManger with their account in Azure AD using federation based on hello SAML protocol.</span></span>
    
    <span data-ttu-id="29c1d-162">Seu aplicativo TimeOffManger espera as asserções de SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML.</span><span class="sxs-lookup"><span data-stu-id="29c1d-162">Your TimeOffManger application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="29c1d-163">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="29c1d-163">hello following screenshot shows an example for this.</span></span>

    <span data-ttu-id="29c1d-164">![Atributos de Token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "Atributos de Token SAML")</span><span class="sxs-lookup"><span data-stu-id="29c1d-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="29c1d-165">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="29c1d-165">Attribute Name</span></span> | <span data-ttu-id="29c1d-166">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="29c1d-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="29c1d-167">Firstname</span><span class="sxs-lookup"><span data-stu-id="29c1d-167">Firstname</span></span> |<span data-ttu-id="29c1d-168">User.givenname</span><span class="sxs-lookup"><span data-stu-id="29c1d-168">User.givenname</span></span> |
    | <span data-ttu-id="29c1d-169">Sobrenome</span><span class="sxs-lookup"><span data-stu-id="29c1d-169">Lastname</span></span> |<span data-ttu-id="29c1d-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="29c1d-170">User.surname</span></span> |
    | <span data-ttu-id="29c1d-171">Email</span><span class="sxs-lookup"><span data-stu-id="29c1d-171">Email</span></span> |<span data-ttu-id="29c1d-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="29c1d-172">User.mail</span></span> |
    
    <span data-ttu-id="29c1d-173">a.</span><span class="sxs-lookup"><span data-stu-id="29c1d-173">a.</span></span>  <span data-ttu-id="29c1d-174">Para cada linha de dados na tabela de saudação acima, clique em **Adicionar atributo de usuário**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-174">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="29c1d-175">![Atributos de Token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "Atributos de Token SAML")</span><span class="sxs-lookup"><span data-stu-id="29c1d-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="29c1d-176">![Atributos de Token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "Atributos de Token SAML")</span><span class="sxs-lookup"><span data-stu-id="29c1d-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="29c1d-177">b.</span><span class="sxs-lookup"><span data-stu-id="29c1d-177">b.</span></span>  <span data-ttu-id="29c1d-178">Em Olá **nome do atributo** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="29c1d-178">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="29c1d-179">c.</span><span class="sxs-lookup"><span data-stu-id="29c1d-179">c.</span></span>  <span data-ttu-id="29c1d-180">Em Olá **o valor do atributo** texto, o valor do atributo select Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="29c1d-180">In hello **Attribute Value** textbox, select hello attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="29c1d-181">d.</span><span class="sxs-lookup"><span data-stu-id="29c1d-181">d.</span></span>  <span data-ttu-id="29c1d-182">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="29c1d-183">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="29c1d-183">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="29c1d-185">Em Olá **TimeOffManager configuração** seção, clique em **configurar TimeOffManager** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="29c1d-185">On hello **TimeOffManager Configuration** section, click **Configure TimeOffManager** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="29c1d-186">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="29c1d-186">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Seção de configuração do TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="29c1d-188">Em outra janela do navegador da Web, faça logon em seu site de empresa TimeOffManager como um administrador.</span><span class="sxs-lookup"><span data-stu-id="29c1d-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="29c1d-189">Vá muito**conta \> opções de conta \> configurações de logon único**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-189">Go too**Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="29c1d-190">![Configurações de Logon Único](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="29c1d-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="29c1d-191">Em Olá **configurações de logon único** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="29c1d-191">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="29c1d-192">![Configurações de Logon Único](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="29c1d-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="29c1d-193">a.</span><span class="sxs-lookup"><span data-stu-id="29c1d-193">a.</span></span> <span data-ttu-id="29c1d-194">Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e cole Olá certificado inteiro na **certificado x. 509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="29c1d-194">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="29c1d-195">b.</span><span class="sxs-lookup"><span data-stu-id="29c1d-195">b.</span></span> <span data-ttu-id="29c1d-196">Em **emissor Idp** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="29c1d-196">In **Idp Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="29c1d-197">c.</span><span class="sxs-lookup"><span data-stu-id="29c1d-197">c.</span></span> <span data-ttu-id="29c1d-198">Em **URL de ponto de extremidade IdP** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="29c1d-198">In **IdP Endpoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="29c1d-199">d.</span><span class="sxs-lookup"><span data-stu-id="29c1d-199">d.</span></span> <span data-ttu-id="29c1d-200">Para **Impor SAML**, selecione **Não**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="29c1d-201">e.</span><span class="sxs-lookup"><span data-stu-id="29c1d-201">e.</span></span> <span data-ttu-id="29c1d-202">Para **Criação Automática de Usuários**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="29c1d-203">f.</span><span class="sxs-lookup"><span data-stu-id="29c1d-203">f.</span></span> <span data-ttu-id="29c1d-204">Em **URL de Logout** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="29c1d-204">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="29c1d-205">g.</span><span class="sxs-lookup"><span data-stu-id="29c1d-205">g.</span></span> <span data-ttu-id="29c1d-206">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="29c1d-207">Em **configurações de logon único** página cópia Olá valor **URL do serviço de consumidor de declaração** e cole-o no hello **URL de resposta** caixa de texto em **TimeOffManager Domínio e URLs** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="29c1d-207">In **Single Sign on settings** page, copy hello value of **Assertion Consumer Service URL** and paste it in hello **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="29c1d-208">![Configurações de Logon Único](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="29c1d-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="29c1d-209">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="29c1d-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="29c1d-210">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="29c1d-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="29c1d-211">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="29c1d-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="29c1d-212">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="29c1d-212">Create an Azure AD test user</span></span>
<span data-ttu-id="29c1d-213">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="29c1d-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="29c1d-215">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="29c1d-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="29c1d-216">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="29c1d-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="29c1d-218">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Usuários e grupos --> Todos os usuários](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="29c1d-220">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="29c1d-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Botão Adicionar](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="29c1d-222">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="29c1d-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Página da caixa de diálogo do usuário](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="29c1d-224">a.</span><span class="sxs-lookup"><span data-stu-id="29c1d-224">a.</span></span> <span data-ttu-id="29c1d-225">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29c1d-226">b.</span><span class="sxs-lookup"><span data-stu-id="29c1d-226">b.</span></span> <span data-ttu-id="29c1d-227">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="29c1d-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="29c1d-228">c.</span><span class="sxs-lookup"><span data-stu-id="29c1d-228">c.</span></span> <span data-ttu-id="29c1d-229">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="29c1d-230">d.</span><span class="sxs-lookup"><span data-stu-id="29c1d-230">d.</span></span> <span data-ttu-id="29c1d-231">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="29c1d-232">Criar um usuário de teste do TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="29c1d-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="29c1d-233">Ordem tooenable AD do Azure usuários toolog no TimeOffManager, elas devem ser provisionado tooTimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="29c1d-233">In order tooenable Azure AD users toolog into TimeOffManager, they must be provisioned tooTimeOffManager.</span></span>  

<span data-ttu-id="29c1d-234">O TimeOffManager dá suporte ao provisionamento de usuário just in time.</span><span class="sxs-lookup"><span data-stu-id="29c1d-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="29c1d-235">Não há nenhum item de ação para você.</span><span class="sxs-lookup"><span data-stu-id="29c1d-235">There is no action item for you.</span></span>  

<span data-ttu-id="29c1d-236">usuários de saudação são adicionados automaticamente durante o primeiro logon de saudação usando o logon único.</span><span class="sxs-lookup"><span data-stu-id="29c1d-236">hello users are added automatically during hello first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="29c1d-237">Você pode usar qualquer ferramenta de criação outros TimeOffManager usuário conta ou APIs fornecidas pelo TimeOffManager tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="29c1d-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="29c1d-238">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="29c1d-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="29c1d-239">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="29c1d-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTimeOffManager.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="29c1d-241">**tooassign Britta Simon tooTimeOffManager, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="29c1d-241">**tooassign Britta Simon tooTimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="29c1d-242">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="29c1d-244">Na lista de aplicativos hello, selecione **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-244">In hello applications list, select **TimeOffManager**.</span></span>

    ![TimeOffManager na lista de aplicativos](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="29c1d-246">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="29c1d-248">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="29c1d-248">Click **Add** button.</span></span> <span data-ttu-id="29c1d-249">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="29c1d-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="29c1d-251">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="29c1d-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="29c1d-252">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="29c1d-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29c1d-253">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="29c1d-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="29c1d-254">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="29c1d-254">Test single sign-on</span></span>

<span data-ttu-id="29c1d-255">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="29c1d-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="29c1d-256">Quando você clica em bloco TimeOffManager Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour TimeOffManager aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29c1d-256">When you click hello TimeOffManager tile in hello Access Panel, you should get automatically signed-on tooyour TimeOffManager application.</span></span> <span data-ttu-id="29c1d-257">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29c1d-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="29c1d-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="29c1d-258">Additional resources</span></span>

* [<span data-ttu-id="29c1d-259">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="29c1d-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29c1d-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="29c1d-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

