---
title: "Tutorial: Integração do Azure Active Directory ao ServiceNow | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ServiceNow e ServiceNow Express."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="71e85-103">Tutorial: Integração do Active Directory do Azure com o ServiceNow</span><span class="sxs-lookup"><span data-stu-id="71e85-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="71e85-104">Neste tutorial, você aprenderá como toointegrate ServiceNow e ServiceNow Express com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="71e85-104">In this tutorial, you learn how toointegrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71e85-105">Integração do ServiceNow e ServiceNow Express com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="71e85-106">Você pode controlar no AD do Azure que tenha acesso tooServiceNow e Express do ServiceNow</span><span class="sxs-lookup"><span data-stu-id="71e85-106">You can control in Azure AD who has access tooServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="71e85-107">Você pode habilitar seus usuários tooautomatically get conectado tooServiceNow e ServiceNow Express (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="71e85-107">You can enable your users tooautomatically get signed-on tooServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="71e85-108">Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="71e85-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="71e85-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="71e85-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71e85-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="71e85-110">Prerequisites</span></span>
<span data-ttu-id="71e85-111">tooconfigure integração do Azure AD com ServiceNow e ServiceNow Express, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-111">tooconfigure Azure AD integration with ServiceNow and ServiceNow Express, you need hello following items:</span></span>

* <span data-ttu-id="71e85-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="71e85-112">An Azure AD subscription</span></span>
* <span data-ttu-id="71e85-113">Para o ServiceNow, uma instância ou um locatário do ServiceNow, versão Calgary ou superior</span><span class="sxs-lookup"><span data-stu-id="71e85-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="71e85-114">Para o ServiceNow Express, uma instância do ServiceNow Express, versão Helsinki ou superior</span><span class="sxs-lookup"><span data-stu-id="71e85-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="71e85-115">locatário de ServiceNow Olá deve ter Olá [vários provedor única entrada no plug-in](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) habilitado.</span><span class="sxs-lookup"><span data-stu-id="71e85-115">hello ServiceNow tenant must have hello [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="71e85-116">Isso pode ser feito [enviando uma solicitação de serviço](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="71e85-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="71e85-117">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="71e85-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="71e85-118">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="71e85-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="71e85-119">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="71e85-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="71e85-120">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71e85-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="71e85-121">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="71e85-121">Scenario description</span></span>
<span data-ttu-id="71e85-122">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="71e85-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="71e85-123">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="71e85-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71e85-124">Adicionando ServiceNow da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="71e85-124">Adding ServiceNow from hello gallery</span></span>
2. <span data-ttu-id="71e85-125">Configurando e testando o logon único do Azure AD para o ServiceNow ou para o ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="71e85-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-hello-gallery"></a><span data-ttu-id="71e85-126">Adicionando ServiceNow da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="71e85-126">Adding ServiceNow from hello gallery</span></span>
<span data-ttu-id="71e85-127">integração de saudação tooconfigure do ServiceNow ou ServiceNow Express no AD do Azure, você precisa tooadd ServiceNow, na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="71e85-127">tooconfigure hello integration of ServiceNow or ServiceNow Express into Azure AD, you need tooadd ServiceNow from hello gallery tooyour list of managed SaaS apps.</span></span> 

<span data-ttu-id="71e85-128">**tooadd ServiceNow da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="71e85-128">**tooadd ServiceNow from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="71e85-129">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="71e85-129">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="71e85-131">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="71e85-131">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="71e85-132">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="71e85-132">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicativos][2]
4. <span data-ttu-id="71e85-134">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="71e85-134">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicativos][3]
5. <span data-ttu-id="71e85-136">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="71e85-136">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicativos][4]
6. <span data-ttu-id="71e85-138">Na caixa de pesquisa hello, digite **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="71e85-138">In hello search box, type **ServiceNow**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="71e85-140">No painel de resultados de saudação, selecione **ServiceNow**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="71e85-140">In hello results pane, select **ServiceNow**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="71e85-142">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="71e85-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="71e85-143">Nesta seção, você configurará e testará o logon único do Azure AD com o ServiceNow ou o ServiceNow Express, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="71e85-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="71e85-144">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ServiceNow é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="71e85-144">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceNow is tooa user in Azure AD.</span></span> <span data-ttu-id="71e85-145">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no ServiceNow precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="71e85-145">In other words, a link relationship between an Azure AD user and hello related user in ServiceNow needs toobe established.</span></span>
<span data-ttu-id="71e85-146">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="71e85-146">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceNow.</span></span> <span data-ttu-id="71e85-147">tooconfigure e teste de logon único do Azure AD com ServiceNow, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-147">tooconfigure and test Azure AD single sign-on with ServiceNow, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="71e85-148">**[Configurando o Azure AD logon único para ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="71e85-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="71e85-149">**[Configurando o Azure AD logon único para ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="71e85-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - tooenable your users toouse this feature.</span></span>
3. <span data-ttu-id="71e85-150">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71e85-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="71e85-151">**[Criar um usuário de teste do ServiceNow](#creating-a-servicenow-test-user)**  -toohave um equivalente do Britta Simon no ServiceNow é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="71e85-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - toohave a counterpart of Britta Simon in ServiceNow that is linked toohello Azure AD representation of her.</span></span>
5. <span data-ttu-id="71e85-152">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="71e85-152">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="71e85-153">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="71e85-153">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="71e85-154">Se você quiser tooconfigure ServiceNow pular a etapa 2.</span><span class="sxs-lookup"><span data-stu-id="71e85-154">If you want tooconfigure ServiceNow omit step 2.</span></span> <span data-ttu-id="71e85-155">Da mesma forma, se você quiser tooconfigure ServiceNow Express pular a etapa 1.</span><span class="sxs-lookup"><span data-stu-id="71e85-155">Likewise, if you want tooconfigure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="71e85-156">Configuração do logon único do Azure AD para o ServiceNow</span><span class="sxs-lookup"><span data-stu-id="71e85-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="71e85-157">No portal clássico de saudação do AD do Azure, em Olá **ServiceNow** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo .</span><span class="sxs-lookup"><span data-stu-id="71e85-157">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="71e85-158">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="71e85-159">Em Olá **como você gostaria usuários toosign em tooServiceNow** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="71e85-159">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="71e85-160">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="71e85-161">Em Olá **definir configurações de aplicativo** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-161">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="71e85-162">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="71e85-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="71e85-163">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-163">a.</span></span> <span data-ttu-id="71e85-164">em Olá **ServiceNow URL de logon** caixa de texto, digite a URL usada pelo seu aplicativo de ServiceNow tooyour toosign em usuários seguindo saudação padrão: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="71e85-164">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="71e85-165">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-165">b.</span></span> <span data-ttu-id="71e85-166">Em Olá **identificador** caixa de texto, digite a URL usada pelo seu aplicativo de ServiceNow tooyour toosign em usuários seguindo saudação padrão: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="71e85-166">In hello **Identifier** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="71e85-167">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-167">c.</span></span> <span data-ttu-id="71e85-168">Clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="71e85-168">Click **Next**</span></span>

4. <span data-ttu-id="71e85-169">toohave AD do Azure automaticamente configurar ServiceNow para autenticação SAML, digite o nome da instância do ServiceNow, nome de usuário administrador e senha do administrador no hello **configurar automaticamente o logon único** formulário e clique em  *Configurar*.</span><span class="sxs-lookup"><span data-stu-id="71e85-169">toohave Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in hello **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="71e85-170">Observe que esse nome de usuário de administrador Olá fornecido deve ter Olá **security_admin** função atribuída no ServiceNow para este toowork.</span><span class="sxs-lookup"><span data-stu-id="71e85-170">Note that hello admin username provided must have hello **security_admin** role assigned in ServiceNow for this toowork.</span></span> <span data-ttu-id="71e85-171">Caso contrário, toomanually configurar ServiceNow toouse AD do Azure como um provedor de identidade SAML, clique em **configurar manualmente o aplicativo hello para logon único**, em seguida, clique em **próximo** e hello concluída as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="71e85-171">Otherwise, toomanually configure ServiceNow toouse Azure AD as a SAML identity provider, click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="71e85-172">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="71e85-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="71e85-173">Em hello **configurar logon único em ServiceNow** , clique em **Download certificado**, salvar arquivo de certificado Olá localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="71e85-173">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="71e85-174">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="71e85-175">Logon tooyour ServiceNow aplicativo como um administrador.</span><span class="sxs-lookup"><span data-stu-id="71e85-175">Sign-on tooyour ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="71e85-176">Ativar Olá *integração - vários provedor Single Sign-On instalador* plug-in seguindo Olá próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="71e85-176">Activate hello *Integration - Multiple Provider Single Sign-On Installer* plugin by following hello next steps:</span></span>
   
    <span data-ttu-id="71e85-177">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-177">a.</span></span> <span data-ttu-id="71e85-178">No painel de navegação Olá no lado esquerdo do hello, vá muito**definição sistema** seção e, em seguida, clique em **plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="71e85-178">In hello navigation pane on hello left side, go too**System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="71e85-179">![Configurar URL do aplicativo](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Ativar o plug-in")</span><span class="sxs-lookup"><span data-stu-id="71e85-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="71e85-180">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-180">b.</span></span> <span data-ttu-id="71e85-181">Procure *Integração - Instalador de Logon Único de Vários Provedores*.</span><span class="sxs-lookup"><span data-stu-id="71e85-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="71e85-182">![Configurar URL do aplicativo](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Ativar o plug-in")</span><span class="sxs-lookup"><span data-stu-id="71e85-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="71e85-183">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-183">c.</span></span> <span data-ttu-id="71e85-184">Selecione Olá plug-in.</span><span class="sxs-lookup"><span data-stu-id="71e85-184">Select hello plugin.</span></span> <span data-ttu-id="71e85-185">Clique com o botão direito do mouse e selecione **Ativar/Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="71e85-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="71e85-186">d.</span><span class="sxs-lookup"><span data-stu-id="71e85-186">d.</span></span> <span data-ttu-id="71e85-187">Clique em Olá **ativar** botão.</span><span class="sxs-lookup"><span data-stu-id="71e85-187">Click hello **Activate** button.</span></span>

