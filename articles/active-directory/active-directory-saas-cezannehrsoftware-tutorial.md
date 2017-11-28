---
title: "Tutorial: integração do Azure Active Directory com o software Cezanne HR | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o software de RH Cezanne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="f3b86-103">Tutorial: integração do Azure Active Directory com o software Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="f3b86-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="f3b86-104">Neste tutorial, você aprenderá como toointegrate Cezanne HR software com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f3b86-104">In this tutorial, you learn how toointegrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f3b86-105">Integração de software de RH Cezanne com o Azure AD fornece Olá benefícios a seguir.</span><span class="sxs-lookup"><span data-stu-id="f3b86-105">Integrating Cezanne HR software with Azure AD provides you with hello following benefits.</span></span> <span data-ttu-id="f3b86-106">Você pode:</span><span class="sxs-lookup"><span data-stu-id="f3b86-106">You can:</span></span>

- <span data-ttu-id="f3b86-107">Controlar no AD do Azure que tenha acesso tooCezanne software de RH.</span><span class="sxs-lookup"><span data-stu-id="f3b86-107">Control in Azure AD who has access tooCezanne HR software.</span></span>
- <span data-ttu-id="f3b86-108">Habilite seus usuários de entrada tooautomatically software tooCezanne HR com logon único (SSO) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3b86-108">Enable your users tooautomatically sign in tooCezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f3b86-109">Gerenciar suas contas em um local central: Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3b86-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="f3b86-110">toolearn mais sobre o software como uma integração de aplicativo de serviço (SaaS) com o AD do Azure, consulte [o que é o acesso ao aplicativo e SSO com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f3b86-110">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3b86-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f3b86-111">Prerequisites</span></span>

<span data-ttu-id="f3b86-112">tooconfigure integração do AD do Azure com HR Cezanne software, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3b86-112">tooconfigure Azure AD integration with Cezanne HR software, you need hello following items:</span></span>

- <span data-ttu-id="f3b86-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f3b86-113">An Azure AD subscription</span></span>
- <span data-ttu-id="f3b86-114">Uma assinatura do software Cezanne HR com SSO habilitado</span><span class="sxs-lookup"><span data-stu-id="f3b86-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f3b86-115">tootest Olá etapas deste tutorial, é recomendável que você não use um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f3b86-115">tootest hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="f3b86-116">etapas de saudação tootest neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f3b86-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="f3b86-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f3b86-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f3b86-118">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3b86-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f3b86-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f3b86-119">Scenario description</span></span>
<span data-ttu-id="f3b86-120">Neste tutorial, você testa o SSO do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f3b86-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="f3b86-121">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="f3b86-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="f3b86-122">Adicionar software de RH Cezanne da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f3b86-122">Adding Cezanne HR software from hello gallery</span></span>
* <span data-ttu-id="f3b86-123">Configurar e testar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3b86-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-hello-gallery"></a><span data-ttu-id="f3b86-124">Adicionar software Cezanne HR da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f3b86-124">Add Cezanne HR software from hello gallery</span></span>
<span data-ttu-id="f3b86-125">tooconfigure a integração de saudação do software Cezanne HR no AD do Azure, adicione o software de RH Cezanne da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f3b86-125">tooconfigure hello integration of Cezanne HR software into Azure AD, add Cezanne HR software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f3b86-126">tooadd Cezanne HR software da Galeria hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3b86-126">tooadd Cezanne HR software from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="f3b86-127">Em Olá  **[portal do Azure](https://portal.azure.com)**, no hello painel esquerdo, selecione Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="f3b86-127">In hello **[Azure portal](https://portal.azure.com)**, in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![botão de "Active Directory do Azure" Hello][1]

2. <span data-ttu-id="f3b86-129">Selecione **Aplicativos empresariais** > **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Olá link de "Todos os aplicativos"][2]
    
