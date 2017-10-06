---
title: "Tutorial: integração do Azure Active Directory com o LinkedIn Elevate | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e elevar LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="cb7d4-103">Tutorial: integração do Azure Active Directory com o LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="cb7d4-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="cb7d4-104">Neste tutorial, você aprenderá como toointegrate LinkedIn elevar com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="cb7d4-104">In this tutorial, you learn how toointegrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb7d4-105">Integrando LinkedIn elevar AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb7d4-105">Integrating LinkedIn Elevate with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cb7d4-106">Você pode controlar no AD do Azure que tenha acesso tooLinkedIn elevar</span><span class="sxs-lookup"><span data-stu-id="cb7d4-106">You can control in Azure AD who has access tooLinkedIn Elevate</span></span>
- <span data-ttu-id="cb7d4-107">Você pode habilitar seu usuários tooautomatically get conectado tooLinkedIn elevar (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb7d4-107">You can enable your users tooautomatically get signed-on tooLinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb7d4-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="cb7d4-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="cb7d4-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb7d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb7d4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cb7d4-110">Prerequisites</span></span>

<span data-ttu-id="cb7d4-111">tooconfigure integração do AD do Azure com elevar LinkedIn, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb7d4-111">tooconfigure Azure AD integration with LinkedIn Elevate, you need hello following items:</span></span>

- <span data-ttu-id="cb7d4-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb7d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb7d4-113">Uma assinatura do LinkedIn Elevate habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="cb7d4-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb7d4-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb7d4-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cb7d4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb7d4-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="cb7d4-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb7d4-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb7d4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cb7d4-118">Scenario description</span></span>
<span data-ttu-id="cb7d4-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb7d4-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="cb7d4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb7d4-121">Adicionando LinkedIn elevar da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="cb7d4-121">Adding LinkedIn Elevate from hello gallery</span></span>
2. <span data-ttu-id="cb7d4-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb7d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-hello-gallery"></a><span data-ttu-id="cb7d4-123">Adicionando LinkedIn elevar da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="cb7d4-123">Adding LinkedIn Elevate from hello gallery</span></span>
<span data-ttu-id="cb7d4-124">integração de saudação tooconfigure do LinkedIn elevar no AD do Azure, você precisa tooadd LinkedIn elevar na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-124">tooconfigure hello integration of LinkedIn Elevate into Azure AD, you need tooadd LinkedIn Elevate from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cb7d4-125">**tooadd LinkedIn elevar da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cb7d4-125">**tooadd LinkedIn Elevate from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb7d4-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb7d4-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cb7d4-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="cb7d4-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="cb7d4-133">Na caixa de pesquisa hello, digite **LinkedIn elevar**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-133">In hello search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="cb7d4-134">No painel de resultados, clique em **LinkedIn elevar** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-134">From results panel, click **LinkedIn Elevate** tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb7d4-136">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb7d4-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb7d4-137">Nesta seção, você configurará e testará o logon único do Azure AD com o LinkedIn Elevate, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cb7d4-138">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no LinkedIn elevar é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Elevate is tooa user in Azure AD.</span></span> <span data-ttu-id="cb7d4-139">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no LinkedIn elevar precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Elevate needs toobe established.</span></span>

<span data-ttu-id="cb7d4-140">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no LinkedIn elevar.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="cb7d4-141">tooconfigure e teste de logon único do AD do Azure com elevar LinkedIn, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb7d4-141">tooconfigure and test Azure AD single sign-on with LinkedIn Elevate, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cb7d4-142">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cb7d4-143">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb7d4-144">**[Criar um usuário de teste LinkedIn elevar](#creating-a-linkedin-elevate-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="cb7d4-145">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb7d4-146">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb7d4-147">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb7d4-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb7d4-148">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo LinkedIn elevar.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-148">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="cb7d4-149">**tooconfigure AD do Azure-logon único com elevar LinkedIn, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cb7d4-149">**tooconfigure Azure AD single sign-on with LinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb7d4-150">No portal de gerenciamento do Azure do hello, no hello **LinkedIn elevar** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-150">In hello Azure Management portal, on hello **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="cb7d4-152">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-152">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="cb7d4-154">Em uma janela de navegador web diferente, logon tooyour LinkedIn elevar locatário como um administrador.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-154">In a different web browser window, sign-on tooyour LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="cb7d4-155">Em **Centro de Contas**, clique em **Configurações Globais** em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="cb7d4-156">Além disso, selecione **elevar - elevar AAD teste** na lista suspensa hello.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-156">Also, select **Elevate - Elevate AAD Test** from hello dropdown list.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="cb7d4-158">Clique em **ou clique aqui tooload e copiar campos individuais de um formulário de saudação** e cópia **Id da entidade** e **Url do consumidor de declaração acesso (ACS)**</span><span class="sxs-lookup"><span data-stu-id="cb7d4-158">Click on **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="cb7d4-160">No Portal do Azure, em **LinkedIn elevar domínio e URLs**, executar Olá etapas a seguir se você quiser tooconfigure SSO em **iniciado pelo IdP** modo</span><span class="sxs-lookup"><span data-stu-id="cb7d4-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="cb7d4-162">a.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-162">a.</span></span> <span data-ttu-id="cb7d4-163">Em Olá **identificador** caixa de texto, digite Olá **ID da entidade** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="cb7d4-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="cb7d4-164">b.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-164">b.</span></span> <span data-ttu-id="cb7d4-165">Em Olá **URL de resposta** caixa de texto, digite Olá **Url do consumidor de declaração acesso (ACS)** copiada do Portal do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="cb7d4-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="cb7d4-166">Se você quiser tooconfigure SSO em **iniciado pelo SP**, clique em Mostrar avançado URL opção de configuração na seção de configuração de saudação e configurar Olá logon URL com saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb7d4-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="cb7d4-168">Seu aplicativo LinkedIn elevar espera as asserções de SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-168">Your LinkedIn Elevate application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="cb7d4-169">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="cb7d4-170">Olá valor padrão de **identificador de usuário** é **User** mas LinkedIn elevar espera este toobe mapeada com o endereço de email do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="cb7d4-171">Para que você pode usar **user.mail** de atributo na lista de saudação ou usar o valor do atributo apropriado Olá com base na configuração de sua organização.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="cb7d4-173">Em **atributos de usuário** seção, clique em **exibir e editar todos os outros atributos de usuário** e definir atributos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="cb7d4-174">Você precisa tooadd outra declaração denominada **departamento** e o valor de saudação precisa toobe mapeado muito**User. Department**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-174">You need tooadd another claim named **department** and hello value needs toobe mapped too**user.department**.</span></span>

    | <span data-ttu-id="cb7d4-175">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="cb7d4-175">Attribute Name</span></span> | <span data-ttu-id="cb7d4-176">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="cb7d4-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="cb7d4-177">department</span><span class="sxs-lookup"><span data-stu-id="cb7d4-177">department</span></span>| <span data-ttu-id="cb7d4-178">user.department</span><span class="sxs-lookup"><span data-stu-id="cb7d4-178">user.department</span></span> |

      ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="cb7d4-180">a.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-180">a.</span></span> <span data-ttu-id="cb7d4-181">Clique na página de detalhes de atributo Adicionar atributo tooopen Olá Adicionar atributo de departamento Olá conforme mostrado abaixo-</span><span class="sxs-lookup"><span data-stu-id="cb7d4-181">Click on Add attribute tooopen hello attribute details page add hello department attribute as shown below-</span></span>

      ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="cb7d4-183">b.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-183">b.</span></span> <span data-ttu-id="cb7d4-184">Clique em **Okey** toosave atributo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-184">Click on **Ok** toosave hello attribute.</span></span>

      <span data-ttu-id="cb7d4-185">c.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-185">c.</span></span> <span data-ttu-id="cb7d4-186">Alterar o nome de saudação do atributo Olá **emailaddress** muito**email**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-186">Change hello name of hello attribute **emailaddress** too**email**.</span></span>


10. <span data-ttu-id="cb7d4-187">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-187">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="cb7d4-189">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-189">Click **Save**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="cb7d4-191">Vá muito**as configurações de administração do LinkedIn** seção.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-191">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="cb7d4-192">Carregar arquivo XML Olá que você acabou de baixar da saudação portal do Azure clicando em Olá opção de carregar o XML de arquivo.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-192">Upload hello XML file you just downloaded from hello Azure portal by clicking on hello Upload XML file option.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="cb7d4-194">Clique em **na** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-194">Click **On** tooenable SSO.</span></span> <span data-ttu-id="cb7d4-195">SSO status será alterado de **não conectado** muito**conectado**</span><span class="sxs-lookup"><span data-stu-id="cb7d4-195">SSO status will change from **Not Connected** too**Connected**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb7d4-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb7d4-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb7d4-198">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-198">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="cb7d4-200">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cb7d4-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb7d4-201">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-201">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb7d4-203">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-203">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb7d4-205">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-205">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb7d4-207">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb7d4-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb7d4-209">a.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-209">a.</span></span> <span data-ttu-id="cb7d4-210">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb7d4-211">b.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-211">b.</span></span> <span data-ttu-id="cb7d4-212">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb7d4-213">c.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-213">c.</span></span> <span data-ttu-id="cb7d4-214">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cb7d4-215">d.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-215">d.</span></span> <span data-ttu-id="cb7d4-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="cb7d4-217">Criando um usuário de teste do LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="cb7d4-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="cb7d4-218">Aplicativo elevar vinculado oferece suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação serão criados no aplicativo hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="cb7d4-219">Na página de configurações de administrador Olá no comutador de portal Olá invertido LinkedIn elevar Olá **automaticamente atribuir licenças** tooactive tooenable apenas durante o provisionamento e isso também irá atribuir um usuário de toohello de licença.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-219">On hello admin settings page on hello LinkedIn Elevate portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>

   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cb7d4-221">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb7d4-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cb7d4-222">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooLinkedIn seu acesso elevar.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLinkedIn Elevate.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="cb7d4-224">**tooassign Britta Simon tooLinkedIn elevar, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cb7d4-224">**tooassign Britta Simon tooLinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb7d4-225">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-225">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="cb7d4-227">Na lista de aplicativos hello, selecione **LinkedIn elevar**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-227">In hello applications list, select **LinkedIn Elevate**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="cb7d4-229">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="cb7d4-231">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-231">Click **Add** button.</span></span> <span data-ttu-id="cb7d4-232">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="cb7d4-234">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cb7d4-235">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb7d4-236">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb7d4-237">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="cb7d4-237">Testing single sign-on</span></span>

<span data-ttu-id="cb7d4-238">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cb7d4-239">Quando você clica Olá LinkedIn elevar lado a lado no painel de acesso de saudação, você deve obter a página de logon do Azure hello e após o logon bem-sucedido, você deve obter em seu aplicativo LinkedIn elevar.</span><span class="sxs-lookup"><span data-stu-id="cb7d4-239">When you click hello LinkedIn Elevate tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb7d4-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cb7d4-240">Additional resources</span></span>

* [<span data-ttu-id="cb7d4-241">Tutorial: Configurar o LinkedIn Elevate para o provisionamento automático de usuário com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb7d4-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="cb7d4-242">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cb7d4-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb7d4-243">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cb7d4-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
