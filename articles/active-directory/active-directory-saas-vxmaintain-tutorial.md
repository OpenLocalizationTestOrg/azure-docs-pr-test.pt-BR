---
title: "Tutorial: Integração do Azure Active Directory ao vxMaintain | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e vxMaintain."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="1a904-103">Tutorial: Integração do Azure Active Directory ao vxMaintain</span><span class="sxs-lookup"><span data-stu-id="1a904-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="1a904-104">Neste tutorial, você aprenderá como vxMaintain toointegrate com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="1a904-104">In this tutorial, you learn how toointegrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a904-105">Essa integração oferece vários benefícios importantes.</span><span class="sxs-lookup"><span data-stu-id="1a904-105">This integration provides several important benefits.</span></span> <span data-ttu-id="1a904-106">Você pode:</span><span class="sxs-lookup"><span data-stu-id="1a904-106">You can:</span></span>

- <span data-ttu-id="1a904-107">Controle no AD do Azure que tenha acesso toovxMaintain.</span><span class="sxs-lookup"><span data-stu-id="1a904-107">Control in Azure AD who has access toovxMaintain.</span></span>
- <span data-ttu-id="1a904-108">Habilite seus usuários de entrada tooautomatically toovxMaintain com logon único (SSO) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a904-108">Enable your users tooautomatically sign in toovxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="1a904-109">Gerenciar suas contas em um local central: Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a904-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="1a904-110">toolearn mais sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1a904-110">toolearn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a904-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1a904-111">Prerequisites</span></span>

<span data-ttu-id="1a904-112">tooconfigure integração do AD do Azure com vxMaintain, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a904-112">tooconfigure Azure AD integration with vxMaintain, you need hello following items:</span></span>

- <span data-ttu-id="1a904-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1a904-113">An Azure AD subscription</span></span>
- <span data-ttu-id="1a904-114">Uma assinatura habilitada pelo SSO do vxMaintain</span><span class="sxs-lookup"><span data-stu-id="1a904-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a904-115">Quando você testar etapas Olá neste tutorial, é recomendável que você não use um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1a904-115">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="1a904-116">etapas de saudação tootest neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1a904-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="1a904-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1a904-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a904-118">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a904-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a904-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1a904-119">Scenario description</span></span>
<span data-ttu-id="1a904-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1a904-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="1a904-121">cenário de saudação que este tutorial descreve consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="1a904-121">hello scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="1a904-122">Adicionando vxMaintain da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1a904-122">Adding vxMaintain from hello gallery</span></span>
* <span data-ttu-id="1a904-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1a904-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-hello-gallery"></a><span data-ttu-id="1a904-124">Adicionar vxMaintain da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1a904-124">Add vxMaintain from hello gallery</span></span>
<span data-ttu-id="1a904-125">integração de saudação do tooconfigure do vxMaintain com o Azure AD, é necessário vxMaintain tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1a904-125">tooconfigure hello integration of vxMaintain with Azure AD, you need tooadd vxMaintain from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1a904-126">vxMaintain tooadd da Galeria de Olá Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a904-126">tooadd vxMaintain from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="1a904-127">Em Olá [portal do Azure](https://portal.azure.com), no hello painel esquerdo, selecione Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="1a904-127">In hello [Azure portal](https://portal.azure.com), in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="1a904-129">Selecione **Aplicativos empresariais** > **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1a904-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Painel de "Aplicativos corporativos" Hello][2]
    
3. <span data-ttu-id="1a904-131">tooadd um aplicativo, em Olá **todos os aplicativos** caixa de diálogo, selecione **novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="1a904-131">tooadd an application, in hello **All applications** dialog box, select **New application**.</span></span>

    ![Olá "Novo application" botão][3]