3. <span data-ttu-id="f3b86-131">tooadd um novo aplicativo, na parte superior de saudação do hello **todos os aplicativos** caixa de diálogo, selecione **novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-131">tooadd a new application, at hello top of hello **All applications** dialog box, select **New application**.</span></span>

    ![Olá "Novo application" botão][3]

4. <span data-ttu-id="f3b86-133">Na caixa de pesquisa hello, digite **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-133">In hello search box, type **Cezanne HR Software**.</span></span>

    ![caixa de pesquisa Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="f3b86-135">Na lista de resultados de saudação, selecione **Cezanne HR Software** e, em seguida, selecione Olá **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f3b86-135">In hello results list, select **Cezanne HR Software** and then select hello **Add** button tooadd hello application.</span></span>

    ![lista de resultados de saudação](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f3b86-137">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3b86-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f3b86-138">Nesta seção, você configura e testa o SSO do Azure AD com o software Cezanne HR, com base em uma usuária de teste chamada “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="f3b86-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f3b86-139">Para SSO toowork, AD do Azure precisa de usuário do AD do Azure tooknow Olá Cezanne HR software contraparte toohello.</span><span class="sxs-lookup"><span data-stu-id="f3b86-139">For SSO toowork, Azure AD needs tooknow hello Cezanne HR software counterpart toohello Azure AD user.</span></span> <span data-ttu-id="f3b86-140">Em outras palavras, você deve estabelecer uma relação de link entre um usuário do AD do Azure e o usuário relacionado Olá no hello HR Cezanne software.</span><span class="sxs-lookup"><span data-stu-id="f3b86-140">In other words, you must establish a link relationship between an Azure AD user and hello related user in hello Cezanne HR software.</span></span>

<span data-ttu-id="f3b86-141">relação de link tooestablish hello, atribuir Olá software HR Cezanne **nome de usuário** valor como Olá AD do Azure **Username** valor.</span><span class="sxs-lookup"><span data-stu-id="f3b86-141">tooestablish hello link relationship, assign hello Cezanne HR software **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="f3b86-142">tooconfigure e teste SSO de AD do Azure usando o software de RH Cezanne, Olá completa blocos de construção a seguir.</span><span class="sxs-lookup"><span data-stu-id="f3b86-142">tooconfigure and test Azure AD SSO by using Cezanne HR software, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="f3b86-143">Configurar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3b86-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="f3b86-144">Nesta seção, você pode habilitar o SSO do AD do Azure no portal do Azure de saudação e configurar SSO no seu aplicativo HR Cezanne fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="f3b86-144">In this section, you can enable Azure AD SSO in hello Azure portal and configure SSO in your Cezanne HR software application by doing hello following:</span></span>

1. <span data-ttu-id="f3b86-145">Em Olá portal do Azure, Olá **Cezanne HR Software** página de integração de aplicativos, selecione **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-145">In hello Azure portal, on hello **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![Olá "Single sign-on" comando][4]

2. <span data-ttu-id="f3b86-147">tooenable SSO, em Olá **o logon único** caixa de diálogo, selecione Olá **modo** como **baseado no SAML logon**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-147">tooenable SSO, in hello **Single sign-on** dialog box, select hello **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![caixa de "Modo de" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="f3b86-149">Em **Cezanne HR Software domínio e URLs**, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3b86-149">Under **Cezanne HR Software Domain and URLs**, do hello following:</span></span>

    ![Olá seção "Cezanne HR Software e URLs de domínio"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="f3b86-151">a.</span><span class="sxs-lookup"><span data-stu-id="f3b86-151">a.</span></span> <span data-ttu-id="f3b86-152">Em Olá **URL de logon** caixa, digite uma URL que tem Olá a sintaxe a seguir:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="f3b86-152">In hello **Sign-on URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="f3b86-153">b.</span><span class="sxs-lookup"><span data-stu-id="f3b86-153">b.</span></span> <span data-ttu-id="f3b86-154">Em Olá **URL de resposta** caixa, digite uma URL que tem Olá a sintaxe a seguir:`https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="f3b86-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="f3b86-155">Olá valores anteriores não são reais.</span><span class="sxs-lookup"><span data-stu-id="f3b86-155">hello preceding values are not real.</span></span> <span data-ttu-id="f3b86-156">Atualizá-las com a URL de resposta real hello e URL de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="f3b86-156">Update them with hello actual reply URL and hello sign-on URL.</span></span> <span data-ttu-id="f3b86-157">valores tooobtain Olá Olá contato [Cezanne HR equipe de suporte de cliente de software](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="f3b86-157">tooobtain hello values, contact hello [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="f3b86-158">Em **o certificado de autenticação SAML**, selecione **certificado (Base64)**e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f3b86-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Olá seção de "Certificado de autenticação SAML"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="f3b86-160">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-160">Select **Save**.</span></span>

    ![botão de "Salvar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="f3b86-162">Em **a configuração de Software de RH Cezanne**, selecione **configurar Software de RH Cezanne** tooopen Olá **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="f3b86-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="f3b86-163">Saudação de cópia **ID da entidade SAML** e **serviço de logon único SAML** URL da saudação **referência rápida** seção.</span><span class="sxs-lookup"><span data-stu-id="f3b86-163">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service** URL from hello **Quick Reference** section.</span></span>

    ![Olá seção "Configuração de Software de RH Cezanne"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="f3b86-165">Em uma janela de navegador web diferente, faça logon no locatário do software de RH Cezanne tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="f3b86-165">In a different web browser window, sign on tooyour Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="f3b86-166">No painel esquerdo do hello, selecione **configuração do sistema**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-166">In hello left pane, select **System Setup**.</span></span> <span data-ttu-id="f3b86-167">Selecione **Configurações de Segurança** > **Configuração de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![link de "Única configuração de logon" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="f3b86-169">Em Olá **permitem que os usuários toolog usando Olá serviços Single Sign-On (SSO) a seguir** painel, selecione Olá **SAML 2.0** caixa de seleção e selecione Olá **configuração avançada de** opção.</span><span class="sxs-lookup"><span data-stu-id="f3b86-169">In hello **Allow users toolog in using hello following Single Sign-On (SSO) services** pane, select hello **SAML 2.0** check box and select hello **Advanced Configuration** option.</span></span>

    ![Opções de logon único em serviços](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="f3b86-171">Selecione **Adicionar Novo**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-171">Select **Add New**.</span></span>

    ![botão "Adicionar novo" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="f3b86-173">Em **provedores de identidade SAML 2.0**, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3b86-173">Under **SAML 2.0 Identity Providers**, do hello following:</span></span>

    ![Olá seção "Provedores de identidade do SAML 2.0"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="f3b86-175">a.</span><span class="sxs-lookup"><span data-stu-id="f3b86-175">a.</span></span> <span data-ttu-id="f3b86-176">Em Olá **nome de exibição** , digite o nome de saudação do seu provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="f3b86-176">In hello **Display Name** box, enter hello name of your identity provider.</span></span>

    <span data-ttu-id="f3b86-177">b.</span><span class="sxs-lookup"><span data-stu-id="f3b86-177">b.</span></span> <span data-ttu-id="f3b86-178">Em Olá **identificador da entidade** caixa, cole Olá **ID da entidade SAML** que você copiou da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3b86-178">In hello **Entity Identifier** box, paste hello **SAML Entity ID** that you copied from hello Azure portal.</span></span> 

    <span data-ttu-id="f3b86-179">c.</span><span class="sxs-lookup"><span data-stu-id="f3b86-179">c.</span></span> <span data-ttu-id="f3b86-180">Em Olá **SAML associação** caixa de listagem, selecione **POST**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-180">In hello **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="f3b86-181">d.</span><span class="sxs-lookup"><span data-stu-id="f3b86-181">d.</span></span> <span data-ttu-id="f3b86-182">Em Olá **ponto de extremidade de serviço de Token de segurança** caixa, cole Olá **serviço de logon único SAML** URL que você copiou da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3b86-182">In hello **Security Token Service Endpoint** box, paste hello **SAML Single Sign-On Service** URL that you copied from hello Azure portal.</span></span> 
    
    <span data-ttu-id="f3b86-183">e.</span><span class="sxs-lookup"><span data-stu-id="f3b86-183">e.</span></span> <span data-ttu-id="f3b86-184">Em Olá **nome do atributo de ID de usuário** , digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="f3b86-184">In hello **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="f3b86-185">f.</span><span class="sxs-lookup"><span data-stu-id="f3b86-185">f.</span></span> <span data-ttu-id="f3b86-186">Olá tooupload baixado o certificado do AD do Azure, selecione Olá **carregar** botão.</span><span class="sxs-lookup"><span data-stu-id="f3b86-186">tooupload hello downloaded certificate from Azure AD, select hello **Upload** button.</span></span>
    
    <span data-ttu-id="f3b86-187">g.</span><span class="sxs-lookup"><span data-stu-id="f3b86-187">g.</span></span> <span data-ttu-id="f3b86-188">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-188">Select **OK**.</span></span> 

12. <span data-ttu-id="f3b86-189">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-189">Select **Save**.</span></span>

    ![botão de "Salvar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="f3b86-191">Como configurar o aplicativo hello, você pode ler uma versão concisa do hello precedem instruções em Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f3b86-191">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f3b86-192">Depois de adicionar o aplicativo hello da saudação **do Active Directory** > **aplicativos empresariais** seção, selecione Olá **o logon único** guia. Então Olá acesso incorporado documentação da saudação **configuração** seção.</span><span class="sxs-lookup"><span data-stu-id="f3b86-192">After you add hello app from hello **Active Directory** > **Enterprise applications** section, select hello **Single sign-on** tab. Then access hello embedded documentation from hello **Configuration** section.</span></span> 

<span data-ttu-id="f3b86-193">toolearn mais sobre o recurso de documentação do embedded hello, consulte [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="f3b86-193">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f3b86-194">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3b86-194">Create an Azure AD test user</span></span>
<span data-ttu-id="f3b86-195">Nesta seção, você cria o usuário de teste Britta Simon em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3b86-195">In this section, you create test user Britta Simon in hello Azure portal.</span></span>

![usuário de teste Olá Britta Simon][100]

<span data-ttu-id="f3b86-197">toocreate um usuário de teste no AD do Azure, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3b86-197">toocreate a test user in Azure AD, do hello following:</span></span>

1. <span data-ttu-id="f3b86-198">Em Olá **portal do Azure**, no hello painel esquerdo, selecione Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="f3b86-198">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![botão de "Active Directory do Azure" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f3b86-200">lista de saudação do toodisplay de usuários, selecionados **usuários e grupos** > **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-200">toodisplay hello list of users, select **Users and groups** > **All users**.</span></span>
    
    ![Olá link de "Todos os usuários"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="f3b86-202">Olá **todos os usuários** caixa de diálogo é aberta.</span><span class="sxs-lookup"><span data-stu-id="f3b86-202">hello **All users** dialog box opens.</span></span>

3. <span data-ttu-id="f3b86-203">Olá tooopen **usuário** caixa de diálogo, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-203">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![botão de "Adicionar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f3b86-205">Em Olá **usuário** caixa de diálogo caixa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3b86-205">In hello **User** dialog box, do hello following:</span></span>
 
    ![caixa de diálogo de "Usuário" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f3b86-207">a.</span><span class="sxs-lookup"><span data-stu-id="f3b86-207">a.</span></span> <span data-ttu-id="f3b86-208">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f3b86-209">b.</span><span class="sxs-lookup"><span data-stu-id="f3b86-209">b.</span></span> <span data-ttu-id="f3b86-210">Em Olá **nome de usuário** caixa, digite o usuário Britta Simon **endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-210">In hello **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="f3b86-211">c.</span><span class="sxs-lookup"><span data-stu-id="f3b86-211">c.</span></span> <span data-ttu-id="f3b86-212">Selecione Olá **Mostrar senha** caixa de seleção e valor de saudação Observação que foi gerado em Olá **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="f3b86-212">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="f3b86-213">d.</span><span class="sxs-lookup"><span data-stu-id="f3b86-213">d.</span></span> <span data-ttu-id="f3b86-214">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="f3b86-215">Criar um usuário de teste do software Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="f3b86-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="f3b86-216">toosign de usuários tooenable AD do Azure no software tooCezanne HR, eles devem ser provisionados no software de RH Cezanne.</span><span class="sxs-lookup"><span data-stu-id="f3b86-216">tooenable Azure AD users toosign in tooCezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="f3b86-217">No caso de saudação de RH Cezanne software, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="f3b86-217">In hello case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="f3b86-218">Provisione uma conta de usuário fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="f3b86-218">Provision a user account by doing hello following:</span></span>

1.  <span data-ttu-id="f3b86-219">Entre no tooyour Cezanne HR site da empresa de software como um administrador.</span><span class="sxs-lookup"><span data-stu-id="f3b86-219">Sign in tooyour Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="f3b86-220">No painel esquerdo do hello, selecione **configuração do sistema** > **gerenciar usuários** > **adicionar novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-220">In hello left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="f3b86-221">![link de "Adicionar novo usuário" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "novo usuário")</span><span class="sxs-lookup"><span data-stu-id="f3b86-221">![hello "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="f3b86-222">Em **detalhes da pessoa**, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3b86-222">Under **Person Details**, do hello following:</span></span>

    <span data-ttu-id="f3b86-223">![Olá pessoa seção "Detalhes"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "novo usuário")</span><span class="sxs-lookup"><span data-stu-id="f3b86-223">![hello "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="f3b86-224">a.</span><span class="sxs-lookup"><span data-stu-id="f3b86-224">a.</span></span> <span data-ttu-id="f3b86-225">Defina **Internal User (Usuário Interno)** como **OFF (DESATIVADO)**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="f3b86-226">b.</span><span class="sxs-lookup"><span data-stu-id="f3b86-226">b.</span></span> <span data-ttu-id="f3b86-227">Em Olá **nome** caixa, tipo hello nome do usuário, por exemplo, **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-227">In hello **First Name** box, type hello user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="f3b86-228">c.</span><span class="sxs-lookup"><span data-stu-id="f3b86-228">c.</span></span> <span data-ttu-id="f3b86-229">Em Olá **Sobrenome** caixa, tipo hello sobrenome do usuário, por exemplo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-229">In hello **Last Name** box, type hello user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="f3b86-230">d.</span><span class="sxs-lookup"><span data-stu-id="f3b86-230">d.</span></span> <span data-ttu-id="f3b86-231">Em Olá **email** , digite o endereço de email do usuário hello, por exemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f3b86-231">In hello **E-mail** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="f3b86-232">Em **informações de conta**, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f3b86-232">Under **Account Information**, do hello following:</span></span>

    <span data-ttu-id="f3b86-233">![Olá seção "Informações de conta"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "novo usuário")</span><span class="sxs-lookup"><span data-stu-id="f3b86-233">![hello "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="f3b86-234">a.</span><span class="sxs-lookup"><span data-stu-id="f3b86-234">a.</span></span> <span data-ttu-id="f3b86-235">Em Olá **Username** , digite o endereço de email do usuário hello, por exemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f3b86-235">In hello **Username** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="f3b86-236">b.</span><span class="sxs-lookup"><span data-stu-id="f3b86-236">b.</span></span> <span data-ttu-id="f3b86-237">Em Olá **senha** , digite a senha do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="f3b86-237">In hello **Password** box, type hello user's password.</span></span>
    
    <span data-ttu-id="f3b86-238">c.</span><span class="sxs-lookup"><span data-stu-id="f3b86-238">c.</span></span> <span data-ttu-id="f3b86-239">Em Olá **função de segurança** selecione **HR Professional**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-239">In hello **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="f3b86-240">d.</span><span class="sxs-lookup"><span data-stu-id="f3b86-240">d.</span></span> <span data-ttu-id="f3b86-241">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-241">Select **OK**.</span></span>

5. <span data-ttu-id="f3b86-242">Em Olá **o logon único** guia Olá **SAML 2.0 identificadores** seção, selecione **adicionar novo**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-242">On hello **Single sign-on** tab, in hello **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="f3b86-243">![botão "Adicionar novo" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "usuário")</span><span class="sxs-lookup"><span data-stu-id="f3b86-243">![hello "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="f3b86-244">Em Olá **provedor de identidade** caixa de listagem, selecione seu provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="f3b86-244">In hello **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="f3b86-245">Em Olá **identificador de usuário** , digite o endereço de email Olá para conta de teste usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f3b86-245">In hello **User Identifier** box, enter hello email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="f3b86-246">![Olá caixas "Provedor de identidade" e "Identificador de usuário"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "usuário")</span><span class="sxs-lookup"><span data-stu-id="f3b86-246">![hello "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="f3b86-247">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-247">Select **Save**.</span></span>

    <span data-ttu-id="f3b86-248">![botão de "Salvar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "usuário")</span><span class="sxs-lookup"><span data-stu-id="f3b86-248">![hello "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f3b86-249">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f3b86-249">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f3b86-250">Nesta seção, você permitir que o usuário de teste Britta Simon toouse SSO do Azure, concedendo acesso tooCezanne HR software.</span><span class="sxs-lookup"><span data-stu-id="f3b86-250">In this section, you enable test user Britta Simon toouse Azure SSO by granting access tooCezanne HR software.</span></span>

![Testar o acesso do usuário][200] 

1. <span data-ttu-id="f3b86-252">No portal do Azure de Olá, abrir modo de exibição de aplicativos hello e vá toohello exibição de diretório.</span><span class="sxs-lookup"><span data-stu-id="f3b86-252">In hello Azure portal, open hello applications view and then go toohello directory view.</span></span> <span data-ttu-id="f3b86-253">Selecione **Aplicativos empresariais** > **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![Olá link de "Todos os aplicativos"][201] 

2. <span data-ttu-id="f3b86-255">Na lista de aplicativos hello, selecione **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-255">In hello applications list, select **Cezanne HR Software**.</span></span>

    ![lista de "Aplicativos" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="f3b86-257">No menu Olá Olá esquerda, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-257">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f3b86-259">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-259">Select **Add**.</span></span> <span data-ttu-id="f3b86-260">Em seguida, em Olá **Adicionar atribuição** caixa de diálogo, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-260">Then in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Link “Usuários e Grupos”][203]

5. <span data-ttu-id="f3b86-262">Em Olá **usuários e grupos** caixa de diálogo Olá **usuários** lista, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-262">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="f3b86-263">Em Olá **usuários e grupos** caixa de diálogo, selecione **selecione**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-263">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="f3b86-264">Em Olá **Adicionar atribuição** caixa de diálogo, selecione **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="f3b86-264">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="f3b86-265">Testar o SSO</span><span class="sxs-lookup"><span data-stu-id="f3b86-265">Test SSO</span></span>

<span data-ttu-id="f3b86-266">Nesta seção, você pode testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3b86-266">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="f3b86-267">Quando você seleciona o bloco de software de RH Cezanne Olá no painel de acesso de saudação, logon automaticamente tooyour HR Cezanne aplicativo de software.</span><span class="sxs-lookup"><span data-stu-id="f3b86-267">When you select hello Cezanne HR software tile in hello Access Panel, you sign on automatically tooyour Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3b86-268">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f3b86-268">Next steps</span></span>

* [<span data-ttu-id="f3b86-269">Lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f3b86-269">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f3b86-270">O que é acesso a aplicativos e SSO com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f3b86-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

