---
title: "Tutorial: Integração do Azure Active Directory com o IBM Kenexa Survey Enterprise | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o IBM Kenexa pesquisa Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="3cae0-103">Tutorial: Integração do Azure Active Directory com o IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="3cae0-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="3cae0-104">Neste tutorial, você aprenderá como toointegrate IBM Kenexa pesquisa Enterprise com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="3cae0-104">In this tutorial, you learn how toointegrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3cae0-105">Integração do IBM Kenexa pesquisa Enterprise com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cae0-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3cae0-106">Você pode controlar no AD do Azure que tenha acesso tooIBM Kenexa pesquisa Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3cae0-106">You can control in Azure AD who has access tooIBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="3cae0-107">Você pode habilitar seus usuários de entrada tooautomatically tooIBM Kenexa pesquisa Enterprise usando logon único (SSO) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cae0-107">You can enable your users tooautomatically sign in tooIBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3cae0-108">Você pode gerenciar suas contas em um local central: Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cae0-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="3cae0-109">Se você quiser tooknow mais sobre o software como uma integração de aplicativo de serviço (SaaS) com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3cae0-109">If you want tooknow more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cae0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3cae0-110">Prerequisites</span></span>

<span data-ttu-id="3cae0-111">tooconfigure integração do AD do Azure com o IBM Kenexa pesquisa Enterprise, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cae0-111">tooconfigure Azure AD integration with IBM Kenexa Survey Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="3cae0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3cae0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3cae0-113">Uma assinatura habilitada para SSO do IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="3cae0-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3cae0-114">Quando você testar etapas Olá neste tutorial, é recomendável que você não use um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3cae0-114">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="3cae0-115">etapas de saudação tootest neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3cae0-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="3cae0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3cae0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3cae0-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3cae0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3cae0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3cae0-118">Scenario description</span></span>
<span data-ttu-id="3cae0-119">Neste tutorial, você testa o SSO do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3cae0-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="3cae0-120">cenário de saudação descrito Olá tutorial consiste em duas principais blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="3cae0-120">hello scenario outlined in hello tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="3cae0-121">Adicionando IBM Kenexa pesquisa Enterprise na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3cae0-121">Adding IBM Kenexa Survey Enterprise from hello gallery</span></span>
* <span data-ttu-id="3cae0-122">Configurar e testar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cae0-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a><span data-ttu-id="3cae0-123">Adicionar IBM Kenexa pesquisa Enterprise na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3cae0-123">Add IBM Kenexa Survey Enterprise from hello gallery</span></span>
<span data-ttu-id="3cae0-124">tooconfigure a integração de saudação do IBM Kenexa pesquisa Enterprise no AD do Azure, adicione IBM Kenexa pesquisa Enterprise na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3cae0-124">tooconfigure hello integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3cae0-125">tooadd IBM Kenexa pesquisa Enterprise na Galeria de hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cae0-125">tooadd IBM Kenexa Survey Enterprise from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="3cae0-126">Em Olá [portal do Azure](https://portal.azure.com), no painel esquerdo de hello, clique Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="3cae0-126">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** button.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="3cae0-128">Selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3cae0-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="3cae0-130">tooadd um aplicativo, clique em Olá **novo aplicativo** botão.</span><span class="sxs-lookup"><span data-stu-id="3cae0-130">tooadd an application, click hello **New application** button.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="3cae0-132">Na caixa de pesquisa hello, digite **IBM Kenexa pesquisa Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="3cae0-132">In hello search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="3cae0-134">Na lista de resultados de saudação, selecione **IBM Kenexa pesquisa Enterprise**e, em seguida, clique em Olá **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3cae0-134">In hello results list, select **IBM Kenexa Survey Enterprise**, and then click hello **Add** button tooadd hello application.</span></span>

    ![IBM Kenexa pesquisa Enterprise na lista de resultados de saudação](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3cae0-136">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cae0-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3cae0-137">Nesta seção, você configura e testa o SSO do Azure AD com o IBM Kenexa Survey Enterprise, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3cae0-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3cae0-138">Para SSO toowork, o AD do Azure precisa equivalente de usuário tooidentify Olá IBM Kenexa pesquisa corporativo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cae0-138">For SSO toowork, Azure AD needs tooidentify hello IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="3cae0-139">Em outras palavras, o Azure AD precisa estabelecer uma relação de vínculo entre um usuário do Azure AD e um usuário relacionado do IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3cae0-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="3cae0-140">relação de link tooestablish hello, atribuir valor Olá Olá **nome de usuário** no IBM Kenexa pesquisa Enterprise como valor de saudação do hello **Username** no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cae0-140">tooestablish hello link relationship, assign hello value of hello **user name** in IBM Kenexa Survey Enterprise as hello value of hello **Username** in Azure AD.</span></span>

<span data-ttu-id="3cae0-141">tooconfigure e teste do Azure AD SSO com o IBM Kenexa pesquisa Enterprise, blocos de construção de saudação concluída em duas seções de saudação.</span><span class="sxs-lookup"><span data-stu-id="3cae0-141">tooconfigure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete hello building blocks in hello next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="3cae0-142">Configurar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cae0-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="3cae0-143">Nesta seção, habilitar o SSO do AD do Azure no portal do Azure de saudação e configurar SSO em seu aplicativo IBM Kenexa pesquisa Enterprise fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="3cae0-143">In this section, you enable Azure AD SSO in hello Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing hello following:</span></span>

1. <span data-ttu-id="3cae0-144">Em Olá portal do Azure, Olá **IBM Kenexa pesquisa Enterprise** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="3cae0-144">In hello Azure portal, on hello **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único do IBM Kenexa Survey Enterprise][4]