4. <span data-ttu-id="1a904-133">Na caixa de pesquisa hello, digite **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="1a904-133">In hello search box, type **vxMaintain**.</span></span>

    ![lista de suspensa Hello "Único modo de logon"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="1a904-135">Na lista de resultados de saudação, selecione **vxMaintain**e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1a904-135">In hello results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![link de vxMaintain Olá](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1a904-137">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a904-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1a904-138">Nesta seção, você configurará e testará o SSO do Azure AD usando o vxMaintain, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="1a904-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1a904-139">Para SSO toowork, AD do Azure precisa de usuário do AD do Azure do tooknow Olá vxMaintain contraparte toohello.</span><span class="sxs-lookup"><span data-stu-id="1a904-139">For SSO toowork, Azure AD needs tooknow hello vxMaintain counterpart toohello Azure AD user.</span></span> <span data-ttu-id="1a904-140">Ou seja, você deve estabelecer uma relação de link entre usuários do AD do Azure hello e usuário vxMaintain correspondente de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a904-140">That is, you must establish a link relationship between hello Azure AD user and hello corresponding vxMaintain user.</span></span>

<span data-ttu-id="1a904-141">relação de link tooestablish hello, atribuir Olá vxMaintain **nome de usuário** valor como Olá AD do Azure **Username** valor.</span><span class="sxs-lookup"><span data-stu-id="1a904-141">tooestablish hello link relationship, assign hello vxMaintain **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="1a904-142">tooconfigure e teste SSO de AD do Azure usando vxMaintain, Olá completa blocos de construção a seguir.</span><span class="sxs-lookup"><span data-stu-id="1a904-142">tooconfigure and test Azure AD SSO by using vxMaintain, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="1a904-143">Configurar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a904-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="1a904-144">Nesta seção, você pode habilitar o SSO do AD do Azure no portal do Azure de saudação e configurar SSO em seu aplicativo vxMaintain fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="1a904-144">In this section, you can both enable Azure AD SSO in hello Azure portal and configure SSO in your vxMaintain application by doing hello following:</span></span>

1. <span data-ttu-id="1a904-145">Em Olá portal do Azure, Olá **vxMaintain** página de integração de aplicativos, selecione **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="1a904-145">In hello Azure portal, on hello **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![Olá "Single sign-on" comando][4]

2. <span data-ttu-id="1a904-147">tooenable SSO, em Olá **modo de logon único** lista suspensa, selecione **baseado no SAML logon**.</span><span class="sxs-lookup"><span data-stu-id="1a904-147">tooenable SSO, in hello **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![Olá "baseado em SAML logon" comando](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="1a904-149">Em **vxMaintain domínio e URLs**, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a904-149">Under **vxMaintain Domain and URLs**, do hello following:</span></span>

    ![Olá vxMaintain seção URLs e de domínio](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="1a904-151">a.</span><span class="sxs-lookup"><span data-stu-id="1a904-151">a.</span></span> <span data-ttu-id="1a904-152">Em Olá **identificador** caixa, digite uma URL que tem Olá a sintaxe a seguir:`https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="1a904-152">In hello **Identifier** box, type a URL that has hello following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="1a904-153">b.</span><span class="sxs-lookup"><span data-stu-id="1a904-153">b.</span></span> <span data-ttu-id="1a904-154">Em Olá **URL de resposta** caixa, digite uma URL que tem Olá a sintaxe a seguir:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="1a904-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1a904-155">Olá valores anteriores não são reais.</span><span class="sxs-lookup"><span data-stu-id="1a904-155">hello preceding values are not real.</span></span> <span data-ttu-id="1a904-156">Atualizá-los com o identificador real hello e URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="1a904-156">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="1a904-157">valores tooobtain Olá Olá contato [a equipe de suporte vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="1a904-157">tooobtain hello values, contact hello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="1a904-158">Em **o certificado de autenticação SAML**, selecione **Metadata XML**e, em seguida, salve o computador de tooyour de arquivo de metadados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a904-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file tooyour computer.</span></span>

    ![Olá seção de "Certificado de autenticação SAML"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="1a904-160">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1a904-160">Select **Save**.</span></span>

    ![botão de salvar Olá](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1a904-162">tooconfigure **vxMaintain** SSO, Olá envio baixado **Metadata XML** arquivo toohello [a equipe de suporte vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="1a904-162">tooconfigure **vxMaintain** SSO, send hello downloaded **Metadata XML** file toohello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="1a904-163">Como configurar o aplicativo hello, você pode ler uma versão concisa do hello precedem instruções em Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1a904-163">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1a904-164">Depois de adicionar o aplicativo hello da saudação **do Active Directory** > **aplicativos empresariais** seção, selecione Olá **Single Sign-On** guia e, em seguida, Olá de acesso incorporado a documentação de saudação **configuração** seção.</span><span class="sxs-lookup"><span data-stu-id="1a904-164">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab, and then access hello embedded documentation from hello **Configuration** section.</span></span> 
>
><span data-ttu-id="1a904-165">toolearn mais sobre o recurso de documentação do embedded hello, consulte [gerenciar logon único para aplicativos corporativos](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="1a904-165">toolearn more about hello embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1a904-166">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a904-166">Create an Azure AD test user</span></span>
<span data-ttu-id="1a904-167">Nesta seção, você pode criar Britta Simon de usuário de teste no portal do Azure de saudação fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="1a904-167">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![usuário de teste de saudação do AD do Azure][100]

1. <span data-ttu-id="1a904-169">Em Olá **portal do Azure**, no hello painel esquerdo, selecione Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="1a904-169">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![botão de "Active Directory do Azure" Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1a904-171">toodisplay uma lista de usuários, vá muito**usuários e grupos** > **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="1a904-171">toodisplay a list of users, go too**Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="1a904-172">![Olá link de "Todos os usuários"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="1a904-172">![hello "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="1a904-173">Olá **todos os usuários** caixa de diálogo é aberta.</span><span class="sxs-lookup"><span data-stu-id="1a904-173">hello **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="1a904-174">Olá tooopen **usuário** caixa de diálogo, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1a904-174">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![botão Adicionar de saudação](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1a904-176">Em Olá **usuário** caixa de diálogo caixa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a904-176">In hello **User** dialog box, do hello following:</span></span>
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a904-178">a.</span><span class="sxs-lookup"><span data-stu-id="1a904-178">a.</span></span> <span data-ttu-id="1a904-179">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a904-179">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a904-180">b.</span><span class="sxs-lookup"><span data-stu-id="1a904-180">b.</span></span> <span data-ttu-id="1a904-181">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário de teste Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a904-181">In hello **User name** box, type hello email address of test user Britta Simon.</span></span>

    <span data-ttu-id="1a904-182">c.</span><span class="sxs-lookup"><span data-stu-id="1a904-182">c.</span></span> <span data-ttu-id="1a904-183">Selecione Olá **Mostrar senha** caixa de seleção e valor de saudação Observação que foi gerado em Olá **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="1a904-183">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="1a904-184">d.</span><span class="sxs-lookup"><span data-stu-id="1a904-184">d.</span></span> <span data-ttu-id="1a904-185">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1a904-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="1a904-186">Criar um usuário de teste vxMaintain</span><span class="sxs-lookup"><span data-stu-id="1a904-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="1a904-187">Nesta seção, você cria a usuária de teste Brenda Fernandes no vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="1a904-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="1a904-188">os usuários de tooadd na plataforma de vxMaintain hello, trabalhar com o [a equipe de suporte vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="1a904-188">tooadd users in hello vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="1a904-189">Antes de usar o SSO, criar e ativar usuários hello.</span><span class="sxs-lookup"><span data-stu-id="1a904-189">Before you use SSO, create and activate hello users.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1a904-190">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1a904-190">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1a904-191">Nesta seção, você permitir que o usuário de teste Britta Simon toouse SSO do Azure, concedendo acesso toovxMaintain.</span><span class="sxs-lookup"><span data-stu-id="1a904-191">In this section, you enable test user Britta Simon toouse Azure SSO by granting access toovxMaintain.</span></span> <span data-ttu-id="1a904-192">toodo, portanto, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a904-192">toodo so, do hello following:</span></span>

![Usuário de teste na lista de nomes de exibição de saudação][200] 

1. <span data-ttu-id="1a904-194">No portal do Azure de saudação **aplicativos** exibir, vá muito**diretório** exibição > **aplicativos empresariais** > **detodososaplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1a904-194">In hello Azure portal **Applications** view, go too**Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![Olá link de "Todos os aplicativos"][201] 

2. <span data-ttu-id="1a904-196">Em Olá **aplicativos** lista, selecione **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="1a904-196">In hello **Applications** list, select **vxMaintain**.</span></span>

    ![link de vxMaintain Olá](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="1a904-198">No painel esquerdo do hello, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1a904-198">In hello left pane, select **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202] 

4. <span data-ttu-id="1a904-200">Selecione **adicionar** e, em seguida, em Olá **Adicionar atribuição** painel, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1a904-200">Select **Add** and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][203]

5. <span data-ttu-id="1a904-202">Em Olá **usuários e grupos** caixa de diálogo Olá **usuários** lista, selecione **Britta Simon**e, em seguida, selecione Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="1a904-202">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**, and then select hello **Select** button.</span></span>

7. <span data-ttu-id="1a904-203">Em Olá **Adicionar atribuição** caixa de diálogo, selecione **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="1a904-203">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="1a904-204">Testar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a904-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="1a904-205">Nesta seção, você pode testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a904-205">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="1a904-206">Olá selecionando **vxMaintain** bloco no painel de acesso de saudação deve entrar no aplicativo de vxMaintain tooyour automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1a904-206">Selecting hello **vxMaintain** tile in hello Access Panel should sign you in tooyour vxMaintain application automatically.</span></span>

<span data-ttu-id="1a904-207">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1a904-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a904-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1a904-208">Next steps</span></span>

* [<span data-ttu-id="1a904-209">Lista de tutoriais sobre como integrar aplicativos SaaS com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a904-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1a904-210">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1a904-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

