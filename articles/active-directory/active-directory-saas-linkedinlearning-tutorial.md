---
title: "Tutorial: integração do Azure Active Directory com o LinkedIn Learning | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e aprendizado LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="f5fa6-103">Tutorial: integração do Azure Active Directory com o LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="f5fa6-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="f5fa6-104">Neste tutorial, você aprenderá como toointegrate LinkedIn aprendizado com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f5fa6-104">In this tutorial, you learn how toointegrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5fa6-105">Integração de aprendizado do LinkedIn com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="f5fa6-105">Integrating LinkedIn Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f5fa6-106">Você pode controlar no AD do Azure que tenha acesso tooLinkedIn de aprendizado</span><span class="sxs-lookup"><span data-stu-id="f5fa6-106">You can control in Azure AD who has access tooLinkedIn Learning</span></span>
- <span data-ttu-id="f5fa6-107">Você pode habilitar seu usuários tooautomatically get conectado tooLinkedIn aprendizado (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f5fa6-107">You can enable your users tooautomatically get signed-on tooLinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5fa6-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f5fa6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f5fa6-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f5fa6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5fa6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f5fa6-110">Prerequisites</span></span>

<span data-ttu-id="f5fa6-111">tooconfigure integração do AD do Azure com o aprendizado LinkedIn, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f5fa6-111">tooconfigure Azure AD integration with LinkedIn Learning, you need hello following items:</span></span>

- <span data-ttu-id="f5fa6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f5fa6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5fa6-113">Uma assinatura do LinkedIn Learning habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="f5fa6-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5fa6-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5fa6-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f5fa6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5fa6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f5fa6-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5fa6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5fa6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f5fa6-118">Scenario description</span></span>
<span data-ttu-id="f5fa6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f5fa6-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="f5fa6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5fa6-121">Adicionando LinkedIn aprendizado da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f5fa6-121">Adding LinkedIn Learning from hello gallery</span></span>
2. <span data-ttu-id="f5fa6-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f5fa6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-hello-gallery"></a><span data-ttu-id="f5fa6-123">Adicionando LinkedIn aprendizado da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f5fa6-123">Adding LinkedIn Learning from hello gallery</span></span>
<span data-ttu-id="f5fa6-124">integração de saudação tooconfigure do LinkedIn aprendizado no AD do Azure, você precisa tooadd LinkedIn aprendizado da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-124">tooconfigure hello integration of LinkedIn Learning into Azure AD, you need tooadd LinkedIn Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f5fa6-125">**tooadd LinkedIn aprendizado da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f5fa6-125">**tooadd LinkedIn Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5fa6-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f5fa6-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f5fa6-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f5fa6-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f5fa6-133">Na caixa de pesquisa hello, digite **LinkedIn aprendizado**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-133">In hello search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="f5fa6-134">No painel de resultados, clique em **LinkedIn aprendizado** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-134">From results panel, click **LinkedIn Learning** tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5fa6-136">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f5fa6-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5fa6-137">Nesta seção, você configurará e testará o logon único do Azure AD com o LinkedIn Learning, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="f5fa6-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f5fa6-138">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no aprendizado LinkedIn é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="f5fa6-139">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no aprendizado LinkedIn precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Learning needs toobe established.</span></span>

<span data-ttu-id="f5fa6-140">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no aprendizado LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="f5fa6-141">tooconfigure e teste de logon único do AD do Azure com o aprendizado LinkedIn, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="f5fa6-141">tooconfigure and test Azure AD single sign-on with LinkedIn Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f5fa6-142">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f5fa6-143">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5fa6-144">**[Criar um usuário de teste de aprendizado LinkedIn](#creating-a-linkedin-learning-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="f5fa6-145">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5fa6-146">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5fa6-147">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5fa6-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f5fa6-148">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de aprendizado do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="f5fa6-149">**tooconfigure AD do Azure-logon único com o aprendizado LinkedIn, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f5fa6-149">**tooconfigure Azure AD single sign-on with LinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5fa6-150">Em Olá portal do Azure, Olá **LinkedIn aprendizado** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-150">In hello Azure portal, on hello **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f5fa6-152">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="f5fa6-154">Em uma janela de navegador web diferente, locatário de aprendizado LinkedIn tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-154">In a different web browser window, sign-on tooyour LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="f5fa6-155">Em **Centro de Contas**, clique em **Configurações Globais** em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="f5fa6-156">Além disso, selecione **aprendizado - padrão** na lista suspensa hello.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-156">Also, select **Learning - Default** from hello dropdown list.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="f5fa6-158">Clique em **ou clique aqui tooload e copiar campos individuais de um formulário de saudação** e cópia **Id da entidade** e **Url do consumidor de declaração acesso (ACS)**</span><span class="sxs-lookup"><span data-stu-id="f5fa6-158">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="f5fa6-160">No portal do Azure, em **LinkedIn aprendizado de domínio e URLs**, executar Olá etapas a seguir se você quiser tooconfigure SSO em **iniciado pelo IdP** modo</span><span class="sxs-lookup"><span data-stu-id="f5fa6-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="f5fa6-162">a.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-162">a.</span></span> <span data-ttu-id="f5fa6-163">Em Olá **identificador** caixa de texto, digite Olá **ID da entidade** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="f5fa6-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="f5fa6-164">b.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-164">b.</span></span> <span data-ttu-id="f5fa6-165">Em Olá **URL de resposta** caixa de texto, digite Olá **Url do consumidor de declaração acesso (ACS)** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="f5fa6-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="f5fa6-166">Se você quiser tooconfigure SSO em **iniciado pelo SP**, clique em Mostrar avançado URL opção de configuração na seção de configuração hello e configurar a URL de entrada hello com saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="f5fa6-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign-on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="f5fa6-168">Seu aplicativo de aprendizado LinkedIn espera asserções SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-168">Your LinkedIn Learning application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="f5fa6-169">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="f5fa6-170">Olá valor padrão de **identificador de usuário** é **User** mas LinkedIn aprendizado espera este toobe mapeada com o endereço de email do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="f5fa6-171">Para que você pode usar **user.mail** de atributo na lista de saudação ou usar o valor do atributo apropriado Olá com base na configuração de sua organização.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="f5fa6-173">Em **atributos de usuário** seção, clique em **exibir e editar todos os outros atributos de usuário** e definir atributos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="f5fa6-174">usuário Olá precisa tooadd quatro declarações denominadas **email**, **departamento**, **firstname**, e **lastname** e valor de saudação é toobe mapeada com **user.mail**, **User. Department**, **user.givenname**, e **user.surname** respectivamente</span><span class="sxs-lookup"><span data-stu-id="f5fa6-174">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="f5fa6-175">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="f5fa6-175">Attribute Name</span></span> | <span data-ttu-id="f5fa6-176">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="f5fa6-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="f5fa6-177">email</span><span class="sxs-lookup"><span data-stu-id="f5fa6-177">email</span></span>| <span data-ttu-id="f5fa6-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="f5fa6-178">user.mail</span></span> |    
    | <span data-ttu-id="f5fa6-179">department</span><span class="sxs-lookup"><span data-stu-id="f5fa6-179">department</span></span>| <span data-ttu-id="f5fa6-180">user.department</span><span class="sxs-lookup"><span data-stu-id="f5fa6-180">user.department</span></span> |
    | <span data-ttu-id="f5fa6-181">nome</span><span class="sxs-lookup"><span data-stu-id="f5fa6-181">firstname</span></span>| <span data-ttu-id="f5fa6-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="f5fa6-182">user.givenname</span></span> |
    | <span data-ttu-id="f5fa6-183">sobrenome</span><span class="sxs-lookup"><span data-stu-id="f5fa6-183">lastname</span></span>| <span data-ttu-id="f5fa6-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="f5fa6-184">user.surname</span></span> |
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="f5fa6-186">a.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-186">a.</span></span> <span data-ttu-id="f5fa6-187">Clique em **Adicionar atributo** caixa de diálogo do atributo tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-187">Click **Add Attribute** tooopen hello attribute dialog.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="f5fa6-190">b.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-190">b.</span></span> <span data-ttu-id="f5fa6-191">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-191">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="f5fa6-192">c.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-192">c.</span></span> <span data-ttu-id="f5fa6-193">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-193">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f5fa6-194">d.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-194">d.</span></span> <span data-ttu-id="f5fa6-195">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="f5fa6-195">Click **Ok**</span></span>

10. <span data-ttu-id="f5fa6-196">Executar Olá seguindo as etapas na Olá **nome** atributo -</span><span class="sxs-lookup"><span data-stu-id="f5fa6-196">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="f5fa6-197">a.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-197">a.</span></span> <span data-ttu-id="f5fa6-198">Clique em saudação do hello atributo tooopen **Editar atributo** janela.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-198">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="f5fa6-200">b.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-200">b.</span></span> <span data-ttu-id="f5fa6-201">Excluir o valor da URL de saudação da saudação **namespace**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-201">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="f5fa6-202">c.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-202">c.</span></span> <span data-ttu-id="f5fa6-203">Clique em **Okey** toosave configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-203">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="f5fa6-204">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-204">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="f5fa6-206">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-206">Click **Save**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="f5fa6-208">Vá muito**as configurações de administração do LinkedIn** seção.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-208">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="f5fa6-209">Carregar arquivo XML Olá baixado do hello portal do Azure clicando em opção de arquivo hello carregar XML.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-209">Upload hello XML file you downloaded from hello Azure portal by clicking hello Upload XML file option.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="f5fa6-211">Clique em **na** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-211">Click **On** tooenable SSO.</span></span> <span data-ttu-id="f5fa6-212">Status SSO é alterado de **não conectado** muito**conectado**</span><span class="sxs-lookup"><span data-stu-id="f5fa6-212">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5fa6-214">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f5fa6-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5fa6-215">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f5fa6-217">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f5fa6-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5fa6-218">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f5fa6-220">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f5fa6-222">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-222">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5fa6-224">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f5fa6-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f5fa6-226">a.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-226">a.</span></span> <span data-ttu-id="f5fa6-227">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5fa6-228">b.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-228">b.</span></span> <span data-ttu-id="f5fa6-229">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f5fa6-230">c.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-230">c.</span></span> <span data-ttu-id="f5fa6-231">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f5fa6-232">d.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-232">d.</span></span> <span data-ttu-id="f5fa6-233">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="f5fa6-234">Criando um usuário de teste do LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="f5fa6-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="f5fa6-235">Com suporte do aplicativo Linked Learning.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-235">Linked Learning Application supports.</span></span> <span data-ttu-id="f5fa6-236">Apenas durante o provisionamento do usuário e após a autenticação de usuários são criados automaticamente no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-236">Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="f5fa6-237">Na página de configurações de administrador Olá no comutador de portal Olá invertido LinkedIn aprendizado Olá **automaticamente atribuir licenças** tooactive tooenable apenas durante o provisionamento e isso também irá atribuir um usuário de toohello de licença.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-237">On hello admin settings page on hello LinkedIn Learning portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f5fa6-239">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f5fa6-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f5fa6-240">Nesta seção, você deve habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLinkedIn de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Learning.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f5fa6-242">**tooassign Britta Simon tooLinkedIn aprendizado, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f5fa6-242">**tooassign Britta Simon tooLinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5fa6-243">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f5fa6-245">Na lista de aplicativos hello, selecione **LinkedIn aprendizado**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-245">In hello applications list, select **LinkedIn Learning**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="f5fa6-247">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f5fa6-249">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-249">Click **Add** button.</span></span> <span data-ttu-id="f5fa6-250">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f5fa6-252">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f5fa6-253">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f5fa6-254">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f5fa6-255">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f5fa6-255">Testing single sign-on</span></span>

<span data-ttu-id="f5fa6-256">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f5fa6-257">Quando você clica em um bloco de aprendizado LinkedIn Olá Olá painel de acesso, você deve obter a página de logon do Azure hello e após o logon bem-sucedido, você deve obter em seu aplicativo de aprendizado do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="f5fa6-257">When you click hello LinkedIn Learning tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5fa6-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f5fa6-258">Additional resources</span></span>

* [<span data-ttu-id="f5fa6-259">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f5fa6-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5fa6-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f5fa6-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png