8. <span data-ttu-id="71e85-188">No painel de navegação Olá no lado esquerdo do hello, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="71e85-188">In hello navigation pane on hello left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="71e85-189">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="71e85-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="71e85-190">Em Olá **várias propriedades do provedor de SSO** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-190">On hello **Multiple Provider SSO Properties** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="71e85-191">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="71e85-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="71e85-192">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-192">a.</span></span> <span data-ttu-id="71e85-193">Como **Habilitar vários provedores SSO**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="71e85-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="71e85-194">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-194">b.</span></span> <span data-ttu-id="71e85-195">Como **Habilitar log de depuração tem Olá provedor múltiplo integração SSO**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="71e85-195">As **Enable debug logging got hello multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="71e85-196">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-196">c.</span></span> <span data-ttu-id="71e85-197">No **campo Olá no usuário de saudação de tabela que...**  caixa de texto, tipo **user_name**.</span><span class="sxs-lookup"><span data-stu-id="71e85-197">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="71e85-198">d.</span><span class="sxs-lookup"><span data-stu-id="71e85-198">d.</span></span> <span data-ttu-id="71e85-199">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="71e85-199">Click **Save**.</span></span>

10. <span data-ttu-id="71e85-200">No painel de navegação Olá no lado esquerdo do hello, clique em **certificados x509**.</span><span class="sxs-lookup"><span data-stu-id="71e85-200">In hello navigation pane on hello left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="71e85-201">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="71e85-202">Em Olá **certificados x. 509** caixa de diálogo, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="71e85-202">On hello **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="71e85-203">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="71e85-204">Em Olá **certificados x. 509** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-204">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="71e85-205">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="71e85-206">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-206">a.</span></span> <span data-ttu-id="71e85-207">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="71e85-207">Click **New**.</span></span>
    
     <span data-ttu-id="71e85-208">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-208">b.</span></span> <span data-ttu-id="71e85-209">Em Olá **nome** caixa de texto, digite um nome para a sua configuração (por exemplo: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="71e85-209">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="71e85-210">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-210">c.</span></span> <span data-ttu-id="71e85-211">Selecione **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="71e85-211">Select **Active**.</span></span>
    
     <span data-ttu-id="71e85-212">d.</span><span class="sxs-lookup"><span data-stu-id="71e85-212">d.</span></span> <span data-ttu-id="71e85-213">Para **Formato**, selecione **PEM**.</span><span class="sxs-lookup"><span data-stu-id="71e85-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="71e85-214">e.</span><span class="sxs-lookup"><span data-stu-id="71e85-214">e.</span></span> <span data-ttu-id="71e85-215">Como **Tipo**, selecione **Confiar nos Certificados do Repositório**.</span><span class="sxs-lookup"><span data-stu-id="71e85-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="71e85-216">f.</span><span class="sxs-lookup"><span data-stu-id="71e85-216">f.</span></span> <span data-ttu-id="71e85-217">Abra seu certificado codificado na Base64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado PEM** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="71e85-217">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="71e85-218">g.</span><span class="sxs-lookup"><span data-stu-id="71e85-218">g.</span></span> <span data-ttu-id="71e85-219">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="71e85-219">Click **Update**.</span></span>

