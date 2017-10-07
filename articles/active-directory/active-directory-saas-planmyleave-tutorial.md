---
title: "Tutorial: integração do Azure Active Directory ao PlanMyLeave | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="f6980-103">Tutorial: integração do Azure Active Directory com o PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="f6980-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="f6980-104">Neste tutorial, você aprenderá como toointegrate PlanMyLeave com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f6980-104">In this tutorial, you learn how toointegrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6980-105">Integrando PlanMyLeave com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6980-105">Integrating PlanMyLeave with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f6980-106">Você pode controlar no AD do Azure que tenha acesso tooPlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="f6980-106">You can control in Azure AD who has access tooPlanMyLeave</span></span>
- <span data-ttu-id="f6980-107">Você pode habilitar seu usuários tooautomatically get conectado tooPlanMyLeave (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f6980-107">You can enable your users tooautomatically get signed-on tooPlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f6980-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="f6980-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="f6980-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f6980-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6980-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f6980-110">Prerequisites</span></span>

<span data-ttu-id="f6980-111">tooconfigure integração do AD do Azure com PlanMyLeave, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6980-111">tooconfigure Azure AD integration with PlanMyLeave, you need hello following items:</span></span>

- <span data-ttu-id="f6980-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f6980-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6980-113">Uma assinatura do PlanMyLeave com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="f6980-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="f6980-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f6980-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="f6980-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f6980-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f6980-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f6980-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f6980-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6980-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="f6980-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f6980-118">Scenario description</span></span>
<span data-ttu-id="f6980-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f6980-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f6980-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="f6980-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6980-121">Adicionando PlanMyLeave da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f6980-121">Adding PlanMyLeave from hello gallery</span></span>
2. <span data-ttu-id="f6980-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f6980-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-hello-gallery"></a><span data-ttu-id="f6980-123">Adicionando PlanMyLeave da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f6980-123">Adding PlanMyLeave from hello gallery</span></span>
<span data-ttu-id="f6980-124">integração de saudação tooconfigure de PlanMyLeave no AD do Azure, você precisa tooadd PlanMyLeave da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f6980-124">tooconfigure hello integration of PlanMyLeave into Azure AD, you need tooadd PlanMyLeave from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f6980-125">**tooadd PlanMyLeave da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f6980-125">**tooadd PlanMyLeave from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6980-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f6980-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f6980-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f6980-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f6980-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f6980-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f6980-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f6980-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f6980-133">Na caixa de pesquisa hello, digite **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="f6980-133">In hello search box, type **PlanMyLeave**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="f6980-135">No painel de resultados de saudação, selecione **PlanMyLeave**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f6980-135">In hello results panel, select **PlanMyLeave**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f6980-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f6980-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f6980-138">Nesta seção, você configurará e testará o logon único do Azure AD com o PlanMyLeave, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="f6980-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f6980-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em PlanMyLeave é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6980-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PlanMyLeave is tooa user in Azure AD.</span></span> <span data-ttu-id="f6980-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em PlanMyLeave precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f6980-140">In other words, a link relationship between an Azure AD user and hello related user in PlanMyLeave needs toobe established.</span></span>

<span data-ttu-id="f6980-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="f6980-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="f6980-142">tooconfigure e teste de logon único do AD do Azure com PlanMyLeave, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6980-142">tooconfigure and test Azure AD single sign-on with PlanMyLeave, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f6980-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f6980-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f6980-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6980-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6980-145">**[Criar um usuário de teste PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave um equivalente do Britta Simon em PlanMyLeave é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="f6980-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - toohave a counterpart of Britta Simon in PlanMyLeave that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="f6980-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="f6980-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6980-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="f6980-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f6980-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6980-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f6980-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="f6980-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="f6980-150">**tooconfigure AD do Azure-logon único com PlanMyLeave, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f6980-150">**tooconfigure Azure AD single sign-on with PlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6980-151">No portal de gerenciamento do Azure do hello, no hello **PlanMyLeave** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="f6980-151">In hello Azure Management portal, on hello **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f6980-153">Em Olá **o logon único** página da caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="f6980-153">On hello **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="f6980-155">Em Olá **PlanMyLeave domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6980-155">On hello **PlanMyLeave Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="f6980-157">a.</span><span class="sxs-lookup"><span data-stu-id="f6980-157">a.</span></span> <span data-ttu-id="f6980-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="f6980-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="f6980-159">b.</span><span class="sxs-lookup"><span data-stu-id="f6980-159">b.</span></span> <span data-ttu-id="f6980-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="f6980-160">In hello **Identifer** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f6980-161">Observe que esses não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="f6980-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="f6980-162">Você tem tooupdate entrassem esses valores com hello real na URL e o identificador.</span><span class="sxs-lookup"><span data-stu-id="f6980-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="f6980-163">Entre em contato com [PlanMyLeave a equipe de suporte](mailto:support@planmyleave.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="f6980-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) tooget these values.</span></span>

4. <span data-ttu-id="f6980-164">Em Olá **o certificado de autenticação SAML** seção, clique em **criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="f6980-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="f6980-166">Em Olá **criar um novo certificado** caixa de diálogo, clique o ícone de calendário hello e selecione um **data de expiração**.</span><span class="sxs-lookup"><span data-stu-id="f6980-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="f6980-167">Em seguida, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f6980-167">Then click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="f6980-169">Em Olá **o certificado de autenticação SAML** seção, selecione **ativar o novo certificado** e clique em **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="f6980-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="f6980-171">Na janela pop-up de saudação **certificado de substituição** janela, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="f6980-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f6980-173">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f6980-173">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="f6980-175">Em Olá **PlanMyLeave configuração** seção, clique em **configurar PlanMyLeave** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="f6980-175">On hello **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** tooopen **Configure sign-on** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="f6980-178">Em outra janela do navegador da Web, faça logon no locatário do PlanMyLeave como administrador.</span><span class="sxs-lookup"><span data-stu-id="f6980-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="f6980-179">Vá muito**configuração do sistema**.</span><span class="sxs-lookup"><span data-stu-id="f6980-179">Go too**System Setup**.</span></span> <span data-ttu-id="f6980-180">Em seguida, na Olá **gerenciamento de segurança** seção clique **configurações da empresa SAML** .</span><span class="sxs-lookup"><span data-stu-id="f6980-180">Then on hello **Security Management** section click **Company SAML settings** .</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="f6980-182">Em Olá **configurações SAML** seção, clique em editor de ícone.</span><span class="sxs-lookup"><span data-stu-id="f6980-182">On hello **SAML Settings** section, click editor icon.</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="f6980-184">Em Olá **configurações de atualização de SAML** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6980-184">On hello **Update SAML Settings** section, perform hello following steps:</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="f6980-186">a.</span><span class="sxs-lookup"><span data-stu-id="f6980-186">a.</span></span>  <span data-ttu-id="f6980-187">Em Olá **URL de logon** caixa de texto, coloque o valor de saudação do **Single Sign-On URL do serviço SAML** da janela de configuração de aplicativo do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6980-187">In hello **Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="f6980-188">b.</span><span class="sxs-lookup"><span data-stu-id="f6980-188">b.</span></span>  <span data-ttu-id="f6980-189">Abra o arquivo de certificado baixado no bloco de notas, copie somente conteúdo de saudação entre hello---Begin Certificate--- e ---End certificate----lo em sua área de transferência e, em seguida, cole-o toohello **certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="f6980-189">Open your downloaded certificate file in notepad, copy only hello content between hello ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>

    <span data-ttu-id="f6980-190">c.</span><span class="sxs-lookup"><span data-stu-id="f6980-190">c.</span></span> <span data-ttu-id="f6980-191">Defina"**é habilitar**"muito"**Sim**".</span><span class="sxs-lookup"><span data-stu-id="f6980-191">Set "**Is Enable**" too"**Yes**".</span></span>

    <span data-ttu-id="f6980-192">d.</span><span class="sxs-lookup"><span data-stu-id="f6980-192">d.</span></span> <span data-ttu-id="f6980-193">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f6980-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f6980-194">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f6980-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="f6980-195">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6980-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f6980-197">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f6980-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6980-198">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f6980-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f6980-200">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="f6980-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f6980-202">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f6980-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6980-204">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6980-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f6980-206">a.</span><span class="sxs-lookup"><span data-stu-id="f6980-206">a.</span></span> <span data-ttu-id="f6980-207">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f6980-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f6980-208">b.</span><span class="sxs-lookup"><span data-stu-id="f6980-208">b.</span></span> <span data-ttu-id="f6980-209">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f6980-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f6980-210">c.</span><span class="sxs-lookup"><span data-stu-id="f6980-210">c.</span></span> <span data-ttu-id="f6980-211">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="f6980-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f6980-212">d.</span><span class="sxs-lookup"><span data-stu-id="f6980-212">d.</span></span> <span data-ttu-id="f6980-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f6980-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="f6980-214">Criação de um usuário de teste PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="f6980-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="f6980-215">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="f6980-215">hello objective of this section is toocreate a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="f6980-216">O PlanMyLeave dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="f6980-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="f6980-217">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="f6980-217">There is no action item for you in this section.</span></span> <span data-ttu-id="f6980-218">Será criado um novo usuário durante uma tentativa tooaccess PlanMyLeave se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="f6980-218">A new user will be created during an attempt tooaccess PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="f6980-219">Se você precisar toocreate um usuário manualmente, será necessário toocontact [a equipe de suporte PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="f6980-219">If you need toocreate an user manually, you need toocontact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f6980-220">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f6980-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f6980-221">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooPlanMyLeave seu acesso.</span><span class="sxs-lookup"><span data-stu-id="f6980-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPlanMyLeave.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f6980-223">**tooassign Britta Simon tooPlanMyLeave, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f6980-223">**tooassign Britta Simon tooPlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6980-224">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f6980-224">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f6980-226">Na lista de aplicativos hello, selecione **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="f6980-226">In hello applications list, select **PlanMyLeave**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="f6980-228">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f6980-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f6980-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f6980-230">Click **Add** button.</span></span> <span data-ttu-id="f6980-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f6980-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f6980-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="f6980-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f6980-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f6980-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f6980-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f6980-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="f6980-236">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f6980-236">Testing single sign-on</span></span>

<span data-ttu-id="f6980-237">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="f6980-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f6980-238">Quando você clica em bloco PlanMyLeave Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour PlanMyLeave aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6980-238">When you click hello PlanMyLeave tile in hello Access Panel, you should get automatically signed-on tooyour PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f6980-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f6980-239">Additional resources</span></span>

* [<span data-ttu-id="f6980-240">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f6980-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6980-241">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f6980-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png