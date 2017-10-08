---
title: "Tutorial: Integração do Azure Active Directory com a SAP HANA Cloud Platform | Autenticação de Identidade | Microsoft Docs"
description: "Saiba como tooconfigure único logon entre o Active Directory do Azure e SAP HANA autenticação de identidade de plataforma de nuvem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="edfbb-103">Tutorial: Integração do Azure Active Directory com a SAP HANA Cloud Platform | Autenticação de Identidade</span><span class="sxs-lookup"><span data-stu-id="edfbb-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="edfbb-104">Neste tutorial, você aprenderá como toointegrate SAP HANA autenticação de identidade de plataforma nuvem com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="edfbb-104">In this tutorial, you learn how toointegrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="edfbb-105">Autenticação de identidade de plataforma de nuvem do SAP HANA é usada como um proxy IdP tooaccess aplicativos SAP usando o AD do Azure como Olá IdP principal.</span><span class="sxs-lookup"><span data-stu-id="edfbb-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP tooaccess SAP applications using Azure AD as hello main IdP.</span></span>

<span data-ttu-id="edfbb-106">Autenticação de identidade de plataforma de nuvem do SAP HANA integrando o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="edfbb-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="edfbb-107">Você pode controlar no AD do Azure que tenha acesso tooSAP aplicativo</span><span class="sxs-lookup"><span data-stu-id="edfbb-107">You can control in Azure AD who has access tooSAP application</span></span>
- <span data-ttu-id="edfbb-108">Você pode habilitar seu usuários tooautomatically get conectado tooSAP aplicativos-logon único (SSO) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="edfbb-108">You can enable your users tooautomatically get signed-on tooSAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="edfbb-109">Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="edfbb-109">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="edfbb-110">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="edfbb-110">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="edfbb-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="edfbb-111">Prerequisites</span></span>

<span data-ttu-id="edfbb-112">tooconfigure integração do AD do Azure com autenticação de identidade de plataforma de nuvem do SAP HANA, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="edfbb-112">tooconfigure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need hello following items:</span></span>

- <span data-ttu-id="edfbb-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="edfbb-113">An Azure AD subscription</span></span>
- <span data-ttu-id="edfbb-114">Uma assinatura da **Autenticação de Identidade da SAP HANA Cloud Platform** habilitada para SSO</span><span class="sxs-lookup"><span data-stu-id="edfbb-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="edfbb-115">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="edfbb-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="edfbb-116">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="edfbb-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="edfbb-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="edfbb-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="edfbb-118">Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="edfbb-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="edfbb-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="edfbb-119">Scenario description</span></span>
<span data-ttu-id="edfbb-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="edfbb-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="edfbb-121">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="edfbb-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="edfbb-122">Adicionando a autenticação de identidade de plataforma de nuvem do SAP HANA da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="edfbb-122">Adding SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
2. <span data-ttu-id="edfbb-123">Configurar e testar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="edfbb-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="edfbb-124">Antes de mergulhar nos detalhes técnicos Olá, é vital toounderstand conceitos de Olá que vai toolook no.</span><span class="sxs-lookup"><span data-stu-id="edfbb-124">Before diving into hello technical details, it is vital toounderstand hello concepts you're going toolook at.</span></span> <span data-ttu-id="edfbb-125">saudação de Federação do Active Directory do Azure e de autenticação de identidade de plataforma de nuvem do SAP HANA permite tooimplement SSO entre aplicativos ou serviços protegidos pelo AAD (como um IdP) com aplicativos SAP e serviços protegidos pela identidade de plataforma de nuvem do SAP HANA Autenticação.</span><span class="sxs-lookup"><span data-stu-id="edfbb-125">hello SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you tooimplement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="edfbb-126">No momento, a autenticação de identidade de plataforma de nuvem do SAP HANA atua como um provedor de identidade de Proxy de tooSAP aplicativos.</span><span class="sxs-lookup"><span data-stu-id="edfbb-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider tooSAP-applications.</span></span> <span data-ttu-id="edfbb-127">Por sua vez, Active Directory do Azure atua como Olá levam o provedor de identidade nessa configuração.</span><span class="sxs-lookup"><span data-stu-id="edfbb-127">Azure Active Directory in turn acts as hello leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="edfbb-128">Olá diagrama a seguir ilustra isso:</span><span class="sxs-lookup"><span data-stu-id="edfbb-128">hello following diagram illustrates this:</span></span>    

