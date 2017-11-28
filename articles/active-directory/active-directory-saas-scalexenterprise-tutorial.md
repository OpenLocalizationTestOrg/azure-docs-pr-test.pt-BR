---
title: "Tutorial: Integração do Azure Active Directory ao ScaleX Enterprise | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="18a50-103">Tutorial: Integração do Azure Active Directory ao ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="18a50-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="18a50-104">Neste tutorial, você aprenderá como toointegrate ScaleX Enterprise com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="18a50-104">In this tutorial, you learn how toointegrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18a50-105">Integrando ScaleX Enterprise com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="18a50-105">Integrating ScaleX Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="18a50-106">Você pode controlar no AD do Azure que tenha acesso tooScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="18a50-106">You can control in Azure AD who has access tooScaleX Enterprise</span></span>
- <span data-ttu-id="18a50-107">Você pode habilitar seu usuários tooautomatically get conectado tooScaleX Enterprise (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="18a50-107">You can enable your users tooautomatically get signed-on tooScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="18a50-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="18a50-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="18a50-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte.</span><span class="sxs-lookup"><span data-stu-id="18a50-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="18a50-110">O que é o acesso a aplicativos e logon único com o [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="18a50-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18a50-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="18a50-111">Prerequisites</span></span>

<span data-ttu-id="18a50-112">tooconfigure integração do AD do Azure com ScaleX Enterprise, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="18a50-112">tooconfigure Azure AD integration with ScaleX Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="18a50-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="18a50-113">An Azure AD subscription</span></span>
- <span data-ttu-id="18a50-114">Uma assinatura do ScaleX Enterprise habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="18a50-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18a50-115">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="18a50-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18a50-116">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="18a50-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18a50-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="18a50-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="18a50-118">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18a50-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18a50-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="18a50-119">Scenario description</span></span>
<span data-ttu-id="18a50-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="18a50-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18a50-121">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="18a50-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18a50-122">Adicionando ScaleX Enterprise na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="18a50-122">Adding ScaleX Enterprise from hello gallery</span></span>
2. <span data-ttu-id="18a50-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="18a50-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-hello-gallery"></a><span data-ttu-id="18a50-124">Adicionando ScaleX Enterprise na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="18a50-124">Adding ScaleX Enterprise from hello gallery</span></span>
<span data-ttu-id="18a50-125">tooconfigure Olá integração do ScaleX Enterprise tooAzure AD, é necessário tooadd ScaleX Enterprise na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="18a50-125">tooconfigure hello integration of ScaleX Enterprise in tooAzure AD, you need tooadd ScaleX Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="18a50-126">**tooadd ScaleX Enterprise na Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="18a50-126">**tooadd ScaleX Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="18a50-127">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="18a50-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="18a50-129">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="18a50-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="18a50-130">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="18a50-130">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="18a50-132">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="18a50-132">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="18a50-134">Na caixa de pesquisa hello, digite **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="18a50-134">In hello search box, type **ScaleX Enterprise**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="18a50-136">No painel de resultados de saudação, selecione **ScaleX Enterprise**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="18a50-136">In hello results panel, select **ScaleX Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="18a50-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="18a50-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="18a50-139">Nesta seção, você configura e testa o logon único do Azure AD com o ScaleX Enterprise, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="18a50-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="18a50-140">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá empresa ScaleX é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="18a50-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScaleX Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="18a50-141">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação ScaleX empresa precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="18a50-141">In other words, a link relationship between an Azure AD user and hello related user in ScaleX Enterprise needs toobe established.</span></span>

<span data-ttu-id="18a50-142">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** ScaleX empresa.</span><span class="sxs-lookup"><span data-stu-id="18a50-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="18a50-143">tooconfigure e teste de logon único do AD do Azure com ScaleX Enterprise, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="18a50-143">tooconfigure and test Azure AD single sign-on with ScaleX Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="18a50-144">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="18a50-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="18a50-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18a50-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18a50-146">**[Criar um usuário de teste ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave um equivalente do Britta Simon ScaleX empresa que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="18a50-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - toohave a counterpart of Britta Simon in ScaleX Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="18a50-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="18a50-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18a50-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="18a50-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="18a50-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="18a50-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="18a50-150">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="18a50-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="18a50-151">**tooconfigure AD do Azure-logon único com ScaleX Enterprise, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="18a50-151">**tooconfigure Azure AD single sign-on with ScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="18a50-152">Em Olá portal do Azure, Olá **ScaleX Enterprise** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="18a50-152">In hello Azure portal, on hello **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="18a50-154">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="18a50-154">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="18a50-156">Em Olá **ScaleX domínio da empresa e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="18a50-156">On hello **ScaleX Enterprise Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="18a50-158">a.</span><span class="sxs-lookup"><span data-stu-id="18a50-158">a.</span></span> <span data-ttu-id="18a50-159">Em Olá **identificador** texto, o valor do tipo hello usando saudação padrão a seguir:`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="18a50-159">In hello **Identifier** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="18a50-160">b.</span><span class="sxs-lookup"><span data-stu-id="18a50-160">b.</span></span> <span data-ttu-id="18a50-161">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="18a50-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="18a50-162">Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="18a50-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="18a50-164">Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="18a50-164">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="18a50-165">Eles não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="18a50-165">These are not hello real values.</span></span> <span data-ttu-id="18a50-166">Atualize esses valores com hello identificador real, a URL de resposta ou a URL de logon.</span><span class="sxs-lookup"><span data-stu-id="18a50-166">Update these values with hello actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="18a50-167">Entre em contato com [a equipe de suporte ScaleX Enterprise Client](http://info.rescale.com/contact_sales) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="18a50-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) tooget these values.</span></span> 

5. <span data-ttu-id="18a50-168">Seu aplicativo ScaleX espera as asserções de SAML de saudação em um formato específico, o que exige que você toomodify atributo personalizado mapeamentos tooyour atributos de token configuração SAML.</span><span class="sxs-lookup"><span data-stu-id="18a50-168">Your ScaleX application expects hello SAML assertions in a specific format, which requires you toomodify custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="18a50-169">Clique em **exibir e editar todos os outros atributos de usuário** configurações de atributos de caixa de seleção tooopen Olá personalizado.</span><span class="sxs-lookup"><span data-stu-id="18a50-169">Click **View and edit all other user attributes** checkbox tooopen hello custom attributes settings.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="18a50-171">a.</span><span class="sxs-lookup"><span data-stu-id="18a50-171">a.</span></span> <span data-ttu-id="18a50-172">Clique com botão direito atributo Olá **nome** e clique em Excluir.</span><span class="sxs-lookup"><span data-stu-id="18a50-172">Right click hello attribute **name** and click delete.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="18a50-174">b.</span><span class="sxs-lookup"><span data-stu-id="18a50-174">b.</span></span> <span data-ttu-id="18a50-175">Clique em **emailaddress** janela Editar atributo do atributo tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="18a50-175">Click **emailaddress** attribute tooopen hello Edit Attribute window.</span></span> <span data-ttu-id="18a50-176">Altere o valor de **user.mail** muito**User** e clique em Okey.</span><span class="sxs-lookup"><span data-stu-id="18a50-176">Change its value from **user.mail** too**user.userprincipalname** and click Ok.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="18a50-178">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="18a50-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="18a50-180">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="18a50-180">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="18a50-182">Em Olá **ScaleX Enterprise configuração** seção, clique em **configurar ScaleX Enterprise** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="18a50-182">On hello **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="18a50-183">Saudação de cópia **ID da entidade SAML** e **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="18a50-183">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="18a50-185">tooconfigure logon único no **ScaleX Enterprise** lado, o site da empresa do logon toohello ScaleX Enterprise como um administrador.</span><span class="sxs-lookup"><span data-stu-id="18a50-185">tooconfigure single sign-on on **ScaleX Enterprise** side, login toohello ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="18a50-186">Clique em menu Olá Olá superior direito e selecione **Contoso administração**.</span><span class="sxs-lookup"><span data-stu-id="18a50-186">Click hello menu in hello upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="18a50-187">Contoso é apenas um exemplo.</span><span class="sxs-lookup"><span data-stu-id="18a50-187">Contoso is just an example.</span></span> <span data-ttu-id="18a50-188">Esse deve ser o Nome real de sua Empresa.</span><span class="sxs-lookup"><span data-stu-id="18a50-188">This should be your actual Company Name.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="18a50-190">Selecione **integrações** no menu superior hello e selecione **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="18a50-190">Select **Integrations** from hello top menu and select **Single Sign-On**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="18a50-192">Preencha o formulário de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="18a50-192">Complete hello form as follows:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="18a50-194">a.</span><span class="sxs-lookup"><span data-stu-id="18a50-194">a.</span></span> <span data-ttu-id="18a50-195">Selecione **“Criar qualquer usuário que pode se autenticar com o SSO”.**</span><span class="sxs-lookup"><span data-stu-id="18a50-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="18a50-196">b.</span><span class="sxs-lookup"><span data-stu-id="18a50-196">b.</span></span> <span data-ttu-id="18a50-197">**Provedor saml**: colar Olá valor ***urn: oasis: nomes: tc: SAML:2.0:nameid-formato: persistente***</span><span class="sxs-lookup"><span data-stu-id="18a50-197">**Service Provider saml**: Paste hello value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="18a50-198">c.</span><span class="sxs-lookup"><span data-stu-id="18a50-198">c.</span></span> <span data-ttu-id="18a50-199">**Nome de campo de email do provedor de identidade na resposta do ACS**: colar Olá valor`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="18a50-199">**Name of Identity Provider email field in ACS response**: Paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="18a50-200">d.</span><span class="sxs-lookup"><span data-stu-id="18a50-200">d.</span></span> <span data-ttu-id="18a50-201">**ID de entidade EntityDescriptor do provedor de identidade:** Olá colar **ID da entidade SAML** valor copiado do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="18a50-201">**Identity Provider EntityDescriptor Entity ID:** Paste hello **SAML Entity ID** value copied from hello Azure portal.</span></span>

    <span data-ttu-id="18a50-202">e.</span><span class="sxs-lookup"><span data-stu-id="18a50-202">e.</span></span> <span data-ttu-id="18a50-203">**URL de SingleSignOnService do provedor de identidade:** Olá colar **Single Sign-On URL do serviço SAML** de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="18a50-203">**Identity Provider SingleSignOnService URL:** Paste hello **SAML Single Sign-On Service URL** from hello Azure portal.</span></span>

    <span data-ttu-id="18a50-204">f.</span><span class="sxs-lookup"><span data-stu-id="18a50-204">f.</span></span> <span data-ttu-id="18a50-205">**Certificado público X509 do provedor de identidade:** certificado abra Olá X509 baixado do hello Azure no bloco de notas e cole conteúdo Olá nesta caixa.</span><span class="sxs-lookup"><span data-stu-id="18a50-205">**Identity Provider public X509 certificate:** Open hello X509 certificate downloaded from hello Azure in notepad and paste hello contents in this box.</span></span> <span data-ttu-id="18a50-206">Certifique-se de que não há que nenhuma linha de quebra em Olá intermediária do conteúdo do certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="18a50-206">Ensure there are no line breaks in hello middle of hello certificate contents.</span></span>
    
    <span data-ttu-id="18a50-207">g.</span><span class="sxs-lookup"><span data-stu-id="18a50-207">g.</span></span> <span data-ttu-id="18a50-208">Verificar Olá caixas de seleção a seguir: **habilitado, criptografar NameID e AuthnRequests de entrada.**</span><span class="sxs-lookup"><span data-stu-id="18a50-208">Check hello following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="18a50-209">h.</span><span class="sxs-lookup"><span data-stu-id="18a50-209">h.</span></span> <span data-ttu-id="18a50-210">Clique em **configurações de atualização de SSO** toosave configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="18a50-210">Click **Update SSO Settings** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="18a50-211">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="18a50-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="18a50-212">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="18a50-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="18a50-213">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="18a50-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="18a50-214">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="18a50-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="18a50-215">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="18a50-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="18a50-217">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="18a50-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="18a50-218">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="18a50-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18a50-220">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="18a50-220">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="18a50-222">Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="18a50-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18a50-224">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="18a50-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18a50-226">a.</span><span class="sxs-lookup"><span data-stu-id="18a50-226">a.</span></span> <span data-ttu-id="18a50-227">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18a50-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18a50-228">b.</span><span class="sxs-lookup"><span data-stu-id="18a50-228">b.</span></span> <span data-ttu-id="18a50-229">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="18a50-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="18a50-230">c.</span><span class="sxs-lookup"><span data-stu-id="18a50-230">c.</span></span> <span data-ttu-id="18a50-231">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="18a50-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="18a50-232">d.</span><span class="sxs-lookup"><span data-stu-id="18a50-232">d.</span></span> <span data-ttu-id="18a50-233">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="18a50-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="18a50-234">Criando um usuário de teste do ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="18a50-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="18a50-235">tooenable AD do Azure usuários toolog em tooScaleX Enterprise, eles devem ser provisionados no tooScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="18a50-235">tooenable Azure AD users toolog in tooScaleX Enterprise, they must be provisioned in tooScaleX Enterprise.</span></span> <span data-ttu-id="18a50-236">No caso de saudação do ScaleX Enterprise, o provisionamento é uma tarefa automática e nenhuma etapa manual é necessária.</span><span class="sxs-lookup"><span data-stu-id="18a50-236">In hello case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="18a50-237">Qualquer usuário que pode autenticar com credenciais de SSO será configurado automaticamente Olá ScaleX lado.</span><span class="sxs-lookup"><span data-stu-id="18a50-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on hello ScaleX side.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="18a50-238">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="18a50-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="18a50-239">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure concedendo Enterprise de tooScaleX de acesso do usuário.</span><span class="sxs-lookup"><span data-stu-id="18a50-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting user access tooScaleX Enterprise.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="18a50-241">**tooassign Britta Simon tooScaleX Enterprise, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="18a50-241">**tooassign Britta Simon tooScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="18a50-242">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="18a50-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="18a50-244">Na lista de aplicativos hello, selecione **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="18a50-244">In hello applications list, select **ScaleX Enterprise**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="18a50-246">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="18a50-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="18a50-248">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="18a50-248">Click **Add** button.</span></span> <span data-ttu-id="18a50-249">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="18a50-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="18a50-251">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="18a50-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="18a50-252">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="18a50-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18a50-253">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="18a50-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="18a50-254">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="18a50-254">Testing single sign-on</span></span>

<span data-ttu-id="18a50-255">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="18a50-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="18a50-256">Clique em Olá ScaleX Enterprise lado a lado no hello painel de acesso, você receberá automaticamente assinado em tooyour aplicativo empresarial ScaleX.</span><span class="sxs-lookup"><span data-stu-id="18a50-256">Click hello ScaleX Enterprise tile in hello Access Panel, you will get automatically signed-on tooyour ScaleX Enterprise application.</span></span> <span data-ttu-id="18a50-257">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="18a50-257">For more information about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="18a50-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="18a50-258">Additional resources</span></span>

* [<span data-ttu-id="18a50-259">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="18a50-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18a50-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="18a50-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

