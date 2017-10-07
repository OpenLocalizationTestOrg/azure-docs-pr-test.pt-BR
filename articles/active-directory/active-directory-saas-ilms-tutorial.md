---
title: "Tutorial: Integração do Azure Active Directory ao iLMS | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="162ff-103">Tutorial: Integração do Azure Active Directory ao iLMS</span><span class="sxs-lookup"><span data-stu-id="162ff-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="162ff-104">Neste tutorial, você aprenderá como iLMS toointegrate com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="162ff-104">In this tutorial, you learn how toointegrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="162ff-105">Integrando iLMS com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="162ff-105">Integrating iLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="162ff-106">Você pode controlar no AD do Azure que tenha acesso tooiLMS</span><span class="sxs-lookup"><span data-stu-id="162ff-106">You can control in Azure AD who has access tooiLMS</span></span>
- <span data-ttu-id="162ff-107">Você pode habilitar seus usuários tooautomatically get conectado tooiLMS (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="162ff-107">You can enable your users tooautomatically get signed-on tooiLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="162ff-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="162ff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="162ff-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="162ff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="162ff-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="162ff-110">Prerequisites</span></span>

<span data-ttu-id="162ff-111">tooconfigure integração do AD do Azure com iLMS, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="162ff-111">tooconfigure Azure AD integration with iLMS, you need hello following items:</span></span>

- <span data-ttu-id="162ff-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="162ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="162ff-113">Uma assinatura do iLMS habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="162ff-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="162ff-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="162ff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="162ff-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="162ff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="162ff-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="162ff-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="162ff-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="162ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="162ff-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="162ff-118">Scenario description</span></span>
<span data-ttu-id="162ff-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="162ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="162ff-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="162ff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="162ff-121">Adicionando iLMS da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="162ff-121">Adding iLMS from hello gallery</span></span>
2. <span data-ttu-id="162ff-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="162ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-hello-gallery"></a><span data-ttu-id="162ff-123">Adicionando iLMS da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="162ff-123">Adding iLMS from hello gallery</span></span>
<span data-ttu-id="162ff-124">integração de saudação tooconfigure de iLMS no AD do Azure, você precisa iLMS tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="162ff-124">tooconfigure hello integration of iLMS into Azure AD, you need tooadd iLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="162ff-125">**iLMS tooadd da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="162ff-125">**tooadd iLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="162ff-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="162ff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="162ff-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="162ff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="162ff-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="162ff-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="162ff-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="162ff-131">tooadd new application, click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="162ff-133">Na caixa de pesquisa hello, digite **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="162ff-133">In hello search box, type **iLMS**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="162ff-135">No painel de resultados de saudação, selecione **iLMS**, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="162ff-135">In hello results panel, select **iLMS**, then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="162ff-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="162ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="162ff-138">Nesta seção, você configura e testa o logon único do Azure AD com o iLMS, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="162ff-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="162ff-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em iLMS é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="162ff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in iLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="162ff-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em iLMS precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="162ff-140">In other words, a link relationship between an Azure AD user and hello related user in iLMS needs toobe established.</span></span>

<span data-ttu-id="162ff-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em iLMS.</span><span class="sxs-lookup"><span data-stu-id="162ff-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in iLMS.</span></span>

<span data-ttu-id="162ff-142">tooconfigure e teste de logon único do AD do Azure com iLMS, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="162ff-142">tooconfigure and test Azure AD single sign-on with iLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="162ff-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="162ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="162ff-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="162ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="162ff-145">**[Criar um usuário de teste iLMS](#creating-an-ilms-test-user)**  -toohave um equivalente do Britta Simon em iLMS é a representação toohello vinculado do Azure AD de seus.</span><span class="sxs-lookup"><span data-stu-id="162ff-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - toohave a counterpart of Britta Simon in iLMS that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="162ff-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="162ff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="162ff-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="162ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="162ff-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="162ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="162ff-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo iLMS.</span><span class="sxs-lookup"><span data-stu-id="162ff-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="162ff-150">**tooconfigure AD do Azure-logon único com iLMS, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="162ff-150">**tooconfigure Azure AD single sign-on with iLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="162ff-151">Em Olá portal do Azure, Olá **iLMS** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="162ff-151">In hello Azure portal, on hello **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="162ff-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="162ff-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="162ff-155">Em Olá **iLMS domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="162ff-155">On hello **iLMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="162ff-157">a.</span><span class="sxs-lookup"><span data-stu-id="162ff-157">a.</span></span> <span data-ttu-id="162ff-158">Em hello **identificador** textbox, colar Olá **identificador** valor copiar de **provedor** seção das configurações de SAML no portal de administração de iLMS.</span><span class="sxs-lookup"><span data-stu-id="162ff-158">In hello **Identifier** textbox, paste hello **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="162ff-159">b.</span><span class="sxs-lookup"><span data-stu-id="162ff-159">b.</span></span> <span data-ttu-id="162ff-160">Em Olá **URL de resposta** caixa de texto, colar Olá **(URL) do ponto de extremidade** valor copiar de **provedor de serviços** seção das configurações de SAML no portal de administração iLMS ter seguinte Olá padrão`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="162ff-160">In hello **Reply URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having hello following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="162ff-161">“123456” é um valor de exemplo de identificador.</span><span class="sxs-lookup"><span data-stu-id="162ff-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="162ff-162">Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="162ff-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="162ff-164">Em hello **URL de logon** textbox, colar Olá **(URL) do ponto de extremidade** valor copiar de **provedor** seção das configurações de SAML no portal de administração de iLMS como`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="162ff-164">In hello **Sign-on URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="162ff-165">tooenable JIT provisionamento, o aplicativo de iLMS espera asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="162ff-165">tooenable JIT provisioning, iLMS application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="162ff-166">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="162ff-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="162ff-167">Você pode gerenciar os valores hello desses atributos de saudação **atributos de usuário** seção na página de integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="162ff-167">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="162ff-168">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="162ff-168">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="162ff-170">Criar **departamento, região** e **divisão** atributos e adicione o nome da saudação desses atributos em iLMS.</span><span class="sxs-lookup"><span data-stu-id="162ff-170">Create **Department, Region** and **Division** attributes and add hello name of these attributes in iLMS.</span></span> <span data-ttu-id="162ff-171">Todos esses atributos mostrados acima são necessários.</span><span class="sxs-lookup"><span data-stu-id="162ff-171">All these attributes shown above are required.</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="162ff-172">Você tem tooenable **criar conta de usuário Un-recognized** na iLMS toomap esses atributos.</span><span class="sxs-lookup"><span data-stu-id="162ff-172">You have tooenable **Create Un-recognized User Account** in iLMS toomap these attributes.</span></span> <span data-ttu-id="162ff-173">Siga as instruções de saudação [aqui](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget uma ideia na configuração de atributos de saudação.</span><span class="sxs-lookup"><span data-stu-id="162ff-173">Follow hello instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget an idea on hello attributes configuration.</span></span>

6. <span data-ttu-id="162ff-174">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="162ff-174">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="162ff-175">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="162ff-175">Attribute Name</span></span> | <span data-ttu-id="162ff-176">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="162ff-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="162ff-177">division</span><span class="sxs-lookup"><span data-stu-id="162ff-177">division</span></span> | <span data-ttu-id="162ff-178">user.department</span><span class="sxs-lookup"><span data-stu-id="162ff-178">user.department</span></span> |
    | <span data-ttu-id="162ff-179">region</span><span class="sxs-lookup"><span data-stu-id="162ff-179">region</span></span> | <span data-ttu-id="162ff-180">user.state</span><span class="sxs-lookup"><span data-stu-id="162ff-180">user.state</span></span> |
    | <span data-ttu-id="162ff-181">department</span><span class="sxs-lookup"><span data-stu-id="162ff-181">department</span></span> | <span data-ttu-id="162ff-182">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="162ff-182">user.jobtitle</span></span> |

    <span data-ttu-id="162ff-183">a.</span><span class="sxs-lookup"><span data-stu-id="162ff-183">a.</span></span> <span data-ttu-id="162ff-184">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="162ff-184">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="162ff-187">b.</span><span class="sxs-lookup"><span data-stu-id="162ff-187">b.</span></span> <span data-ttu-id="162ff-188">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="162ff-188">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="162ff-189">c.</span><span class="sxs-lookup"><span data-stu-id="162ff-189">c.</span></span> <span data-ttu-id="162ff-190">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="162ff-190">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="162ff-191">d.</span><span class="sxs-lookup"><span data-stu-id="162ff-191">d.</span></span> <span data-ttu-id="162ff-192">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="162ff-192">Click **Ok**</span></span>

7. <span data-ttu-id="162ff-193">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="162ff-193">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="162ff-195">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="162ff-195">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="162ff-197">Em uma janela do navegador web diferente, faça logon no tooyour **portal de administração de iLMS** como um administrador.</span><span class="sxs-lookup"><span data-stu-id="162ff-197">In a different web browser window, log in tooyour **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="162ff-198">Clique em **SSO:SAML** em **configurações** guia Configurações do SAML tooopen e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="162ff-198">Click **SSO:SAML** under **Settings** tab tooopen SAML settings and perform hello following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="162ff-200">a.</span><span class="sxs-lookup"><span data-stu-id="162ff-200">a.</span></span> <span data-ttu-id="162ff-201">Expanda Olá **provedor** Olá seção e cópia **identificador** e **(URL) do ponto de extremidade** valor.</span><span class="sxs-lookup"><span data-stu-id="162ff-201">Expand hello **Service Provider** section and copy hello **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="162ff-203">b.</span><span class="sxs-lookup"><span data-stu-id="162ff-203">b.</span></span> <span data-ttu-id="162ff-204">Na seção **Provedor de Identidade**, clique em **Importar Metadados**.</span><span class="sxs-lookup"><span data-stu-id="162ff-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="162ff-205">c.</span><span class="sxs-lookup"><span data-stu-id="162ff-205">c.</span></span> <span data-ttu-id="162ff-206">Selecione Olá **metadados** arquivo baixado do Portal do Azure de **o certificado de autenticação SAML** seção.</span><span class="sxs-lookup"><span data-stu-id="162ff-206">Select hello **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="162ff-208">d.</span><span class="sxs-lookup"><span data-stu-id="162ff-208">d.</span></span> <span data-ttu-id="162ff-209">Se você quiser tooenable JIT Provisionando toocreate iLMS contas para cancelar-reconhecer os usuários, execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="162ff-209">If you want tooenable JIT provisioning toocreate iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="162ff-210">Marque a opção **Criar Conta de Usuário Não Reconhecido**.</span><span class="sxs-lookup"><span data-stu-id="162ff-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="162ff-212">Mapear atributos de saudação no AD do Azure com atributos de saudação em iLMS.</span><span class="sxs-lookup"><span data-stu-id="162ff-212">Map hello attributes in Azure AD with hello attributes in iLMS.</span></span> <span data-ttu-id="162ff-213">Na coluna de atributo hello, especifique valor padrão do hello atributos nome ou hello.</span><span class="sxs-lookup"><span data-stu-id="162ff-213">In hello attribute column, specify hello attributes name or hello default value.</span></span>

    <span data-ttu-id="162ff-214">e.</span><span class="sxs-lookup"><span data-stu-id="162ff-214">e.</span></span> <span data-ttu-id="162ff-215">Vá muito**regras de negócio** guia e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="162ff-215">Go too**Business Rules** tab and perform hello following steps:</span></span> 
        
       ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="162ff-217">Verificar **criar regiões de Un-recognized, divisões e departamentos** toocreate regiões, divisões e departamentos que já não existem no tempo de saudação do logon único.</span><span class="sxs-lookup"><span data-stu-id="162ff-217">Check **Create Un-recognized Regions, Divisions and Departments** toocreate Regions, Divisions, and Departments that do not already exist at hello time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="162ff-218">Verificar **atualização perfil de usuário durante entrar** toospecify se o perfil do usuário Olá é atualizado com cada logon único.</span><span class="sxs-lookup"><span data-stu-id="162ff-218">Check **Update User Profile During Sign-in** toospecify whether hello user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="162ff-219">Se hello **"Atualização em branco valores para não campos no perfil de usuário obrigatório"** opção estiver marcada, os campos de perfil opcional que estão em branco após a entrada será também fazem com que Olá iLMS perfil de usuário toocontain de valores em branco para esses campos.</span><span class="sxs-lookup"><span data-stu-id="162ff-219">If hello **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause hello user’s iLMS profile toocontain blank values for those fields.</span></span>
        
       - <span data-ttu-id="162ff-220">Verificar **Enviar Email de notificação de erro** e insira o email de saudação do usuário Olá onde você deseja que o email de notificação de erro tooreceive hello.</span><span class="sxs-lookup"><span data-stu-id="162ff-220">Check **Send Error Notification Email** and enter hello email of hello user where you want tooreceive hello error notification email.</span></span>

11. <span data-ttu-id="162ff-221">Clique em **salvar** botão Configurações de saudação toosave.</span><span class="sxs-lookup"><span data-stu-id="162ff-221">Click **Save** button toosave hello settings.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="162ff-223">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="162ff-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="162ff-224">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="162ff-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="162ff-225">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="162ff-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="162ff-226">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="162ff-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="162ff-227">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="162ff-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="162ff-229">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="162ff-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="162ff-230">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="162ff-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="162ff-232">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="162ff-232">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="162ff-234">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="162ff-234">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="162ff-236">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="162ff-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="162ff-238">a.</span><span class="sxs-lookup"><span data-stu-id="162ff-238">a.</span></span> <span data-ttu-id="162ff-239">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="162ff-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="162ff-240">b.</span><span class="sxs-lookup"><span data-stu-id="162ff-240">b.</span></span> <span data-ttu-id="162ff-241">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="162ff-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="162ff-242">c.</span><span class="sxs-lookup"><span data-stu-id="162ff-242">c.</span></span> <span data-ttu-id="162ff-243">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="162ff-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="162ff-244">d.</span><span class="sxs-lookup"><span data-stu-id="162ff-244">d.</span></span> <span data-ttu-id="162ff-245">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="162ff-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="162ff-246">Criando um usuário de teste do iLMS</span><span class="sxs-lookup"><span data-stu-id="162ff-246">Creating an iLMS test user</span></span>

<span data-ttu-id="162ff-247">Aplicativo dá suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação são criados automaticamente no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="162ff-247">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="162ff-248">JIT funcionará, se você clicou Olá **criar conta de usuário Un-recognized** caixa de seleção durante a configuração de SAML no portal de administração de iLMS.</span><span class="sxs-lookup"><span data-stu-id="162ff-248">JIT will work, if you have clicked hello **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="162ff-249">Se você precisar toocreate um usuário manualmente, em seguida, siga etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="162ff-249">If you need toocreate an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="162ff-250">Faça logon no site da empresa iLMS tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="162ff-250">Log in tooyour iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="162ff-251">Clique em **"Registrar usuário"** em **usuários** guia tooopen **registrar usuário** página.</span><span class="sxs-lookup"><span data-stu-id="162ff-251">Click **“Register User”** under **Users** tab tooopen **Register User** page.</span></span> 
   
   ![Adicionar Funcionário](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="162ff-253">Em Olá **"Registrar usuário"** página, execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="162ff-253">On hello **“Register User”** page, perform hello following steps.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="162ff-255">a.</span><span class="sxs-lookup"><span data-stu-id="162ff-255">a.</span></span> <span data-ttu-id="162ff-256">Em Olá **nome** caixa de texto, tipo hello nome Britta.</span><span class="sxs-lookup"><span data-stu-id="162ff-256">In hello **First Name** textbox, type hello first name Britta.</span></span>
   
    <span data-ttu-id="162ff-257">b.</span><span class="sxs-lookup"><span data-stu-id="162ff-257">b.</span></span> <span data-ttu-id="162ff-258">Em Olá **Sobrenome** caixa de texto, Olá tipo sobrenome Simon.</span><span class="sxs-lookup"><span data-stu-id="162ff-258">In hello **Last Name** textbox, type hello last name Simon.</span></span>

    <span data-ttu-id="162ff-259">c.</span><span class="sxs-lookup"><span data-stu-id="162ff-259">c.</span></span> <span data-ttu-id="162ff-260">Em Olá **ID de Email** caixa de texto, tipo hello endereço de email da conta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="162ff-260">In hello **Email ID** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="162ff-261">d.</span><span class="sxs-lookup"><span data-stu-id="162ff-261">d.</span></span> <span data-ttu-id="162ff-262">Em Olá **região** suspenso, o valor Olá selecione região.</span><span class="sxs-lookup"><span data-stu-id="162ff-262">In hello **Region** dropdown, select hello value for region.</span></span>

    <span data-ttu-id="162ff-263">e.</span><span class="sxs-lookup"><span data-stu-id="162ff-263">e.</span></span> <span data-ttu-id="162ff-264">Em Olá **divisão** suspenso, o valor Olá selecione divisão.</span><span class="sxs-lookup"><span data-stu-id="162ff-264">In hello **Division** dropdown, select hello value for division.</span></span>

    <span data-ttu-id="162ff-265">f.</span><span class="sxs-lookup"><span data-stu-id="162ff-265">f.</span></span> <span data-ttu-id="162ff-266">Em Olá **departamento** suspenso, o valor Olá selecione departamento.</span><span class="sxs-lookup"><span data-stu-id="162ff-266">In hello **Department** dropdown, select hello value for department.</span></span>

    <span data-ttu-id="162ff-267">g.</span><span class="sxs-lookup"><span data-stu-id="162ff-267">g.</span></span> <span data-ttu-id="162ff-268">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="162ff-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="162ff-269">Você pode enviar toouser de email de registro selecionando **enviar email de registro** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="162ff-269">You can send registration mail toouser by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="162ff-270">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="162ff-270">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="162ff-271">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooiLMS seu acesso.</span><span class="sxs-lookup"><span data-stu-id="162ff-271">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooiLMS.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="162ff-273">**tooassign Britta Simon tooiLMS, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="162ff-273">**tooassign Britta Simon tooiLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="162ff-274">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="162ff-274">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="162ff-276">Na lista de aplicativos hello, selecione **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="162ff-276">In hello applications list, select **iLMS**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="162ff-278">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="162ff-278">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="162ff-280">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="162ff-280">Click **Add** button.</span></span> <span data-ttu-id="162ff-281">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="162ff-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="162ff-283">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="162ff-283">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="162ff-284">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="162ff-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="162ff-285">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="162ff-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="162ff-286">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="162ff-286">Testing single sign-on</span></span>

<span data-ttu-id="162ff-287">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="162ff-287">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="162ff-288">Quando você clica em Olá iLMS bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour iLMS aplicativo.</span><span class="sxs-lookup"><span data-stu-id="162ff-288">When you click hello iLMS tile in hello Access Panel, you should get automatically signed-on tooyour iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="162ff-289">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="162ff-289">Additional resources</span></span>

* [<span data-ttu-id="162ff-290">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="162ff-290">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="162ff-291">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="162ff-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