13. <span data-ttu-id="71e85-220">No painel de navegação Olá no lado esquerdo do hello, clique em **provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="71e85-220">In hello navigation pane on hello left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="71e85-221">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="71e85-222">Em Olá **provedores de identidade** caixa de diálogo, clique em **novo**:</span><span class="sxs-lookup"><span data-stu-id="71e85-222">On hello **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="71e85-223">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="71e85-224">Em Olá **provedores de identidade** caixa de diálogo, clique em **SAML2 Update1?**:</span><span class="sxs-lookup"><span data-stu-id="71e85-224">On hello **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="71e85-225">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="71e85-226">Na caixa de diálogo de propriedades de Update1 SAML2 hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-226">On hello SAML2 Update1 Properties dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="71e85-227">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="71e85-228">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-228">a.</span></span> <span data-ttu-id="71e85-229">em Olá **nome** caixa de texto, digite um nome para a sua configuração (por exemplo: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="71e85-229">in hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="71e85-230">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-230">b.</span></span> <span data-ttu-id="71e85-231">Em Olá **campo usuário** caixa de texto, tipo **email** ou **user_name**, dependendo de qual campo é usado toouniquely identificar os usuários de sua implantação do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="71e85-231">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="71e85-232">Você pode tooemit de configuração do AD do Azure ou ID de usuário de saudação do AD do Azure (nome principal do usuário) ou Olá endereço de email como Olá identificador exclusivo no token SAML Olá por vai toohello **ServiceNow > atributos > Single Sign-On** seção Olá portal clássico do Azure e mapeamento Olá desejado campo toohello **nameidentifier** atributo.</span><span class="sxs-lookup"><span data-stu-id="71e85-232">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="71e85-233">valor Olá armazenado para o atributo selecionado Olá no AD do Azure (por exemplo, nome) deve corresponder o valor de saudação armazenado no ServiceNow para o campo de saudação inserido (por exemplo, user_name)</span><span class="sxs-lookup"><span data-stu-id="71e85-233">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>

    <span data-ttu-id="71e85-234">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-234">c.</span></span> <span data-ttu-id="71e85-235">No portal clássico de saudação do AD do Azure, copie Olá **ID do provedor de identidade** valor e, em seguida, cole-o em Olá **URL do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="71e85-235">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="71e85-236">d.</span><span class="sxs-lookup"><span data-stu-id="71e85-236">d.</span></span> <span data-ttu-id="71e85-237">No portal clássico de saudação do AD do Azure, copie Olá **URL de solicitação de autenticação** valor e, em seguida, cole-o em Olá **AuthnRequest do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="71e85-237">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="71e85-238">e.</span><span class="sxs-lookup"><span data-stu-id="71e85-238">e.</span></span> <span data-ttu-id="71e85-239">No portal clássico de saudação do AD do Azure, copie Olá **URL do serviço de logon único** valor e, em seguida, cole-o em Olá **SingleLogoutRequest do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="71e85-239">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="71e85-240">f.</span><span class="sxs-lookup"><span data-stu-id="71e85-240">f.</span></span> <span data-ttu-id="71e85-241">Em Olá **ServiceNow Homepage** caixa de texto, digite a URL de saudação da instância ServiceNow home page.</span><span class="sxs-lookup"><span data-stu-id="71e85-241">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="71e85-242">página inicial da instância de ServiceNow Olá é uma concatenação do seu **URL do locatário ServieNow** e **/navpage.do** (por exemplo:`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="71e85-242">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="71e85-243">g.</span><span class="sxs-lookup"><span data-stu-id="71e85-243">g.</span></span> <span data-ttu-id="71e85-244">Em Olá **ID da entidade / emissor** caixa de texto, digite a URL de saudação do seu locatário ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="71e85-244">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="71e85-245">h.</span><span class="sxs-lookup"><span data-stu-id="71e85-245">h.</span></span> <span data-ttu-id="71e85-246">Em Olá **URL público** caixa de texto, digite a URL de saudação do seu locatário ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="71e85-246">In hello **Audience URL** textbox, type hello URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="71e85-247">i.</span><span class="sxs-lookup"><span data-stu-id="71e85-247">i.</span></span> <span data-ttu-id="71e85-248">Em Olá **protocolo de associação de saudação do IDP SingleLogoutRequest** caixa de texto, tipo **urn: oasis: nomes: tc: SAML:2.0:bindings:HTTP-redirecionar**.</span><span class="sxs-lookup"><span data-stu-id="71e85-248">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="71e85-249">j.</span><span class="sxs-lookup"><span data-stu-id="71e85-249">j.</span></span> <span data-ttu-id="71e85-250">Em Olá política NameID caixa de texto, digite **urn: oasis: nomes: tc: SAML: 1.1 nameid-format: não especificado**.</span><span class="sxs-lookup"><span data-stu-id="71e85-250">In hello NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="71e85-251">k.</span><span class="sxs-lookup"><span data-stu-id="71e85-251">k.</span></span> <span data-ttu-id="71e85-252">Desmarque **Criar um AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="71e85-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="71e85-253">l.</span><span class="sxs-lookup"><span data-stu-id="71e85-253">l.</span></span> <span data-ttu-id="71e85-254">Em Olá **método AuthnContextClassRef**, tipo `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="71e85-254">In hello **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="71e85-255">Isso só será necessário se você for uma organização que esteja somente na nuvem.</span><span class="sxs-lookup"><span data-stu-id="71e85-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="71e85-256">Se você estiver usando o ADFS ou o MFA local para autenticação, não deverá configurar esse valor.</span><span class="sxs-lookup"><span data-stu-id="71e85-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="71e85-257">m.</span><span class="sxs-lookup"><span data-stu-id="71e85-257">m.</span></span> <span data-ttu-id="71e85-258">Na caixa de texto **Distorção do Relógio**, digite **60**.</span><span class="sxs-lookup"><span data-stu-id="71e85-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="71e85-259">n.</span><span class="sxs-lookup"><span data-stu-id="71e85-259">n.</span></span> <span data-ttu-id="71e85-260">Como **Script de Logon Único**, selecione **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="71e85-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="71e85-261">o.</span><span class="sxs-lookup"><span data-stu-id="71e85-261">o.</span></span> <span data-ttu-id="71e85-262">Como **x509 certificado**, selecione certificado Olá que você criou na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="71e85-262">As **x509 Certificate**, select hello certificate you have created in hello previous step.</span></span>

    <span data-ttu-id="71e85-263">p.</span><span class="sxs-lookup"><span data-stu-id="71e85-263">p.</span></span> <span data-ttu-id="71e85-264">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="71e85-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="71e85-265">No portal clássico de saudação do AD do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="71e85-265">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="71e85-266">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="71e85-267">Em Olá **único logon confirmação** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="71e85-267">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="71e85-268">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="71e85-269">Configuração do logon único do Azure AD para o ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="71e85-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="71e85-270">No portal clássico de saudação do AD do Azure, em Olá **ServiceNow** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo .</span><span class="sxs-lookup"><span data-stu-id="71e85-270">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="71e85-271">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="71e85-272">Em Olá **como você gostaria usuários toosign em tooServiceNow** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="71e85-272">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="71e85-273">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="71e85-274">Em Olá **definir configurações de aplicativo** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-274">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="71e85-275">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="71e85-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="71e85-276">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-276">a.</span></span> <span data-ttu-id="71e85-277">em Olá **ServiceNow URL de logon** caixa de texto, digite a URL usada pelo seu aplicativo de ServiceNow tooyour toosign em usuários seguindo saudação padrão: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="71e85-277">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="71e85-278">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-278">b.</span></span> <span data-ttu-id="71e85-279">Em Olá **URL do emissor** caixa de texto, digite a URL usada pelo seu aplicativo de ServiceNow tooyour toosign em usuários seguindo saudação padrão `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="71e85-279">In hello **Issuer URL** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="71e85-280">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-280">c.</span></span> <span data-ttu-id="71e85-281">Clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="71e85-281">Click **Next**</span></span>

4. <span data-ttu-id="71e85-282">Clique em **configurar manualmente o aplicativo hello para logon único**, em seguida, clique em **próximo** e Olá completo seguindo as etapas.</span><span class="sxs-lookup"><span data-stu-id="71e85-282">Click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="71e85-283">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="71e85-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="71e85-284">Em Olá **configurar logon único em ServiceNow** , clique em **Download certificado**, salvar o arquivo de certificado Olá localmente no seu computador e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="71e85-284">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="71e85-285">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="71e85-286">Logon tooyour aplicativo ServiceNow expresso como um administrador.</span><span class="sxs-lookup"><span data-stu-id="71e85-286">Sign-on tooyour ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="71e85-287">No painel de navegação Olá no lado esquerdo do hello, clique em **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="71e85-287">In hello navigation pane on hello left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="71e85-288">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="71e85-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="71e85-289">Em Olá **Single Sign-On** caixa de diálogo, clique Olá configuração ícone superior de saudação à direita e defina hello propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-289">On hello **Single Sign-On** dialog, click hello configuration icon on hello upper right and set hello following properties:</span></span>
   
    <span data-ttu-id="71e85-290">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="71e85-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="71e85-291">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-291">a.</span></span> <span data-ttu-id="71e85-292">Ativar/desativar **Habilitar provedor múltiplo SSO** toohello direita.</span><span class="sxs-lookup"><span data-stu-id="71e85-292">Toggle **Enable multiple provider SSO** toohello right.</span></span>
   
    <span data-ttu-id="71e85-293">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-293">b.</span></span> <span data-ttu-id="71e85-294">Ativar/desativar **depuração habilitar registro em log para Olá provedor múltiplo integração SSO** toohello direita.</span><span class="sxs-lookup"><span data-stu-id="71e85-294">Toggle **Enable debug logging for hello multiple provider SSO integration** toohello right.</span></span>
   
    <span data-ttu-id="71e85-295">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-295">c.</span></span> <span data-ttu-id="71e85-296">No **campo Olá no usuário de saudação de tabela que...**  caixa de texto, tipo **user_name**.</span><span class="sxs-lookup"><span data-stu-id="71e85-296">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="71e85-297">Em Olá **Single Sign-On** caixa de diálogo, clique em **adicionar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="71e85-297">On hello **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="71e85-298">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="71e85-299">Em Olá **certificados x. 509** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-299">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="71e85-300">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="71e85-301">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-301">a.</span></span> <span data-ttu-id="71e85-302">Em Olá **nome** caixa de texto, digite um nome para a sua configuração (por exemplo: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="71e85-302">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="71e85-303">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-303">b.</span></span> <span data-ttu-id="71e85-304">Selecione **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="71e85-304">Select **Active**.</span></span>
    
    <span data-ttu-id="71e85-305">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-305">c.</span></span> <span data-ttu-id="71e85-306">Para **Formato**, selecione **PEM**.</span><span class="sxs-lookup"><span data-stu-id="71e85-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="71e85-307">d.</span><span class="sxs-lookup"><span data-stu-id="71e85-307">d.</span></span> <span data-ttu-id="71e85-308">Como **Tipo**, selecione **Confiar nos Certificados do Repositório**.</span><span class="sxs-lookup"><span data-stu-id="71e85-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="71e85-309">e.</span><span class="sxs-lookup"><span data-stu-id="71e85-309">e.</span></span> <span data-ttu-id="71e85-310">Crie um arquivo codificado em Base64 usando o certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="71e85-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="71e85-311">Para obter mais detalhes, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="71e85-311">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="71e85-312">f.</span><span class="sxs-lookup"><span data-stu-id="71e85-312">f.</span></span> <span data-ttu-id="71e85-313">Abra seu certificado codificado na Base64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado PEM** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="71e85-313">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="71e85-314">g.</span><span class="sxs-lookup"><span data-stu-id="71e85-314">g.</span></span> <span data-ttu-id="71e85-315">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="71e85-315">Click **Update**.</span></span>
11. <span data-ttu-id="71e85-316">Em Olá **Single Sign-On** caixa de diálogo, clique em **adicionar novo IdP**.</span><span class="sxs-lookup"><span data-stu-id="71e85-316">On hello **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="71e85-317">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="71e85-318">Em Olá **adicionar novo provedor de identidade** caixa de diálogo, em **configurar o provedor de identidade**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-318">On hello **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform hello following steps:</span></span>
    
    <span data-ttu-id="71e85-319">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="71e85-320">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-320">a.</span></span> <span data-ttu-id="71e85-321">em Olá **nome** caixa de texto, digite um nome para a sua configuração (por exemplo: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="71e85-321">In hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="71e85-322">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-322">b.</span></span> <span data-ttu-id="71e85-323">No portal clássico de saudação do AD do Azure, copie Olá **ID do provedor de identidade** valor e, em seguida, cole-o em Olá **URL do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="71e85-323">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="71e85-324">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-324">c.</span></span> <span data-ttu-id="71e85-325">No portal clássico de saudação do AD do Azure, copie Olá **URL de solicitação de autenticação** valor e, em seguida, cole-o em Olá **AuthnRequest do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="71e85-325">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="71e85-326">d.</span><span class="sxs-lookup"><span data-stu-id="71e85-326">d.</span></span> <span data-ttu-id="71e85-327">No portal clássico de saudação do AD do Azure, copie Olá **URL do serviço de logon único** valor e, em seguida, cole-o em Olá **SingleLogoutRequest do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="71e85-327">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="71e85-328">e.</span><span class="sxs-lookup"><span data-stu-id="71e85-328">e.</span></span> <span data-ttu-id="71e85-329">Como **certificado do provedor de identidade**, selecione certificado Olá que você criou na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="71e85-329">As **Identity Provider Certificate**, select hello certificate you have created in hello previous step.</span></span>


1. <span data-ttu-id="71e85-330">Clique em **configurações avançadas**e, em **propriedades adicionais do provedor de identidade**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="71e85-331">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="71e85-332">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-332">a.</span></span> <span data-ttu-id="71e85-333">Em Olá **protocolo de associação de saudação do IDP SingleLogoutRequest** caixa de texto, tipo **urn: oasis: nomes: tc: SAML:2.0:bindings:HTTP-redirecionar**.</span><span class="sxs-lookup"><span data-stu-id="71e85-333">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="71e85-334">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-334">b.</span></span> <span data-ttu-id="71e85-335">Em hello **política NameID** caixa de texto, tipo **urn: oasis: nomes: tc: SAML: 1.1 nameid-format: não especificado**.</span><span class="sxs-lookup"><span data-stu-id="71e85-335">In hello **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="71e85-336">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-336">c.</span></span> <span data-ttu-id="71e85-337">Em Olá **método AuthnContextClassRef**, tipo **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="71e85-337">In hello **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="71e85-338">d.</span><span class="sxs-lookup"><span data-stu-id="71e85-338">d.</span></span> <span data-ttu-id="71e85-339">Desmarque **Criar um AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="71e85-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="71e85-340">Em **propriedades adicionais do provedor de serviço**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-340">Under **Additional Service Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="71e85-341">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="71e85-342">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-342">a.</span></span> <span data-ttu-id="71e85-343">Em Olá **ServiceNow Homepage** caixa de texto, digite a URL de saudação da instância ServiceNow home page.</span><span class="sxs-lookup"><span data-stu-id="71e85-343">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="71e85-344">página inicial da instância de ServiceNow Olá é uma concatenação do seu **URL do locatário ServieNow** e **/navpage.do** (por exemplo: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="71e85-344">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="71e85-345">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-345">b.</span></span> <span data-ttu-id="71e85-346">Em Olá **ID da entidade / emissor** caixa de texto, digite a URL de saudação do seu locatário ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="71e85-346">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="71e85-347">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-347">c.</span></span> <span data-ttu-id="71e85-348">Em Olá **URI de audiência** caixa de texto, digite a URL de saudação do seu locatário ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="71e85-348">In hello **Audience URI** textbox, type hello URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="71e85-349">d.</span><span class="sxs-lookup"><span data-stu-id="71e85-349">d.</span></span> <span data-ttu-id="71e85-350">Na caixa de texto **Distorção do Relógio**, digite **60**.</span><span class="sxs-lookup"><span data-stu-id="71e85-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="71e85-351">e.</span><span class="sxs-lookup"><span data-stu-id="71e85-351">e.</span></span> <span data-ttu-id="71e85-352">Em Olá **campo usuário** caixa de texto, tipo **email** ou **user_name**, dependendo de qual campo é usado toouniquely identificar os usuários de sua implantação do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="71e85-352">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="71e85-353">Você pode tooemit de configuração do AD do Azure ou ID de usuário de saudação do AD do Azure (nome principal do usuário) ou Olá endereço de email como Olá identificador exclusivo no token SAML Olá por vai toohello **ServiceNow > atributos > Single Sign-On** seção Olá portal clássico do Azure e mapeamento Olá desejado campo toohello **nameidentifier** atributo.</span><span class="sxs-lookup"><span data-stu-id="71e85-353">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="71e85-354">valor Olá armazenado para o atributo selecionado Olá no AD do Azure (por exemplo, nome) deve corresponder o valor de saudação armazenado no ServiceNow para o campo de saudação inserido (por exemplo, user_name)</span><span class="sxs-lookup"><span data-stu-id="71e85-354">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="71e85-355">f.</span><span class="sxs-lookup"><span data-stu-id="71e85-355">f.</span></span> <span data-ttu-id="71e85-356">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="71e85-356">Click **Save**.</span></span> 

3. <span data-ttu-id="71e85-357">No portal clássico de saudação do AD do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="71e85-357">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="71e85-358">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="71e85-359">Em Olá **único logon confirmação** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="71e85-359">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="71e85-360">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="71e85-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="71e85-361">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="71e85-361">Configuring user provisioning</span></span>
<span data-ttu-id="71e85-362">Olá o objetivo desta seção é toooutline como tooenable o provisionamento de usuário do usuário do Active Directory contas tooServiceNow.</span><span class="sxs-lookup"><span data-stu-id="71e85-362">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooServiceNow.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="71e85-363">tooconfigure provisionamento de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-363">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="71e85-364">No portal clássico do hello gerenciamento do Azure, em Olá **ServiceNow** página de integração de aplicativos, clique em **configurar provisionamento de usuário**.</span><span class="sxs-lookup"><span data-stu-id="71e85-364">In hello Azure Management classic portal, on hello **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="71e85-365">![Provisionamento do usuário](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Provisionamento do usuário")</span><span class="sxs-lookup"><span data-stu-id="71e85-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="71e85-366">Em Olá **insira seu ServiceNow credenciais tooenable provisionamento automático de usuário** , forneça Olá definições de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-366">On hello **Enter your ServiceNow credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
     <span data-ttu-id="71e85-367">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-367">a.</span></span> <span data-ttu-id="71e85-368">Em Olá **nome da instância ServiceNow** caixa de texto, nome da instância do tipo hello ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="71e85-368">In hello **ServiceNow Instance Name** textbox, type hello ServiceNow instance name.</span></span>
   
     <span data-ttu-id="71e85-369">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-369">b.</span></span> <span data-ttu-id="71e85-370">Em Olá **nome de usuário administrador ServiceNow** caixa de texto Nome do tipo hello de saudação conta de administrador do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="71e85-370">In hello **ServiceNow Admin User Name** textbox, type hello name of hello ServiceNow admin account.</span></span>
   
     <span data-ttu-id="71e85-371">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-371">c.</span></span> <span data-ttu-id="71e85-372">Em Olá **senha do administrador do ServiceNow** caixa de texto, digite a senha Olá para esta conta.</span><span class="sxs-lookup"><span data-stu-id="71e85-372">In hello **ServiceNow Admin Password** textbox, type hello password for this account.</span></span>
   
     <span data-ttu-id="71e85-373">d.</span><span class="sxs-lookup"><span data-stu-id="71e85-373">d.</span></span> <span data-ttu-id="71e85-374">Clique em **validar** tooverify sua configuração.</span><span class="sxs-lookup"><span data-stu-id="71e85-374">Click **validate** tooverify your configuration.</span></span>
   
     <span data-ttu-id="71e85-375">e.</span><span class="sxs-lookup"><span data-stu-id="71e85-375">e.</span></span> <span data-ttu-id="71e85-376">Clique em Olá **próximo** saudação do botão tooopen **próximas etapas** página.</span><span class="sxs-lookup"><span data-stu-id="71e85-376">Click hello **Next** button tooopen hello **Next steps** page.</span></span>
   
     <span data-ttu-id="71e85-377">f.</span><span class="sxs-lookup"><span data-stu-id="71e85-377">f.</span></span> <span data-ttu-id="71e85-378">Se você desejar tooprovision todos os usuários toothis de aplicativos, selecione "**provisionar automaticamente todas as contas de usuário no aplicativo do hello diretório toothis**".</span><span class="sxs-lookup"><span data-stu-id="71e85-378">If you want tooprovision all users toothis application, select “**Automatically provision all user accounts in hello directory toothis application**”.</span></span> 
   
    <span data-ttu-id="71e85-379">![Próximas etapas](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Próximas etapas")</span><span class="sxs-lookup"><span data-stu-id="71e85-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="71e85-380">g.</span><span class="sxs-lookup"><span data-stu-id="71e85-380">g.</span></span> <span data-ttu-id="71e85-381">Em Olá **próximas etapas** , clique em **concluir** toosave sua configuração.</span><span class="sxs-lookup"><span data-stu-id="71e85-381">On hello **Next steps** page, click **Complete** toosave your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="71e85-382">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="71e85-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="71e85-383">Nesta seção, você pode criar um usuário de teste no portal clássico do hello chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71e85-383">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="71e85-385">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="71e85-385">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="71e85-386">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="71e85-386">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="71e85-388">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="71e85-388">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="71e85-389">lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="71e85-389">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="71e85-391">Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="71e85-391">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="71e85-393">Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-393">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="71e85-395">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-395">a.</span></span> <span data-ttu-id="71e85-396">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="71e85-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="71e85-397">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-397">b.</span></span> <span data-ttu-id="71e85-398">Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="71e85-398">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="71e85-399">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-399">c.</span></span> <span data-ttu-id="71e85-400">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="71e85-400">Click **Next**.</span></span>

6. <span data-ttu-id="71e85-401">Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-401">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="71e85-403">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-403">a.</span></span> <span data-ttu-id="71e85-404">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="71e85-404">In hello **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="71e85-405">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-405">b.</span></span> <span data-ttu-id="71e85-406">Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="71e85-406">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="71e85-407">c.</span><span class="sxs-lookup"><span data-stu-id="71e85-407">c.</span></span> <span data-ttu-id="71e85-408">Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="71e85-408">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="71e85-409">d.</span><span class="sxs-lookup"><span data-stu-id="71e85-409">d.</span></span> <span data-ttu-id="71e85-410">Em Olá **função** lista, selecione **usuário**.</span><span class="sxs-lookup"><span data-stu-id="71e85-410">In hello **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="71e85-411">e.</span><span class="sxs-lookup"><span data-stu-id="71e85-411">e.</span></span> <span data-ttu-id="71e85-412">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="71e85-412">Click **Next**.</span></span>

7. <span data-ttu-id="71e85-413">Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="71e85-413">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="71e85-415">Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="71e85-415">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="71e85-417">a.</span><span class="sxs-lookup"><span data-stu-id="71e85-417">a.</span></span> <span data-ttu-id="71e85-418">Anote o valor Olá Olá **nova senha**.</span><span class="sxs-lookup"><span data-stu-id="71e85-418">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="71e85-419">b.</span><span class="sxs-lookup"><span data-stu-id="71e85-419">b.</span></span> <span data-ttu-id="71e85-420">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="71e85-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="71e85-421">Criar um usuário de teste do ServiceNow</span><span class="sxs-lookup"><span data-stu-id="71e85-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="71e85-422">Nesta seção, você criará uma usuária chamada Brenda Fernandes no ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="71e85-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="71e85-423">Nesta seção, você criará uma usuária chamada Brenda Fernandes no ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="71e85-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="71e85-424">Se você não souber como tooadd a um usuário no ServiceNow ou ServiceNow Express conta, contate a equipe de suporte do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="71e85-424">If you don't know how tooadd a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="71e85-425">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="71e85-425">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="71e85-426">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooServiceNow seu acesso.</span><span class="sxs-lookup"><span data-stu-id="71e85-426">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceNow.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="71e85-428">**tooassign Britta Simon tooServiceNow, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="71e85-428">**tooassign Britta Simon tooServiceNow, perform hello following steps:**</span></span>

1. <span data-ttu-id="71e85-429">No portal clássico do hello, exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, clique em **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="71e85-429">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Atribuir usuário][201] 

2. <span data-ttu-id="71e85-431">Na lista de aplicativos hello, selecione **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="71e85-431">In hello applications list, select **ServiceNow**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="71e85-433">No menu de saudação na parte superior de saudação, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="71e85-433">In hello menu on hello top, click **Users**.</span></span>
   
    ![Atribuir usuário][203] 

4. <span data-ttu-id="71e85-435">Na lista de todos os usuários hello, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="71e85-435">In hello All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="71e85-436">Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="71e85-436">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Atribuir usuário][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="71e85-438">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="71e85-438">Testing single sign-on</span></span>
<span data-ttu-id="71e85-439">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="71e85-439">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="71e85-440">Quando você clica em bloco ServiceNow Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour ServiceNow aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71e85-440">When you click hello ServiceNow tile in hello Access Panel, you should get automatically signed-on tooyour ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="71e85-441">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="71e85-441">Additional resources</span></span>
* [<span data-ttu-id="71e85-442">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="71e85-442">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="71e85-443">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="71e85-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