2. <span data-ttu-id="3cae0-146">Em Olá **o logon único** caixa de diálogo Olá **modo** selecione **baseado no SAML logon** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="3cae0-146">In hello **Single sign-on** dialog box, in hello **Mode** box, select **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="3cae0-148">Em Olá **URLs e domínio da empresa de pesquisa do IBM Kenexa** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cae0-148">In hello **IBM Kenexa Survey Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="3cae0-150">a.</span><span class="sxs-lookup"><span data-stu-id="3cae0-150">a.</span></span> <span data-ttu-id="3cae0-151">Em Olá **identificador** caixa de texto, digite uma URL com saudação padrão a seguir:`https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="3cae0-151">In hello **Identifier** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="3cae0-152">b.</span><span class="sxs-lookup"><span data-stu-id="3cae0-152">b.</span></span> <span data-ttu-id="3cae0-153">Em Olá **URL de resposta** caixa de texto, digite uma URL com saudação padrão a seguir:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="3cae0-153">In hello **Reply URL** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3cae0-154">Olá valores anteriores não são reais.</span><span class="sxs-lookup"><span data-stu-id="3cae0-154">hello preceding values are not real.</span></span> <span data-ttu-id="3cae0-155">Atualizá-los com o identificador real hello e URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="3cae0-155">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="3cae0-156">tooobtain Olá valores reais, Olá contato [equipe de suporte da empresa de pesquisa do IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="3cae0-156">tooobtain hello actual values, contact hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="3cae0-157">Em **o certificado de autenticação SAML**, clique em **certificado (Base64)**e, em seguida, salve o computador de tooyour de arquivo de certificado hello.</span><span class="sxs-lookup"><span data-stu-id="3cae0-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save hello certificate file tooyour computer.</span></span>

    ![link de download de certificado (Base64) Olá](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="3cae0-159">Olá aplicativo corporativo de pesquisa do IBM Kenexa espera asserções do tooreceive Olá Security asserções Markup Language (SAML) em um formato específico, o que exige que você tooadd atributo personalizado toohello configuração de mapeamentos de seus atributos de token SAML.</span><span class="sxs-lookup"><span data-stu-id="3cae0-159">hello IBM Kenexa Survey Enterprise application expects tooreceive hello Security Assertions Markup Language (SAML) assertions in a specific format, which requires you tooadd custom attribute mappings toohello configuration of your SAML token attributes.</span></span> <span data-ttu-id="3cae0-160">Olá valor da declaração do identificador de usuário Olá em resposta Olá deve corresponder Olá ID de SSO é configurado no sistema de Kenexa hello.</span><span class="sxs-lookup"><span data-stu-id="3cae0-160">hello value of hello user-identifier claim in hello response must match hello SSO ID that's configured in hello Kenexa system.</span></span> <span data-ttu-id="3cae0-161">toomap Olá identificador de usuário apropriado na sua organização como protocolo de datagrama de Internet para SSO (IDP), trabalhará com hello [equipe de suporte da empresa de pesquisa do IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="3cae0-161">toomap hello appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="3cae0-162">Por padrão, o AD do Azure define o identificador de usuário Olá como valor de nome principal (UPN) do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="3cae0-162">By default, Azure AD sets hello user identifier as hello user principal name (UPN) value.</span></span> <span data-ttu-id="3cae0-163">Você pode alterar esse valor no hello **atributo** guia, conforme mostrado no hello captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="3cae0-163">You can change this value on hello **Attribute** tab, as shown in hello following screenshot.</span></span> <span data-ttu-id="3cae0-164">integração de saudação funciona somente depois de concluir Olá mapeamento corretamente.</span><span class="sxs-lookup"><span data-stu-id="3cae0-164">hello integration works only after you've completed hello mapping correctly.</span></span>
    
    ![caixa de diálogo atributos de usuário Olá](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. <span data-ttu-id="3cae0-166">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3cae0-166">Click **Save**.</span></span>

    ![Olá configurar logon único botão Salvar](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3cae0-168">Olá tooopen **configurar o logon** janela, em **IBM Kenexa pesquisa Enterprise Configuration**, clique em **configurar o IBM Kenexa pesquisa Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="3cae0-168">tooopen hello **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![link de configurar o IBM Kenexa pesquisa Enterprise Olá](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="3cae0-170">Saudação de cópia **URL de logout**, **ID da entidade SAML**, e **único logon URL do serviço SAML** valores de saudação **referência rápida** seção.</span><span class="sxs-lookup"><span data-stu-id="3cae0-170">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from hello **Quick Reference** section.</span></span>

8. <span data-ttu-id="3cae0-171">Em Olá **configurar o logon** janela, em **referência rápida**, Olá cópia **URL de logout**, **ID da entidade SAML**, e  **Único logon URL do serviço SAML** valores.</span><span class="sxs-lookup"><span data-stu-id="3cae0-171">In hello **Configure sign-on** window, under **Quick Reference**, copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="3cae0-172">tooconfigure SSO em Olá **IBM Kenexa pesquisa Enterprise** lado, enviar Olá baixado **certificado (Base64)**, **URL de logout**, **ID da entidade SAML**, e **único logon URL do serviço SAML** valores toohello [equipe de suporte da empresa de pesquisa do IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="3cae0-172">tooconfigure SSO on hello **IBM Kenexa Survey Enterprise** side, send hello downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values toohello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="3cae0-173">Você pode consultar a versão concisa tooa essas instruções Olá [portal do Azure](https://portal.azure.com) enquanto você estiver configurando o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3cae0-173">You can refer tooa concise version of these instructions in hello [Azure portal](https://portal.azure.com) while you are setting up hello app.</span></span> <span data-ttu-id="3cae0-174">Depois de adicionar o aplicativo hello da saudação **do Active Directory** > **aplicativos empresariais** seção, basta clicar em Olá **o logon único** guia e, em seguida, acessar Olá inseridos documentação por meio de saudação **configuração** seção Olá final.</span><span class="sxs-lookup"><span data-stu-id="3cae0-174">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, simply click hello **single sign-on** tab, and then access hello embedded documentation through hello **Configuration** section at hello end.</span></span> <span data-ttu-id="3cae0-175">toolearn mais sobre o recurso de documentação do embedded hello, consulte [AD do Azure inseridos documentação](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3cae0-175">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3cae0-176">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cae0-176">Create an Azure AD test user</span></span>
<span data-ttu-id="3cae0-177">Nesta seção, você pode criar Britta Simon de usuário de teste no portal do Azure de saudação fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="3cae0-177">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![Criar um usuário de teste do Azure AD][100]

1. <span data-ttu-id="3cae0-179">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="3cae0-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3cae0-181">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3cae0-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3cae0-183">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3cae0-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![botão Adicionar de saudação](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3cae0-185">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cae0-185">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3cae0-187">a.</span><span class="sxs-lookup"><span data-stu-id="3cae0-187">a.</span></span> <span data-ttu-id="3cae0-188">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3cae0-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3cae0-189">b.</span><span class="sxs-lookup"><span data-stu-id="3cae0-189">b.</span></span> <span data-ttu-id="3cae0-190">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cae0-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="3cae0-191">c.</span><span class="sxs-lookup"><span data-stu-id="3cae0-191">c.</span></span> <span data-ttu-id="3cae0-192">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="3cae0-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="3cae0-193">d.</span><span class="sxs-lookup"><span data-stu-id="3cae0-193">d.</span></span> <span data-ttu-id="3cae0-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3cae0-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="3cae0-195">Criar um usuário de teste do IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="3cae0-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="3cae0-196">Nesta seção, você criará uma usuária chamada Brenda Fernandes no IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3cae0-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="3cae0-197">usuários toocreate Olá sistema IBM Kenexa pesquisa Enterprise e Olá mapa identificação do SSO para eles, você pode trabalhar com hello [equipe de suporte da empresa de pesquisa do IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="3cae0-197">toocreate users in hello IBM Kenexa Survey Enterprise system and map hello SSO ID for them, you can work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="3cae0-198">Este valor de ID de SSO também deve ser mapeado toohello valor de identificador de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cae0-198">This SSO ID value should also be mapped toohello user identifier value from Azure AD.</span></span> <span data-ttu-id="3cae0-199">Você pode alterar essa configuração padrão em Olá **atributo** guia.</span><span class="sxs-lookup"><span data-stu-id="3cae0-199">You can change this default setting on hello **Attribute** tab.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3cae0-200">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3cae0-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="3cae0-201">Nesta seção, você permitir que o usuário Britta Simon toouse SSO do Azure, concedendo acesso tooIBM Kenexa pesquisa Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3cae0-201">In this section, you enable user Britta Simon toouse Azure SSO by granting access tooIBM Kenexa Survey Enterprise.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="3cae0-203">usuário tooassign Britta Simon tooIBM Kenexa pesquisa Enterprise, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cae0-203">tooassign user Britta Simon tooIBM Kenexa Survey Enterprise, do hello following:</span></span>

1. <span data-ttu-id="3cae0-204">Olá portal do Azure, abra o hello **aplicativos** exibir, vá toohello **diretório** exibição, selecione **aplicativos empresariais**e, em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3cae0-204">In hello Azure portal, open hello **Applications** view, go toohello **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![Olá "aplicativos corporativos" e links de "Todos os aplicativos"][201] 

2. <span data-ttu-id="3cae0-206">Em Olá **aplicativos** lista, selecione **IBM Kenexa pesquisa Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="3cae0-206">In hello **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![link do IBM Kenexa pesquisa Enterprise Olá na lista de aplicativos Olá](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="3cae0-208">No painel esquerdo do hello, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3cae0-208">In hello left pane, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202] 

4. <span data-ttu-id="3cae0-210">Clique em Olá **adicionar** botão e, em seguida, em Olá **Adicionar atribuição** painel, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3cae0-210">Click hello **Add** button and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="3cae0-212">Em Olá **usuários e grupos** caixa de diálogo Olá **usuários** lista, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3cae0-212">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="3cae0-213">Em Olá **usuários e grupos** caixa de diálogo, clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="3cae0-213">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="3cae0-214">Em Olá **Adicionar atribuição** caixa de diálogo, clique em Olá **atribuir** botão.</span><span class="sxs-lookup"><span data-stu-id="3cae0-214">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3cae0-215">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="3cae0-215">Test single sign-on</span></span>

<span data-ttu-id="3cae0-216">Nesta seção, você pode testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="3cae0-216">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="3cae0-217">Quando você clica em Olá **IBM Kenexa pesquisa Enterprise** Olá de bloco no painel de acesso, você deve ser conectado automaticamente tooyour aplicativo IBM Kenexa pesquisa empresarial.</span><span class="sxs-lookup"><span data-stu-id="3cae0-217">When you click hello **IBM Kenexa Survey Enterprise** tile in hello Access Panel, you should be automatically signed in tooyour IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3cae0-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3cae0-218">Additional resources</span></span>

* [<span data-ttu-id="3cae0-219">Lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3cae0-219">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3cae0-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3cae0-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
