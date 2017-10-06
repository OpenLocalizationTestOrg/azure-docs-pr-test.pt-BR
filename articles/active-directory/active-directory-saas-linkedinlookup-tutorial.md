---
title: "Tutorial: Integração do Azure Active Directory ao LinkedIn Lookup | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e pesquisa LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="80c3b-103">Tutorial: Integração do Azure Active Directory ao LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="80c3b-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="80c3b-104">Neste tutorial, você aprenderá como toointegrate pesquisa LinkedIn com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="80c3b-104">In this tutorial, you learn how toointegrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="80c3b-105">Integração de pesquisa do LinkedIn com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="80c3b-105">Integrating LinkedIn Lookup with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="80c3b-106">Você pode controlar no AD do Azure que tenha acesso tooLinkedIn pesquisa</span><span class="sxs-lookup"><span data-stu-id="80c3b-106">You can control in Azure AD who has access tooLinkedIn Lookup</span></span>
- <span data-ttu-id="80c3b-107">Você pode habilitar seu usuários tooautomatically get conectado tooLinkedIn pesquisa (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80c3b-107">You can enable your users tooautomatically get signed-on tooLinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="80c3b-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="80c3b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="80c3b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80c3b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80c3b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="80c3b-110">Prerequisites</span></span>

<span data-ttu-id="80c3b-111">tooconfigure integração do AD do Azure com pesquisa LinkedIn, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="80c3b-111">tooconfigure Azure AD integration with LinkedIn Lookup, you need hello following items:</span></span>

- <span data-ttu-id="80c3b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80c3b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="80c3b-113">Uma assinatura habilitada para logon único do LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="80c3b-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="80c3b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="80c3b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="80c3b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="80c3b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="80c3b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="80c3b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="80c3b-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="80c3b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="80c3b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="80c3b-118">Scenario description</span></span>
<span data-ttu-id="80c3b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="80c3b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="80c3b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="80c3b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="80c3b-121">Adicionando LinkedIn pesquisa da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="80c3b-121">Adding LinkedIn Lookup from hello gallery</span></span>
2. <span data-ttu-id="80c3b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80c3b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-hello-gallery"></a><span data-ttu-id="80c3b-123">Adicionando LinkedIn pesquisa da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="80c3b-123">Adding LinkedIn Lookup from hello gallery</span></span>
<span data-ttu-id="80c3b-124">integração de saudação tooconfigure da pesquisa do LinkedIn no AD do Azure, você precisa tooadd LinkedIn pesquisa na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="80c3b-124">tooconfigure hello integration of LinkedIn Lookup into Azure AD, you need tooadd LinkedIn Lookup from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="80c3b-125">**tooadd LinkedIn pesquisa da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="80c3b-125">**tooadd LinkedIn Lookup from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="80c3b-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="80c3b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="80c3b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="80c3b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="80c3b-131">Clique em **novo aplicativo** botão na parte superior de saudação do novo aplicativo do hello diálogo tooadd.</span><span class="sxs-lookup"><span data-stu-id="80c3b-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="80c3b-133">Na caixa de pesquisa hello, digite **LinkedIn pesquisa**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-133">In hello search box, type **LinkedIn Lookup**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="80c3b-135">No painel de resultados de saudação, selecione **LinkedIn pesquisa**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="80c3b-135">In hello results panel, select **LinkedIn Lookup**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="80c3b-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80c3b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="80c3b-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o LinkedIn Lookup, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="80c3b-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="80c3b-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na pesquisa do LinkedIn é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="80c3b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Lookup is tooa user in Azure AD.</span></span> <span data-ttu-id="80c3b-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na pesquisa do LinkedIn precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="80c3b-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Lookup needs toobe established.</span></span>

<span data-ttu-id="80c3b-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** na pesquisa do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="80c3b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="80c3b-142">tooconfigure e teste de logon único do AD do Azure com pesquisa LinkedIn, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="80c3b-142">tooconfigure and test Azure AD single sign-on with LinkedIn Lookup, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="80c3b-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="80c3b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="80c3b-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80c3b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="80c3b-145">**[Criar um usuário de teste de pesquisa LinkedIn](#creating-an-linkedin-lookup-test-user)**  -toohave um equivalente do Britta Simon na pesquisa LinkedIn que é a representação toohello vinculado do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80c3b-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Lookup that is linked toohello Azure AD representation.</span></span>
4. <span data-ttu-id="80c3b-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="80c3b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="80c3b-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="80c3b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="80c3b-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="80c3b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="80c3b-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de pesquisa do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="80c3b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="80c3b-150">**tooconfigure AD do Azure-logon único com pesquisa LinkedIn, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="80c3b-150">**tooconfigure Azure AD single sign-on with LinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="80c3b-151">Em Olá portal do Azure, Olá **LinkedIn pesquisa** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-151">In hello Azure portal, on hello **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="80c3b-153">Em Olá **o logon único** caixa de diálogo, na **modo** selecione **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="80c3b-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="80c3b-155">Em uma janela de navegador web diferente, o logon tooyour **LinkedIn pesquisa** site como um administrador.</span><span class="sxs-lookup"><span data-stu-id="80c3b-155">In a different web browser window, sign-on tooyour **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="80c3b-156">Em **Centro de Contas**, clique em **Configurações Globais** em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="80c3b-157">Além disso, selecione **pesquisa** na lista suspensa hello.</span><span class="sxs-lookup"><span data-stu-id="80c3b-157">Also, select **Lookup** from hello dropdown list.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="80c3b-159">Clique em **ou clique aqui tooload e copiar campos individuais de um formulário de saudação** e cópia **Id da entidade** e **Url do consumidor de declaração acesso (ACS)**</span><span class="sxs-lookup"><span data-stu-id="80c3b-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="80c3b-161">No portal do Azure, em **LinkedIn pesquisa domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="80c3b-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="80c3b-163">a.</span><span class="sxs-lookup"><span data-stu-id="80c3b-163">a.</span></span> <span data-ttu-id="80c3b-164">Em Olá **identificador** caixa de texto, digite Olá **ID da entidade** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="80c3b-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="80c3b-165">b.</span><span class="sxs-lookup"><span data-stu-id="80c3b-165">b.</span></span> <span data-ttu-id="80c3b-166">Em Olá **URL de resposta** caixa de texto, digite Olá **Url do consumidor de declaração acesso (ACS)** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="80c3b-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="80c3b-167">Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="80c3b-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="80c3b-169">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="80c3b-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="80c3b-170">Isso não é um valor real.</span><span class="sxs-lookup"><span data-stu-id="80c3b-170">This is not real value.</span></span> <span data-ttu-id="80c3b-171">usuário Olá tem tooupdate esses valores com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="80c3b-171">hello user has tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="80c3b-172">Entre em contato com [equipe de suporte do cliente do LinkedIn pesquisa](https://business.LinkedIn.com/lookup) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="80c3b-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) tooget this value.</span></span>

8. <span data-ttu-id="80c3b-173">O **LinkedIn pesquisa** aplicativo espera as asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="80c3b-173">Your **LinkedIn Lookup** application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="80c3b-174">usuário Olá tem uma configuração de atributos de token SAML do toohello de mapeamentos de atributo personalizado tooadd.</span><span class="sxs-lookup"><span data-stu-id="80c3b-174">hello user has tooadd custom attribute mappings toohello SAML token attributes configuration.</span></span> <span data-ttu-id="80c3b-175">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="80c3b-175">hello following screenshot shows an example.</span></span> <span data-ttu-id="80c3b-176">Olá valor padrão de **identificador de usuário** é **User** mas pesquisa LinkedIn espera este toobe mapeada com o endereço de email do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="80c3b-176">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="80c3b-177">Você pode usar **user.mail** de atributo na lista de saudação ou usar o valor do atributo apropriado Olá com base na configuração de sua organização.</span><span class="sxs-lookup"><span data-stu-id="80c3b-177">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="80c3b-179">Em **atributos de usuário** seção, clique em **exibir e editar todos os outros atributos de usuário** e definir atributos de saudação.</span><span class="sxs-lookup"><span data-stu-id="80c3b-179">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="80c3b-180">usuário Olá precisa tooadd quatro declarações denominadas **email**, **departamento**, **firstname**, e **lastname** e valor de saudação é toobe mapeada com **user.mail**, **User. Department**, **user.givenname**, e **user.surname** respectivamente</span><span class="sxs-lookup"><span data-stu-id="80c3b-180">hello user needs tooadd four claims named **email**,  **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="80c3b-181">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="80c3b-181">Attribute Name</span></span> | <span data-ttu-id="80c3b-182">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="80c3b-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="80c3b-183">email</span><span class="sxs-lookup"><span data-stu-id="80c3b-183">email</span></span>| <span data-ttu-id="80c3b-184">user.mail</span><span class="sxs-lookup"><span data-stu-id="80c3b-184">user.mail</span></span> |    
    | <span data-ttu-id="80c3b-185">department</span><span class="sxs-lookup"><span data-stu-id="80c3b-185">department</span></span>| <span data-ttu-id="80c3b-186">user.department</span><span class="sxs-lookup"><span data-stu-id="80c3b-186">user.department</span></span> |
    | <span data-ttu-id="80c3b-187">nome</span><span class="sxs-lookup"><span data-stu-id="80c3b-187">firstname</span></span>| <span data-ttu-id="80c3b-188">user.givenname</span><span class="sxs-lookup"><span data-stu-id="80c3b-188">user.givenname</span></span> |
    | <span data-ttu-id="80c3b-189">sobrenome</span><span class="sxs-lookup"><span data-stu-id="80c3b-189">lastname</span></span>| <span data-ttu-id="80c3b-190">user.surname</span><span class="sxs-lookup"><span data-stu-id="80c3b-190">user.surname</span></span> |

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="80c3b-192">a.</span><span class="sxs-lookup"><span data-stu-id="80c3b-192">a.</span></span> <span data-ttu-id="80c3b-193">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80c3b-193">Click **Add Attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="80c3b-196">b.</span><span class="sxs-lookup"><span data-stu-id="80c3b-196">b.</span></span> <span data-ttu-id="80c3b-197">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="80c3b-197">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="80c3b-198">c.</span><span class="sxs-lookup"><span data-stu-id="80c3b-198">c.</span></span> <span data-ttu-id="80c3b-199">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="80c3b-199">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="80c3b-200">d.</span><span class="sxs-lookup"><span data-stu-id="80c3b-200">d.</span></span> <span data-ttu-id="80c3b-201">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="80c3b-201">Click **Ok**</span></span>

10. <span data-ttu-id="80c3b-202">Executar Olá seguindo as etapas na Olá **nome** atributo -</span><span class="sxs-lookup"><span data-stu-id="80c3b-202">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="80c3b-203">a.</span><span class="sxs-lookup"><span data-stu-id="80c3b-203">a.</span></span> <span data-ttu-id="80c3b-204">Clique em saudação do hello atributo tooopen **Editar atributo** janela.</span><span class="sxs-lookup"><span data-stu-id="80c3b-204">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="80c3b-206">b.</span><span class="sxs-lookup"><span data-stu-id="80c3b-206">b.</span></span> <span data-ttu-id="80c3b-207">Excluir o valor da URL de saudação da saudação **namespace**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-207">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="80c3b-208">c.</span><span class="sxs-lookup"><span data-stu-id="80c3b-208">c.</span></span> <span data-ttu-id="80c3b-209">Clique em **Okey** toosave configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="80c3b-209">Click **Ok** toosave hello setting.</span></span>

10. <span data-ttu-id="80c3b-210">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="80c3b-210">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="80c3b-212">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="80c3b-212">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="80c3b-214">Vá muito**as configurações de administração do LinkedIn** seção.</span><span class="sxs-lookup"><span data-stu-id="80c3b-214">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="80c3b-215">Carregue o arquivo de XML de saudação baixado do hello portal do Azure clicando Olá **arquivo carregar XML** opção.</span><span class="sxs-lookup"><span data-stu-id="80c3b-215">Upload hello XML file you downloaded from hello Azure portal by clicking hello **Upload XML file** option.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="80c3b-217">Clique em **na** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="80c3b-217">Click **On** tooenable SSO.</span></span> <span data-ttu-id="80c3b-218">Status SSO é alterado de **não conectado** muito**conectado**</span><span class="sxs-lookup"><span data-stu-id="80c3b-218">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="80c3b-220">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="80c3b-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="80c3b-221">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="80c3b-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="80c3b-222">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="80c3b-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="80c3b-223">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80c3b-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="80c3b-224">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="80c3b-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="80c3b-226">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="80c3b-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="80c3b-227">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="80c3b-227">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="80c3b-229">Vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-229">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="80c3b-231">Clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80c3b-231">Click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="80c3b-233">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="80c3b-233">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="80c3b-235">a.</span><span class="sxs-lookup"><span data-stu-id="80c3b-235">a.</span></span> <span data-ttu-id="80c3b-236">Em Olá **nome** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-236">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="80c3b-237">b.</span><span class="sxs-lookup"><span data-stu-id="80c3b-237">b.</span></span> <span data-ttu-id="80c3b-238">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80c3b-238">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="80c3b-239">c.</span><span class="sxs-lookup"><span data-stu-id="80c3b-239">c.</span></span> <span data-ttu-id="80c3b-240">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-240">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="80c3b-241">d.</span><span class="sxs-lookup"><span data-stu-id="80c3b-241">d.</span></span> <span data-ttu-id="80c3b-242">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="80c3b-243">Criação de um usuário de teste do LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="80c3b-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="80c3b-244">Aplicativo de pesquisa vinculado oferece suporte a apenas em Time (JIT) de provisionamento de usuário e depois que os usuários de autenticação são criados automaticamente no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="80c3b-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="80c3b-245">Ativar **automaticamente atribuir licenças** tooassign um usuário de toohello de licença.</span><span class="sxs-lookup"><span data-stu-id="80c3b-245">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="80c3b-247">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80c3b-247">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="80c3b-248">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLinkedIn pesquisa.</span><span class="sxs-lookup"><span data-stu-id="80c3b-248">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Lookup.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="80c3b-250">**tooassign Britta Simon tooLinkedIn pesquisa, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="80c3b-250">**tooassign Britta Simon tooLinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="80c3b-251">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-251">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="80c3b-253">Na lista de aplicativos hello, selecione **LinkedIn pesquisa**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-253">In hello applications list, select **LinkedIn Lookup**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="80c3b-255">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-255">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="80c3b-257">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="80c3b-257">Click **Add** button.</span></span> <span data-ttu-id="80c3b-258">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80c3b-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="80c3b-260">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="80c3b-260">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="80c3b-261">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80c3b-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="80c3b-262">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80c3b-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="80c3b-263">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="80c3b-263">Testing single sign-on</span></span>

<span data-ttu-id="80c3b-264">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="80c3b-264">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="80c3b-265">Quando você clica em Olá LinkedIn pesquisa bloco no painel de acesso de saudação, você deve ser redirecionado tooOrganizational página onde você tem tooprovide os detalhes da conta pessoais LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="80c3b-265">When you click hello LinkedIn Lookup tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="80c3b-266">Ele vincula a sua conta pessoal à sua conta de negócios do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="80c3b-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="80c3b-267">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="80c3b-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="80c3b-268">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="80c3b-268">Additional resources</span></span>

* [<span data-ttu-id="80c3b-269">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="80c3b-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80c3b-270">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="80c3b-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

