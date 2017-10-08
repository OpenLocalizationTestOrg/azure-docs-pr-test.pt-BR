---
title: "Tutorial: Integração do Azure Active Directory ao Slack | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e margem de atraso."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="5d82b-103">Tutorial: Integração do Active Directory do Azure com o Slack</span><span class="sxs-lookup"><span data-stu-id="5d82b-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="5d82b-104">Neste tutorial, você aprenderá como toointegrate atraso com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="5d82b-104">In this tutorial, you learn how toointegrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5d82b-105">Integrando a margem de atraso do AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="5d82b-105">Integrating Slack with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5d82b-106">Você pode controlar no AD do Azure que tenha acesso tooSlack</span><span class="sxs-lookup"><span data-stu-id="5d82b-106">You can control in Azure AD who has access tooSlack</span></span>
- <span data-ttu-id="5d82b-107">Você pode habilitar seu usuários tooautomatically get conectado tooSlack (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5d82b-107">You can enable your users tooautomatically get signed-on tooSlack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5d82b-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5d82b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5d82b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5d82b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d82b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5d82b-110">Prerequisites</span></span>

<span data-ttu-id="5d82b-111">tooconfigure integração do AD do Azure com atraso, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="5d82b-111">tooconfigure Azure AD integration with Slack, you need hello following items:</span></span>

- <span data-ttu-id="5d82b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5d82b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5d82b-113">Uma assinatura habilitada para logon único do Slack</span><span class="sxs-lookup"><span data-stu-id="5d82b-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5d82b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5d82b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5d82b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5d82b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5d82b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5d82b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5d82b-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5d82b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5d82b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5d82b-118">Scenario description</span></span>
<span data-ttu-id="5d82b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5d82b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5d82b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="5d82b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5d82b-121">Adicionando o atraso da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5d82b-121">Adding Slack from hello gallery</span></span>
2. <span data-ttu-id="5d82b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5d82b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-hello-gallery"></a><span data-ttu-id="5d82b-123">Adicionando o atraso da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5d82b-123">Adding Slack from hello gallery</span></span>
<span data-ttu-id="5d82b-124">integração de saudação tooconfigure de atraso no AD do Azure, você precisa tooadd margem de atraso na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5d82b-124">tooconfigure hello integration of Slack into Azure AD, you need tooadd Slack from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5d82b-125">**tooadd atraso da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5d82b-125">**tooadd Slack from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d82b-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5d82b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5d82b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5d82b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="5d82b-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5d82b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="5d82b-133">Na caixa de pesquisa hello, digite **Slack**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-133">In hello search box, type **Slack**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="5d82b-135">No painel de resultados de saudação, selecione **Slack**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5d82b-135">In hello results panel, select **Slack**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5d82b-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5d82b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5d82b-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Slack, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="5d82b-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5d82b-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na margem de atraso é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d82b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Slack is tooa user in Azure AD.</span></span> <span data-ttu-id="5d82b-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em atraso precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="5d82b-140">In other words, a link relationship between an Azure AD user and hello related user in Slack needs toobe established.</span></span>

<span data-ttu-id="5d82b-141">Margem de atraso, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d82b-141">In Slack, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5d82b-142">tooconfigure e teste de logon único do AD do Azure com atraso, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="5d82b-142">tooconfigure and test Azure AD single sign-on with Slack, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5d82b-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5d82b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5d82b-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5d82b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5d82b-145">**[Criar um usuário de teste Slack](#creating-a-slack-test-user)**  -toohave um equivalente do Britta Simon na margem de atraso é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="5d82b-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - toohave a counterpart of Britta Simon in Slack that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5d82b-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="5d82b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5d82b-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="5d82b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5d82b-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d82b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5d82b-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo a margem de atraso.</span><span class="sxs-lookup"><span data-stu-id="5d82b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="5d82b-150">**tooconfigure AD do Azure-logon único com atraso, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5d82b-150">**tooconfigure Azure AD single sign-on with Slack, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d82b-151">Em Olá portal do Azure, Olá **Slack** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-151">In hello Azure portal, on hello **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="5d82b-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="5d82b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="5d82b-155">Em Olá **margem de atraso do domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5d82b-155">On hello **Slack Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="5d82b-157">a.</span><span class="sxs-lookup"><span data-stu-id="5d82b-157">a.</span></span> <span data-ttu-id="5d82b-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="5d82b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="5d82b-159">b.</span><span class="sxs-lookup"><span data-stu-id="5d82b-159">b.</span></span> <span data-ttu-id="5d82b-160">Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="5d82b-160">In hello **Identifier** textbox, type hello URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5d82b-161">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="5d82b-161">hello value is not real.</span></span> <span data-ttu-id="5d82b-162">Você tem valor de saudação tooupdate com hello real URL de logon.</span><span class="sxs-lookup"><span data-stu-id="5d82b-162">You have tooupdate hello value with hello actual Sign On URL.</span></span> <span data-ttu-id="5d82b-163">Entre em contato com [a equipe de suporte de atraso](https://slack.com/help/contact) tooget valor de saudação</span><span class="sxs-lookup"><span data-stu-id="5d82b-163">Contact [Slack support team](https://slack.com/help/contact) tooget hello value</span></span>
     
4. <span data-ttu-id="5d82b-164">Margem de atraso aplicativo espera asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="5d82b-164">Slack application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="5d82b-165">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5d82b-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="5d82b-166">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5d82b-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="5d82b-167">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="5d82b-167">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="5d82b-169">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, selecione **user.mail** como **identificador de usuário** e para cada linha mostrado na tabela de saudação abaixo, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5d82b-169">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="5d82b-170">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="5d82b-170">Attribute Name</span></span> | <span data-ttu-id="5d82b-171">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="5d82b-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5d82b-172">first_name</span><span class="sxs-lookup"><span data-stu-id="5d82b-172">first_name</span></span> | <span data-ttu-id="5d82b-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="5d82b-173">user.givenname</span></span> |
    | <span data-ttu-id="5d82b-174">last_name</span><span class="sxs-lookup"><span data-stu-id="5d82b-174">last_name</span></span> | <span data-ttu-id="5d82b-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="5d82b-175">user.surname</span></span> |
    | <span data-ttu-id="5d82b-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="5d82b-176">User.Email</span></span> | <span data-ttu-id="5d82b-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="5d82b-177">user.mail</span></span> |  
    | <span data-ttu-id="5d82b-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="5d82b-178">User.Username</span></span> | <span data-ttu-id="5d82b-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="5d82b-179">user.userprincipalname</span></span> |

    <span data-ttu-id="5d82b-180">a.</span><span class="sxs-lookup"><span data-stu-id="5d82b-180">a.</span></span> <span data-ttu-id="5d82b-181">Clique em **atributo** tooopen **Editar atributo** caixa de diálogo caixa e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5d82b-181">Click on **Attribute** tooopen **Edit Attribute** dialog box and perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="5d82b-183">a.</span><span class="sxs-lookup"><span data-stu-id="5d82b-183">a.</span></span> <span data-ttu-id="5d82b-184">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="5d82b-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="5d82b-185">b.</span><span class="sxs-lookup"><span data-stu-id="5d82b-185">b.</span></span> <span data-ttu-id="5d82b-186">De saudação **valor** lista, o valor do atributo select Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="5d82b-186">From hello **Value** list, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5d82b-187">c.</span><span class="sxs-lookup"><span data-stu-id="5d82b-187">c.</span></span> <span data-ttu-id="5d82b-188">Clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="5d82b-188">Click **OK**</span></span>

6. <span data-ttu-id="5d82b-189">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5d82b-189">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="5d82b-191">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5d82b-191">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5d82b-193">Em Olá **atraso configuração** seção, clique em **configurar atraso** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="5d82b-193">On hello **Slack Configuration** section, click **Configure Slack** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5d82b-194">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="5d82b-194">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="5d82b-196">Em uma janela de navegador web diferente, faça logon no site da empresa margem de atraso de tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="5d82b-196">In a different web browser window, log in tooyour Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="5d82b-197">Navegue muito**AD do Microsoft Azure** vá muito**as configurações de equipe**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-197">Navigate too**Microsoft Azure AD** then go too**Team Settings**.</span></span>

     ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="5d82b-199">Em Olá **as configurações de equipe** seção, clique em Olá **autenticação** guia e, em seguida, clique em **alterar configurações**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-199">In hello **Team Settings** section, click hello **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="5d82b-201">Em Olá **configurações de autenticação SAML** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5d82b-201">On hello **SAML Authentication Settings** dialog, perform hello following steps:</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="5d82b-203">a.</span><span class="sxs-lookup"><span data-stu-id="5d82b-203">a.</span></span>  <span data-ttu-id="5d82b-204">Em Olá **SAML 2.0 ponto de extremidade (HTTP)** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d82b-204">In hello **SAML 2.0 Endpoint (HTTP)** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5d82b-205">b.</span><span class="sxs-lookup"><span data-stu-id="5d82b-205">b.</span></span>  <span data-ttu-id="5d82b-206">Em hello **emissor do provedor de identidade** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d82b-206">In hello **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5d82b-207">c.</span><span class="sxs-lookup"><span data-stu-id="5d82b-207">c.</span></span>  <span data-ttu-id="5d82b-208">Abra o arquivo de certificado baixado no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado público** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="5d82b-208">Open your downloaded certificate file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>

    <span data-ttu-id="5d82b-209">d.</span><span class="sxs-lookup"><span data-stu-id="5d82b-209">d.</span></span> <span data-ttu-id="5d82b-210">Configure Olá acima três configurações conforme apropriado para sua equipe de margem de atraso.</span><span class="sxs-lookup"><span data-stu-id="5d82b-210">Configure hello above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="5d82b-211">Para obter mais informações sobre configurações de hello, localizar o hello **guia de configuração de SSO do atraso** aqui.</span><span class="sxs-lookup"><span data-stu-id="5d82b-211">For more information about hello settings, please find hello **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="5d82b-212">e.</span><span class="sxs-lookup"><span data-stu-id="5d82b-212">e.</span></span>  <span data-ttu-id="5d82b-213">Clique em **Salvar Configuração**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="5d82b-214">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="5d82b-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5d82b-215">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="5d82b-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5d82b-216">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5d82b-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5d82b-217">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5d82b-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="5d82b-218">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d82b-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="5d82b-220">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5d82b-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d82b-221">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5d82b-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5d82b-223">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5d82b-225">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d82b-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5d82b-227">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5d82b-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5d82b-229">a.</span><span class="sxs-lookup"><span data-stu-id="5d82b-229">a.</span></span> <span data-ttu-id="5d82b-230">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5d82b-231">b.</span><span class="sxs-lookup"><span data-stu-id="5d82b-231">b.</span></span> <span data-ttu-id="5d82b-232">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5d82b-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5d82b-233">c.</span><span class="sxs-lookup"><span data-stu-id="5d82b-233">c.</span></span> <span data-ttu-id="5d82b-234">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5d82b-235">d.</span><span class="sxs-lookup"><span data-stu-id="5d82b-235">d.</span></span> <span data-ttu-id="5d82b-236">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="5d82b-237">Criar um usuário de teste do Slack</span><span class="sxs-lookup"><span data-stu-id="5d82b-237">Creating a Slack test user</span></span>

<span data-ttu-id="5d82b-238">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon em atraso.</span><span class="sxs-lookup"><span data-stu-id="5d82b-238">hello objective of this section is toocreate a user called Britta Simon in Slack.</span></span> <span data-ttu-id="5d82b-239">O Slack dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="5d82b-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="5d82b-240">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="5d82b-240">There is no action item for you in this section.</span></span> <span data-ttu-id="5d82b-241">Um novo usuário é criado durante uma tentativa tooaccess margem de atraso se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="5d82b-241">A new user is created during an attempt tooaccess Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="5d82b-242">Se você precisar toocreate um usuário manualmente, será necessário tooContact [a equipe de suporte de atraso](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="5d82b-242">If you need toocreate a user manually, you need tooContact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5d82b-243">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5d82b-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5d82b-244">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSlack.</span><span class="sxs-lookup"><span data-stu-id="5d82b-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSlack.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="5d82b-246">**tooassign Britta Simon tooSlack, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5d82b-246">**tooassign Britta Simon tooSlack, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d82b-247">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5d82b-249">Na lista de aplicativos hello, selecione **Slack**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-249">In hello applications list, select **Slack**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="5d82b-251">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="5d82b-253">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5d82b-253">Click **Add** button.</span></span> <span data-ttu-id="5d82b-254">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5d82b-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="5d82b-256">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d82b-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5d82b-257">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5d82b-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5d82b-258">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5d82b-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5d82b-259">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="5d82b-259">Testing single sign-on</span></span>

<span data-ttu-id="5d82b-260">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d82b-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5d82b-261">Quando você clica em bloco de margem de atraso de saudação em Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de margem de atraso.</span><span class="sxs-lookup"><span data-stu-id="5d82b-261">When you click hello Slack tile in hello Access Panel, you should get automatically signed-on tooyour Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5d82b-262">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5d82b-262">Additional resources</span></span>

* [<span data-ttu-id="5d82b-263">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5d82b-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5d82b-264">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5d82b-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