![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="edfbb-130">Com essa configuração, seu locatário de Autenticação de Identidade da SAP HANA Cloud Platform será configurado como um aplicativo confiável no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="edfbb-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="edfbb-131">Todos os aplicativos do SAP e serviços que você deseja tooprotect por meio dessa maneira são posteriormente configurados no console de gerenciamento de autenticação de identidade de plataforma de nuvem do SAP HANA Olá!</span><span class="sxs-lookup"><span data-stu-id="edfbb-131">All SAP applications and services you want tooprotect through this way are subsequently configured in hello SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="edfbb-132">Isso significa que a autorização para conceder acesso tooSAP aplicativos e serviços necessidades tootake local autenticação de identidade de plataforma de nuvem do SAP HANA para essa configuração (como autorização tooconfiguring contrário no Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="edfbb-132">This means that authorization for granting access tooSAP applications and services needs tootake place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed tooconfiguring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="edfbb-133">Configurando a autenticação de identidade de plataforma de nuvem do SAP HANA como um aplicativo por meio de saudação Marketplace do Azure Active Directory, você não precisa tootake respeito Configurando declarações individuais necessárias / asserções SAML e transformações necessárias tooproduce um token de autenticação válido para aplicativos SAP.</span><span class="sxs-lookup"><span data-stu-id="edfbb-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through hello Azure Active Directory Marketplace, you don't need tootake care of configuring needed individual claims / SAML assertions and transformations needed tooproduce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="edfbb-134">Atualmente, o SSO da Web foi testado somente por ambas as partes.</span><span class="sxs-lookup"><span data-stu-id="edfbb-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="edfbb-135">Fluxos necessários para a comunicação de aplicativo a API ou de API para API devem funcionar, mas ainda não foram testados.</span><span class="sxs-lookup"><span data-stu-id="edfbb-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="edfbb-136">Eles serão testados como parte das atividades subsequentes.</span><span class="sxs-lookup"><span data-stu-id="edfbb-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a><span data-ttu-id="edfbb-137">Adicionar autenticação de identidade de plataforma de nuvem do SAP HANA da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="edfbb-137">Add SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
<span data-ttu-id="edfbb-138">integração de saudação tooconfigure de autenticação de identidade de plataforma de nuvem do SAP HANA no AD do Azure, você precisa tooadd autenticação de identidade de plataforma de nuvem do SAP HANA na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="edfbb-138">tooconfigure hello integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="edfbb-139">**tooadd autenticação de identidade de plataforma do SAP HANA nuvem da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="edfbb-139">**tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="edfbb-140">Em Olá [ **portal de gerenciamento do Azure**](https://portal.azure.com), em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="edfbb-140">In hello [**Azure Management portal**](https://portal.azure.com), on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="edfbb-142">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="edfbb-142">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="edfbb-143">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="edfbb-143">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="edfbb-145">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="edfbb-145">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="edfbb-147">Na caixa de pesquisa hello, digite **autenticação de identidade de plataforma de nuvem do SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="edfbb-147">In hello search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="edfbb-149">No painel de resultados de saudação, selecione **autenticação de identidade de plataforma de nuvem do SAP HANA**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="edfbb-149">In hello results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="edfbb-151">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="edfbb-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="edfbb-152">Nesta seção, você configura e testa o SSO do Azure AD com a Autenticação de Identidade da SAP HANA Cloud Platform com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="edfbb-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="edfbb-153">Para SSO toowork, o AD do Azure precisa tooknow que usuário de contraparte Olá na autenticação de identidade de plataforma de nuvem do SAP HANA é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="edfbb-153">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA Cloud Platform Identity Authentication is tooa user in Azure AD.</span></span> <span data-ttu-id="edfbb-154">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na autenticação de identidade de plataforma de nuvem do SAP HANA deve toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="edfbb-154">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA Cloud Platform Identity Authentication needs toobe established.</span></span>

<span data-ttu-id="edfbb-155">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** na autenticação de identidade de plataforma de nuvem do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="edfbb-155">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="edfbb-156">tooconfigure e teste do Azure AD SSO com a autenticação de identidade de plataforma de nuvem do SAP HANA, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="edfbb-156">tooconfigure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="edfbb-157">**[Configurar o logon único do AD do Azure](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="edfbb-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="edfbb-158">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edfbb-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="edfbb-159">**[Criar um usuário de teste de autenticação de identidade de plataforma de nuvem do SAP HANA](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave um equivalente do Britta Simon no SAP HANA plataforma de identidade de autenticação de nuvem que é a representação toohello vinculado do Azure AD de seus.</span><span class="sxs-lookup"><span data-stu-id="edfbb-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - toohave a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="edfbb-160">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="edfbb-160">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="edfbb-161">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="edfbb-161">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="edfbb-162">Configurar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="edfbb-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="edfbb-163">Nesta seção, habilitar o SSO de AD do Azure no portal de gerenciamento do Azure hello e configurar o logon único em seu aplicativo de autenticação de identidade de plataforma de nuvem do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="edfbb-163">In this section, you enable Azure AD SSO in hello Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="edfbb-164">Aplicativo de autenticação de identidade de plataforma de nuvem do SAP HANA espera asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="edfbb-164">SAP HANA Cloud Platform Identity Authentication application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="edfbb-165">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="edfbb-165">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="edfbb-166">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="edfbb-166">hello following screenshot shows an example for this.</span></span>

![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="edfbb-168">**tooconfigure SSO do AD do Azure com a autenticação do SAP HANA nuvem plataforma de identidade, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="edfbb-168">**tooconfigure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="edfbb-169">No portal de gerenciamento do Azure do hello, no hello **autenticação de identidade de plataforma de nuvem do SAP HANA** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="edfbb-169">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="edfbb-171">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="edfbb-171">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único][5]

3. <span data-ttu-id="edfbb-173">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, se seu aplicativo SAP espera um atributo, por exemplo "firstName".</span><span class="sxs-lookup"><span data-stu-id="edfbb-173">In hello **User Attributes** section on hello **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="edfbb-174">No diálogo de atributos de token de SAML hello, adicione atributo de "firstName" hello.</span><span class="sxs-lookup"><span data-stu-id="edfbb-174">On hello SAML token attributes dialog, add hello "firstName" attribute.</span></span>
 1. <span data-ttu-id="edfbb-175">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edfbb-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
 
    ![Configurar Logon Único][6]

    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="edfbb-178">Em Olá **nome do atributo** caixa de texto Nome do tipo de atributo hello "firstName".</span><span class="sxs-lookup"><span data-stu-id="edfbb-178">In hello **Attribute Name** textbox, type hello attribute name "firstName".</span></span>
 3. <span data-ttu-id="edfbb-179">De saudação **o valor do atributo** lista, o valor do atributo select hello "user.givenname".</span><span class="sxs-lookup"><span data-stu-id="edfbb-179">From hello **Attribute Value** list, select hello attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="edfbb-180">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="edfbb-180">Click **Ok**.</span></span>

4. <span data-ttu-id="edfbb-181">Em Olá **URLs e domínio de autenticação de identidade de plataforma do SAP HANA nuvem** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="edfbb-181">On hello **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="edfbb-183">Em Olá **URL de logon** caixa de texto, digite Olá sinal na URL para aplicativo de SAP hello.</span><span class="sxs-lookup"><span data-stu-id="edfbb-183">In hello **Sign On URL** textbox, type hello sign on URL for hello SAP application.</span></span>
 2. <span data-ttu-id="edfbb-184">Em Olá **identificador** caixa de texto valor de tipo de saudação padrão a seguir:`<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="edfbb-184">In hello **Identifier** textbox, type hello value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="edfbb-185">Se você não souber esse valor, siga documentação de autenticação de identidade de plataforma de nuvem do SAP HANA Olá na [locatário SAML 2.0 configuração](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span><span class="sxs-lookup"><span data-stu-id="edfbb-185">If you don't know this value, please follow hello SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="edfbb-186">Em Olá **configuração de autenticação de identidade de plataforma do SAP HANA nuvem** seção, clique em **configurar autenticação identidade de plataforma de nuvem do SAP HANA** tooopen **configurar o logon** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edfbb-186">On hello **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** tooopen **Configure sign-on** dialog.</span></span> <span data-ttu-id="edfbb-187">Em seguida, clique em **SAML XML metadados** e salve o arquivo hello em seu computador.</span><span class="sxs-lookup"><span data-stu-id="edfbb-187">Then, click on **SAML XML Metadata** and save hello file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="edfbb-190">tooget SSO configurado para o seu aplicativo, vá tooSAP Console de administração do HANA nuvem plataforma de identidade de autenticação.</span><span class="sxs-lookup"><span data-stu-id="edfbb-190">tooget SSO configured for your application, go tooSAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="edfbb-191">Olá URL tem saudação padrão a seguir:`https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="edfbb-191">hello URL has hello following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="edfbb-192">Em seguida, siga a documentação do hello na autenticação de identidade de plataforma de nuvem do SAP HANA muito[configurar o AD do Azure como provedor de identidade corporativa na autenticação de identidade de plataforma de nuvem do SAP HANA](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="edfbb-192">Then, follow hello documentation on SAP HANA Cloud Platform Identity Authentication too[Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="edfbb-193">No portal de gerenciamento do Azure hello, clique em **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="edfbb-193">In hello Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="edfbb-194">Continue Olá etapas a seguir somente se você quiser tooadd e habilitar o SSO para outro aplicativo SAP.</span><span class="sxs-lookup"><span data-stu-id="edfbb-194">Continue hello following steps only if you want tooadd and enable SSO for another SAP application.</span></span> <span data-ttu-id="edfbb-195">Repita as etapas em Olá seção "Adicionando SAP HANA nuvem plataforma autenticação de identidade da Galeria hello" tooadd outra instância de autenticação de identidade de plataforma de nuvem do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="edfbb-195">Repeat steps under hello section “Adding SAP HANA Cloud Platform Identity Authentication from hello gallery” tooadd another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="edfbb-196">No portal de gerenciamento do Azure do hello, no hello **autenticação de identidade de plataforma de nuvem do SAP HANA** página de integração de aplicativos, clique em **logon vinculado**.</span><span class="sxs-lookup"><span data-stu-id="edfbb-196">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Configurar o logon vinculado](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="edfbb-198">Em seguida, salve a configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="edfbb-198">Then, save hello configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="edfbb-199">novo aplicativo de saudação aproveitará a configuração de SSO Olá para aplicativo SAP anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="edfbb-199">hello new application will leverage hello SSO configuration for hello previous SAP application.</span></span> <span data-ttu-id="edfbb-200">Certifique-se de use Olá mesmo provedores de identidade corporativa no hello Console de administração do SAP HANA nuvem plataforma de identidade de autenticação.</span><span class="sxs-lookup"><span data-stu-id="edfbb-200">Please make sure you use hello same Corporate Identity Providers in hello SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="edfbb-201">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="edfbb-201">Create an Azure AD test user</span></span>
<span data-ttu-id="edfbb-202">Olá objetivo desta seção é toocreate um usuário de teste no novo portal de saudação chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edfbb-202">hello objective of this section is toocreate a test user in hello new portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="edfbb-204">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="edfbb-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="edfbb-205">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="edfbb-205">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="edfbb-207">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="edfbb-207">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="edfbb-209">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edfbb-209">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="edfbb-211">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="edfbb-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="edfbb-213">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="edfbb-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="edfbb-214">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="edfbb-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="edfbb-215">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="edfbb-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>
  4. <span data-ttu-id="edfbb-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="edfbb-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="edfbb-217">Criar um usuário de teste da Autenticação de Identidade da SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="edfbb-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="edfbb-218">Você não precisa toocreate um usuário na autenticação de identidade de plataforma de nuvem do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="edfbb-218">You don't need toocreate an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="edfbb-219">Os usuários que estão no repositório do usuário de saudação do AD do Azure podem usar a funcionalidade de SSO de saudação.</span><span class="sxs-lookup"><span data-stu-id="edfbb-219">Users who are in hello Azure AD user store can use hello SSO functionality.</span></span>

<span data-ttu-id="edfbb-220">Autenticação de identidade de plataforma de nuvem do SAP HANA dá suporte à opção de federação de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="edfbb-220">SAP HANA Cloud Platform Identity Authentication supports hello Identity Federation option.</span></span> <span data-ttu-id="edfbb-221">Esta opção permite Olá aplicativo toocheck se usuários Olá autenticados pelo provedor de identidade corporativa Olá existirem em Olá repositório do SAP HANA nuvem plataforma identidade autenticação do usuário.</span><span class="sxs-lookup"><span data-stu-id="edfbb-221">This option allows hello application toocheck if hello users authenticated by hello corporate identity provider exist in hello user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="edfbb-222">Na configuração padrão de saudação, Olá opção de federação de identidade está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="edfbb-222">In hello default setting, hello Identity Federation option is disabled.</span></span> <span data-ttu-id="edfbb-223">Se a federação de identidade é habilitada, somente os usuários de saudação que são importados na autenticação de identidade de plataforma de nuvem do SAP HANA são tooaccess capaz de aplicativo de hello.</span><span class="sxs-lookup"><span data-stu-id="edfbb-223">If Identity Federation is enabled, only hello users that are imported in SAP HANA Cloud Platform Identity Authentication are able tooaccess hello application.</span></span> 

<span data-ttu-id="edfbb-224">Para obter mais informações sobre como tooenable ou desabilitar a federação de identidade com a autenticação do SAP HANA nuvem plataforma de identidade, consulte Habilitar a federação de identidade com a autenticação de identidade de plataforma do SAP HANA nuvem em [configurar federação de identidade com hello repositório do SAP HANA nuvem plataforma identidade de autenticação do usuário. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="edfbb-224">For more information about how tooenable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with hello User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="edfbb-225">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="edfbb-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="edfbb-226">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooSAP seu acesso autenticação de identidade de plataforma de nuvem HANA.</span><span class="sxs-lookup"><span data-stu-id="edfbb-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooSAP HANA Cloud Platform Identity Authentication.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="edfbb-228">**tooassign Britta Simon tooSAP autenticação de identidade de plataforma de nuvem HANA, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="edfbb-228">**tooassign Britta Simon tooSAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="edfbb-229">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="edfbb-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="edfbb-231">Na lista de aplicativos hello, selecione **autenticação de identidade de plataforma de nuvem do SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="edfbb-231">In hello applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="edfbb-233">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="edfbb-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="edfbb-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="edfbb-235">Click **Add** button.</span></span> <span data-ttu-id="edfbb-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edfbb-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="edfbb-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="edfbb-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="edfbb-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edfbb-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="edfbb-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edfbb-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="edfbb-241">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="edfbb-241">Test single sign-on</span></span>

<span data-ttu-id="edfbb-242">Nesta seção, você deve testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="edfbb-242">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="edfbb-243">Quando você clica em um bloco de autenticação de identidade de plataforma de nuvem do SAP HANA Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de autenticação de identidade de plataforma de nuvem do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="edfbb-243">When you click hello SAP HANA Cloud Platform Identity Authentication tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="edfbb-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="edfbb-244">Additional resources</span></span>

* [<span data-ttu-id="edfbb-245">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="edfbb-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="edfbb-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="edfbb-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png