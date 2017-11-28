---
title: "Tutorial: Integração do Azure Active Directory ao Sistema de Monitoramento de Temperatura Sem Fio SensoScientific | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o sistema de monitoramento de temperatura do SensoScientific sem fio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="51f16-103">Tutorial: Integração do Azure Active Directory ao Sistema de Monitoramento de Temperatura Sem Fio SensoScientific</span><span class="sxs-lookup"><span data-stu-id="51f16-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="51f16-104">Neste tutorial, você aprenderá como toointegrate a sistema de monitoramento de temperatura SensoScientific sem fio com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="51f16-104">In this tutorial, you learn how toointegrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="51f16-105">Integração do sistema de monitoramento de temperatura do SensoScientific sem fio com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="51f16-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="51f16-106">Você pode controlar no AD do Azure que tenha acesso tooSensoScientific sistema de monitoramento de temperatura sem fio</span><span class="sxs-lookup"><span data-stu-id="51f16-106">You can control in Azure AD who has access tooSensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="51f16-107">Você pode habilitar seu usuários tooautomatically get conectado tooSensoScientific sistema de monitoramento de temperatura sem fio (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="51f16-107">You can enable your users tooautomatically get signed-on tooSensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="51f16-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="51f16-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="51f16-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="51f16-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51f16-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="51f16-110">Prerequisites</span></span>

<span data-ttu-id="51f16-111">tooconfigure integração do AD do Azure com o sistema de monitoramento de temperatura do SensoScientific sem fio, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="51f16-111">tooconfigure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need hello following items:</span></span>

- <span data-ttu-id="51f16-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="51f16-112">An Azure AD subscription</span></span>
- <span data-ttu-id="51f16-113">Uma assinatura do Sistema de Monitoramento de Temperatura Sem Fio SensoScientific habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="51f16-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="51f16-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="51f16-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="51f16-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="51f16-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="51f16-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="51f16-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="51f16-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="51f16-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="51f16-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="51f16-118">Scenario description</span></span>
<span data-ttu-id="51f16-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="51f16-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="51f16-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="51f16-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="51f16-121">Adicionando o sistema de monitoramento de temperatura do SensoScientific sem fio da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="51f16-121">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
2. <span data-ttu-id="51f16-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="51f16-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a><span data-ttu-id="51f16-123">Adicionando o sistema de monitoramento de temperatura do SensoScientific sem fio da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="51f16-123">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
<span data-ttu-id="51f16-124">integração de saudação tooconfigure do sistema de monitoramento de temperatura do SensoScientific sem fio no AD do Azure, você precisa tooadd sistema de monitoramento de temperatura do SensoScientific sem fio na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="51f16-124">tooconfigure hello integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="51f16-125">**tooadd a sistema de monitoramento de temperatura SensoScientific sem fio da Galeria Olá, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="51f16-125">**tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="51f16-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="51f16-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="51f16-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="51f16-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="51f16-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="51f16-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="51f16-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="51f16-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="51f16-133">Na caixa de pesquisa hello, digite **sistema de monitoramento de temperatura do SensoScientific sem fio**.</span><span class="sxs-lookup"><span data-stu-id="51f16-133">In hello search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="51f16-135">No painel de resultados de saudação, selecione **sistema de monitoramento de temperatura do SensoScientific sem fio**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="51f16-135">In hello results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="51f16-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="51f16-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="51f16-138">Nesta seção, você configura e testa o logon único do Azure AD com o Sistema de Monitoramento de Temperatura Sem Fio SensoScientific com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="51f16-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="51f16-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no sistema de monitoramento de temperatura do SensoScientific sem fio é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="51f16-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SensoScientific Wireless Temperature Monitoring System is tooa user in Azure AD.</span></span> <span data-ttu-id="51f16-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no sistema de monitoramento de temperatura do SensoScientific sem fio precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="51f16-140">In other words, a link relationship between an Azure AD user and hello related user in SensoScientific Wireless Temperature Monitoring System needs toobe established.</span></span>

