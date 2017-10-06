---
title: "Tutorial: integração do Azure Active Directory ao LinkedInSalesNavigator | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e LinkedInSalesNavigator."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 443d302d40d7af16aba5114e00963f23ea8d12d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="62bc5-103">Tutorial: integração do Azure Active Directory com o LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="62bc5-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="62bc5-104">Neste tutorial, você aprenderá como toointegrate LinkedIn vendas navegador com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="62bc5-104">In this tutorial, you learn how toointegrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62bc5-105">Integrando LinkedIn vendas navegador com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="62bc5-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="62bc5-106">Você pode controlar no AD do Azure que tenha acesso tooLinkedIn navegador de vendas</span><span class="sxs-lookup"><span data-stu-id="62bc5-106">You can control in Azure AD who has access tooLinkedIn Sales Navigator</span></span>
- <span data-ttu-id="62bc5-107">Você pode habilitar seu usuários tooautomatically get conectado tooLinkedIn navegador de vendas (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62bc5-107">You can enable your users tooautomatically get signed-on tooLinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62bc5-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="62bc5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="62bc5-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o Azure AD, procurar [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62bc5-109">If you want tooknow more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62bc5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="62bc5-110">Prerequisites</span></span>

<span data-ttu-id="62bc5-111">tooconfigure integração do AD do Azure com o navegador de vendas LinkedIn, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="62bc5-111">tooconfigure Azure AD integration with LinkedIn Sales Navigator, you need hello following items:</span></span>

- <span data-ttu-id="62bc5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62bc5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62bc5-113">Uma assinatura do LinkedIn Sales Navigator com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="62bc5-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62bc5-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="62bc5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62bc5-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="62bc5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62bc5-116">Evite usar o ambiente de produção a menos que necessário.</span><span class="sxs-lookup"><span data-stu-id="62bc5-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="62bc5-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62bc5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62bc5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="62bc5-118">Scenario description</span></span>
<span data-ttu-id="62bc5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="62bc5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62bc5-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="62bc5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62bc5-121">Adicionando LinkedIn vendas navegador da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="62bc5-121">Adding LinkedIn Sales Navigator from hello gallery</span></span>
2. <span data-ttu-id="62bc5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62bc5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-hello-gallery"></a><span data-ttu-id="62bc5-123">Adicionando LinkedIn vendas navegador da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="62bc5-123">Adding LinkedIn Sales Navigator from hello gallery</span></span>
<span data-ttu-id="62bc5-124">integração de saudação tooconfigure do navegador de vendas LinkedIn no AD do Azure, você precisa tooadd LinkedIn vendas navegador na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="62bc5-124">tooconfigure hello integration of LinkedIn Sales Navigator into Azure AD, you need tooadd LinkedIn Sales Navigator from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="62bc5-125">**tooadd LinkedIn navegador de vendas da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="62bc5-125">**tooadd LinkedIn Sales Navigator from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="62bc5-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="62bc5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62bc5-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="62bc5-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="62bc5-131">Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="62bc5-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="62bc5-133">Na caixa de pesquisa hello, digite **LinkedIn vendas navegador**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-133">In hello search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="62bc5-135">No painel de resultados de saudação, selecione **LinkedIn vendas navegador**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="62bc5-135">In hello results panel, select **LinkedIn Sales Navigator**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62bc5-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62bc5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62bc5-138">Nesta seção, você configurará e testará o logon único do Azure AD com o LinkedIn Sales Navigator, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="62bc5-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62bc5-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no navegador de vendas LinkedIn é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="62bc5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Sales Navigator is tooa user in Azure AD.</span></span> <span data-ttu-id="62bc5-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no navegador de vendas LinkedIn precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="62bc5-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Sales Navigator needs toobe established.</span></span>

<span data-ttu-id="62bc5-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no navegador de vendas do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="62bc5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="62bc5-142">tooconfigure e teste de logon único do AD do Azure com o navegador de vendas LinkedIn, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="62bc5-142">tooconfigure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="62bc5-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="62bc5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="62bc5-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62bc5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62bc5-145">**[Criar um usuário de teste do navegador de vendas LinkedIn](#creating-a-linkedin-sales-navigator-test-user)**  -toohave um equivalente do Britta Simon no navegador de vendas LinkedIn que é vinculado toohello AD do Azure representação do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="62bc5-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="62bc5-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="62bc5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62bc5-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="62bc5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62bc5-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="62bc5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62bc5-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de navegador de vendas do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="62bc5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="62bc5-150">**tooconfigure logon único do AD do Azure com o navegador de vendas LinkedIn, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="62bc5-150">**tooconfigure Azure AD single sign-on with LinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="62bc5-151">Em Olá portal do Azure, Olá **LinkedIn vendas navegador** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-151">In hello Azure portal, on hello **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="62bc5-153">Em Olá **o logon único** caixa de diálogo, na **modo** selecione **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="62bc5-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="62bc5-155">Em uma janela de navegador web diferente, o logon tooyour **LinkedIn vendas navegador** site como um administrador.</span><span class="sxs-lookup"><span data-stu-id="62bc5-155">In a different web browser window, sign-on tooyour **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="62bc5-156">Em **Centro de Contas**, clique em **Configurações Globais** em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="62bc5-157">Além disso, selecione **vendas navegador** na lista suspensa hello.</span><span class="sxs-lookup"><span data-stu-id="62bc5-157">Also, select **Sales Navigator** from hello dropdown list.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="62bc5-159">Clique em **ou clique aqui tooload e copiar campos individuais de um formulário de saudação** e cópia **Id da entidade** e **Url do consumidor de declaração acesso (ACS)**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="62bc5-161">No portal do Azure, em **LinkedIn vendas navegador de domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado.</span><span class="sxs-lookup"><span data-stu-id="62bc5-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="62bc5-163">a.</span><span class="sxs-lookup"><span data-stu-id="62bc5-163">a.</span></span> <span data-ttu-id="62bc5-164">Em Olá **identificador** caixa de texto, digite Olá **ID da entidade** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="62bc5-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="62bc5-165">b.</span><span class="sxs-lookup"><span data-stu-id="62bc5-165">b.</span></span> <span data-ttu-id="62bc5-166">Em Olá **URL de resposta** caixa de texto, digite Olá **Url do consumidor de declaração acesso (ACS)** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="62bc5-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="62bc5-167">Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado.</span><span class="sxs-lookup"><span data-stu-id="62bc5-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="62bc5-169">Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="62bc5-169">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="62bc5-170">O **LinkedIn vendas navegador** aplicativo espera asserções SAML de saudação em um formato específico, o que exige que a configuração de atributos de token SAML do tooyour de mapeamentos de atributo personalizado tooadd.</span><span class="sxs-lookup"><span data-stu-id="62bc5-170">Your **LinkedIn Sales Navigator** application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="62bc5-171">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="62bc5-171">hello following screenshot shows an example.</span></span> <span data-ttu-id="62bc5-172">Olá valor padrão de **identificador de usuário** é **User** mas LinkedIn vendas navegador espera toobe mapeada com o endereço de email do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="62bc5-172">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it toobe mapped with hello user's email address.</span></span> <span data-ttu-id="62bc5-173">Você pode usar **user.mail** de atributo na lista de saudação ou usar o valor do atributo apropriado Olá com base na configuração de sua organização.</span><span class="sxs-lookup"><span data-stu-id="62bc5-173">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="62bc5-175">Em **atributos de usuário** seção, clique em **exibir e editar todos os outros atributos de usuário** e definir atributos de saudação.</span><span class="sxs-lookup"><span data-stu-id="62bc5-175">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="62bc5-176">usuário Olá precisa tooadd quatro declarações denominadas **email**, **departamento**, **firstname**, e **lastname** e valor de saudação é toobe mapeada com **user.mail**, **User. Department**, **user.givenname**, e **user.surname** respectivamente</span><span class="sxs-lookup"><span data-stu-id="62bc5-176">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="62bc5-177">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="62bc5-177">Attribute Name</span></span> | <span data-ttu-id="62bc5-178">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="62bc5-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="62bc5-179">email</span><span class="sxs-lookup"><span data-stu-id="62bc5-179">email</span></span>| <span data-ttu-id="62bc5-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="62bc5-180">user.mail</span></span> |
    | <span data-ttu-id="62bc5-181">department</span><span class="sxs-lookup"><span data-stu-id="62bc5-181">department</span></span>| <span data-ttu-id="62bc5-182">user.department</span><span class="sxs-lookup"><span data-stu-id="62bc5-182">user.department</span></span> |
    | <span data-ttu-id="62bc5-183">nome</span><span class="sxs-lookup"><span data-stu-id="62bc5-183">firstname</span></span>| <span data-ttu-id="62bc5-184">user.givenname</span><span class="sxs-lookup"><span data-stu-id="62bc5-184">user.givenname</span></span> |
    | <span data-ttu-id="62bc5-185">sobrenome</span><span class="sxs-lookup"><span data-stu-id="62bc5-185">lastname</span></span>| <span data-ttu-id="62bc5-186">user.surname</span><span class="sxs-lookup"><span data-stu-id="62bc5-186">user.surname</span></span> |
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="62bc5-188">a.</span><span class="sxs-lookup"><span data-stu-id="62bc5-188">a.</span></span> <span data-ttu-id="62bc5-189">Clique em **Adicionar atributo** caixa de diálogo do atributo tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="62bc5-189">Click on **Add Attribute** tooopen hello attribute dialog.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="62bc5-192">b.</span><span class="sxs-lookup"><span data-stu-id="62bc5-192">b.</span></span> <span data-ttu-id="62bc5-193">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="62bc5-193">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="62bc5-194">c.</span><span class="sxs-lookup"><span data-stu-id="62bc5-194">c.</span></span> <span data-ttu-id="62bc5-195">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="62bc5-195">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="62bc5-196">d.</span><span class="sxs-lookup"><span data-stu-id="62bc5-196">d.</span></span> <span data-ttu-id="62bc5-197">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="62bc5-197">Click **Ok**</span></span>

10. <span data-ttu-id="62bc5-198">Executar Olá seguindo as etapas na Olá **nome** atributo -</span><span class="sxs-lookup"><span data-stu-id="62bc5-198">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="62bc5-199">a.</span><span class="sxs-lookup"><span data-stu-id="62bc5-199">a.</span></span> <span data-ttu-id="62bc5-200">Clique em saudação do hello atributo tooopen **Editar atributo** janela.</span><span class="sxs-lookup"><span data-stu-id="62bc5-200">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="62bc5-202">b.</span><span class="sxs-lookup"><span data-stu-id="62bc5-202">b.</span></span> <span data-ttu-id="62bc5-203">Excluir o valor da URL de saudação da saudação **namespace**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-203">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="62bc5-204">c.</span><span class="sxs-lookup"><span data-stu-id="62bc5-204">c.</span></span> <span data-ttu-id="62bc5-205">Clique em **Okey** toosave configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="62bc5-205">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="62bc5-206">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="62bc5-206">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="62bc5-208">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="62bc5-208">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="62bc5-210">Vá muito**as configurações de administração do LinkedIn** seção.</span><span class="sxs-lookup"><span data-stu-id="62bc5-210">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="62bc5-211">Clique em **arquivo carregar XML** Olá tooupload arquivo Metadata XML que você baixou do portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="62bc5-211">Click **Upload XML file** tooupload hello Metadata XML file that you have downloaded from hello Azure portal.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="62bc5-213">Clique em **na** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="62bc5-213">Click **On** tooenable SSO.</span></span> <span data-ttu-id="62bc5-214">Status SSO é alterado de **não conectado** muito**conectado**</span><span class="sxs-lookup"><span data-stu-id="62bc5-214">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="62bc5-216">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="62bc5-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="62bc5-217">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="62bc5-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="62bc5-218">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="62bc5-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62bc5-219">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62bc5-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="62bc5-220">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="62bc5-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="62bc5-222">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="62bc5-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="62bc5-223">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="62bc5-223">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62bc5-225">Vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-225">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62bc5-227">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62bc5-227">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62bc5-229">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="62bc5-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62bc5-231">a.</span><span class="sxs-lookup"><span data-stu-id="62bc5-231">a.</span></span> <span data-ttu-id="62bc5-232">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62bc5-233">b.</span><span class="sxs-lookup"><span data-stu-id="62bc5-233">b.</span></span> <span data-ttu-id="62bc5-234">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="62bc5-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62bc5-235">c.</span><span class="sxs-lookup"><span data-stu-id="62bc5-235">c.</span></span> <span data-ttu-id="62bc5-236">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="62bc5-237">d.</span><span class="sxs-lookup"><span data-stu-id="62bc5-237">d.</span></span> <span data-ttu-id="62bc5-238">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="62bc5-239">Criar um usuário de teste do LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="62bc5-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="62bc5-240">Aplicativo de navegador de vendas vinculado dá suporte apenas em Time (JIT) de provisionamento de usuário e depois que os usuários de autenticação são criados automaticamente no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="62bc5-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="62bc5-241">Ativar **automaticamente atribuir licenças** tooassign um usuário de toohello de licença.</span><span class="sxs-lookup"><span data-stu-id="62bc5-241">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="62bc5-243">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62bc5-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="62bc5-244">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLinkedIn navegador de vendas.</span><span class="sxs-lookup"><span data-stu-id="62bc5-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Sales Navigator.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="62bc5-246">**tooassign Britta Simon tooLinkedIn navegador de vendas, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="62bc5-246">**tooassign Britta Simon tooLinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="62bc5-247">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="62bc5-249">Na lista de aplicativos hello, selecione **LinkedIn vendas navegador**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-249">In hello applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="62bc5-251">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="62bc5-253">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="62bc5-253">Click **Add** button.</span></span> <span data-ttu-id="62bc5-254">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62bc5-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="62bc5-256">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="62bc5-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="62bc5-257">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62bc5-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62bc5-258">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62bc5-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="62bc5-259">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="62bc5-259">Testing single sign-on</span></span>

<span data-ttu-id="62bc5-260">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="62bc5-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="62bc5-261">Quando você clica em bloco LinkedIn vendas navegador Olá Olá painel de acesso, você deve ser redirecionado tooOrganizational página onde você tem tooprovide os detalhes da conta pessoais LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="62bc5-261">When you click hello LinkedIn Sales Navigator tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="62bc5-262">Ele vincula a sua conta pessoal à sua conta de negócios do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="62bc5-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="62bc5-263">Para obter mais informações sobre Olá painel de acesso, consulte [Introdução ao painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="62bc5-263">For more information about hello Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="62bc5-264">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="62bc5-264">Additional resources</span></span>

* [<span data-ttu-id="62bc5-265">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="62bc5-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62bc5-266">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="62bc5-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