<span data-ttu-id="51f16-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no sistema de monitoramento de temperatura do SensoScientific sem fio.</span><span class="sxs-lookup"><span data-stu-id="51f16-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="51f16-142">tooconfigure e teste de logon único do AD do Azure com o sistema de monitoramento de temperatura do SensoScientific sem fio, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="51f16-142">tooconfigure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="51f16-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="51f16-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="51f16-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="51f16-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="51f16-145">**[Criar um usuário de teste do sistema de monitoramento de temperatura do SensoScientific sem fio](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave um equivalente de Britta Simon SensoScientific sem fio temperatura monitoramento de sistema que é vinculado a representação toohello AD do Azure de usuário.</span><span class="sxs-lookup"><span data-stu-id="51f16-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - toohave a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="51f16-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="51f16-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="51f16-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="51f16-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="51f16-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="51f16-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="51f16-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de sistema de monitoramento de temperatura do SensoScientific sem fio.</span><span class="sxs-lookup"><span data-stu-id="51f16-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="51f16-150">**tooconfigure logon único do AD do Azure com SensoScientific sem fio temperatura monitoramento de sistema, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="51f16-150">**tooconfigure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="51f16-151">Em Olá portal do Azure, Olá **sistema de monitoramento de temperatura do SensoScientific sem fio** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="51f16-151">In hello Azure portal, on hello **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="51f16-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="51f16-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="51f16-155">Em Olá **SensoScientific sem fio temperatura monitoramento de sistema de domínio e URLs** seção tooperform sem necessidade de que todas as etapas de como o aplicativo hello previamente já está integrado com o Azure:</span><span class="sxs-lookup"><span data-stu-id="51f16-155">On hello **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need tooperform any steps as hello app is already pre-integrated with Azure:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="51f16-157">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="51f16-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="51f16-159">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="51f16-159">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="51f16-161">Em Olá **configuração de sistema de monitoramento do SensoScientific sem fio temperatura** seção, clique em **configurar SensoScientific sem fio temperatura monitoramento sistema** tooopen  **Configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="51f16-161">On hello **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="51f16-162">Saudação de cópia **URL de logout, ID da entidade SAML** e **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="51f16-162">Copy hello **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="51f16-164">Logon tooyour aplicativo de sistema de monitoramento de temperatura do SensoScientific sem fio como um administrador.</span><span class="sxs-lookup"><span data-stu-id="51f16-164">Sign on tooyour SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="51f16-165">No menu de navegação de saudação na parte superior do hello, clique em **configuração** e goto **configurar** em **Single Sign On** tooopen Olá logon único.</span><span class="sxs-lookup"><span data-stu-id="51f16-165">In hello navigation menu on hello top, click **Configuration** and goto **Configure** under **Single Sign On** tooopen hello Single Sign On Settings.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="51f16-167">Em **logon único** formulário executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="51f16-167">In **Single Sign On Settings** form perform hello following steps:</span></span>
 
    <span data-ttu-id="51f16-168">a.</span><span class="sxs-lookup"><span data-stu-id="51f16-168">a.</span></span> <span data-ttu-id="51f16-169">Selecione **Nome do Emissor** como Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51f16-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="51f16-170">b.</span><span class="sxs-lookup"><span data-stu-id="51f16-170">b.</span></span> <span data-ttu-id="51f16-171">Saudação de colar **ID da entidade SAML** que você copiou do portal do Azure na caixa de texto URL do emissor.</span><span class="sxs-lookup"><span data-stu-id="51f16-171">Paste hello **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="51f16-172">c.</span><span class="sxs-lookup"><span data-stu-id="51f16-172">c.</span></span> <span data-ttu-id="51f16-173">Saudação de colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure na caixa de texto o URL de serviço logon único.</span><span class="sxs-lookup"><span data-stu-id="51f16-173">Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="51f16-174">d.</span><span class="sxs-lookup"><span data-stu-id="51f16-174">d.</span></span> <span data-ttu-id="51f16-175">Saudação de colar **URL de logout** que você copiou do portal do Azure na caixa de texto URL de serviço de logon único.</span><span class="sxs-lookup"><span data-stu-id="51f16-175">Paste hello **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="51f16-176">e.</span><span class="sxs-lookup"><span data-stu-id="51f16-176">e.</span></span> <span data-ttu-id="51f16-177">Procure o certificado de saudação que você baixou do portal do Azure e carregar aqui.</span><span class="sxs-lookup"><span data-stu-id="51f16-177">Browse hello certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="51f16-178">f.</span><span class="sxs-lookup"><span data-stu-id="51f16-178">f.</span></span> <span data-ttu-id="51f16-179">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="51f16-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="51f16-180">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="51f16-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="51f16-181">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="51f16-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="51f16-182">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="51f16-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="51f16-183">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="51f16-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="51f16-184">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="51f16-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="51f16-186">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="51f16-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="51f16-187">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="51f16-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="51f16-189">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="51f16-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="51f16-191">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="51f16-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="51f16-193">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="51f16-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="51f16-195">a.</span><span class="sxs-lookup"><span data-stu-id="51f16-195">a.</span></span> <span data-ttu-id="51f16-196">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="51f16-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="51f16-197">b.</span><span class="sxs-lookup"><span data-stu-id="51f16-197">b.</span></span> <span data-ttu-id="51f16-198">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="51f16-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="51f16-199">c.</span><span class="sxs-lookup"><span data-stu-id="51f16-199">c.</span></span> <span data-ttu-id="51f16-200">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="51f16-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="51f16-201">d.</span><span class="sxs-lookup"><span data-stu-id="51f16-201">d.</span></span> <span data-ttu-id="51f16-202">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="51f16-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="51f16-203">Criando um usuário de teste do Sistema de Monitoramento de Temperatura Sem Fio SensoScientific</span><span class="sxs-lookup"><span data-stu-id="51f16-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="51f16-204">tooenable AD do Azure usuários toolog em tooSensoScientific sistema de monitoramento de temperatura sem fio, eles devem ser provisionados no sistema de monitoramento de temperatura do SensoScientific sem fio.</span><span class="sxs-lookup"><span data-stu-id="51f16-204">tooenable Azure AD users toolog in tooSensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="51f16-205">Trabalhar com [equipe de suporte do sistema de monitoramento de temperatura do SensoScientific sem fio](https://www.sensoscientific.com/contact-us/) para adicionar usuários de saudação na plataforma do sistema de monitoramento de temperatura do SensoScientific sem fio hello.</span><span class="sxs-lookup"><span data-stu-id="51f16-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add hello users in hello SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="51f16-206">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="51f16-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="51f16-207">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="51f16-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="51f16-208">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSensoScientific sistema de monitoramento de temperatura sem fio.</span><span class="sxs-lookup"><span data-stu-id="51f16-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSensoScientific Wireless Temperature Monitoring System.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="51f16-210">**tooassign Britta Simon tooSensoScientific sistema de monitoramento de temperatura de sem fio, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="51f16-210">**tooassign Britta Simon tooSensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="51f16-211">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="51f16-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="51f16-213">Na lista de aplicativos hello, selecione **sistema de monitoramento de temperatura do SensoScientific sem fio**.</span><span class="sxs-lookup"><span data-stu-id="51f16-213">In hello applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="51f16-215">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="51f16-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="51f16-217">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="51f16-217">Click **Add** button.</span></span> <span data-ttu-id="51f16-218">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="51f16-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="51f16-220">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="51f16-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="51f16-221">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="51f16-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="51f16-222">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="51f16-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="51f16-223">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="51f16-223">Testing single sign-on</span></span>

<span data-ttu-id="51f16-224">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="51f16-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="51f16-225">Clique em bloco de sistema de monitoramento de temperatura do SensoScientific sem fio Olá Olá painel de acesso, será automaticamente conectado em tooyour aplicativo de sistema de monitoramento de temperatura do SensoScientific sem fio.</span><span class="sxs-lookup"><span data-stu-id="51f16-225">Click hello SensoScientific Wireless Temperature Monitoring System tile in hello Access Panel, you will be automatically signed-on tooyour SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="51f16-226">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="51f16-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="51f16-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="51f16-227">Additional resources</span></span>

* [<span data-ttu-id="51f16-228">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="51f16-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="51f16-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="51f16-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

