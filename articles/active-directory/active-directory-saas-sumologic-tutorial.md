---
title: "Tutorial: Integração do Azure Active Directory ao SumoLogic | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do SumoLogic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="130da-103">Tutorial: Integração do Azure Active Directory ao SumoLogic</span><span class="sxs-lookup"><span data-stu-id="130da-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="130da-104">Neste tutorial, você aprenderá como toointegrate SumoLogic com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="130da-104">In this tutorial, you learn how toointegrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="130da-105">Integrando o SumoLogic com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="130da-105">Integrating SumoLogic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="130da-106">Você pode controlar no AD do Azure que tenha acesso tooSumoLogic</span><span class="sxs-lookup"><span data-stu-id="130da-106">You can control in Azure AD who has access tooSumoLogic</span></span>
- <span data-ttu-id="130da-107">Você pode habilitar seu usuários tooautomatically get conectado tooSumoLogic (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="130da-107">You can enable your users tooautomatically get signed-on tooSumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="130da-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="130da-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="130da-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="130da-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="130da-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="130da-110">Prerequisites</span></span>

<span data-ttu-id="130da-111">tooconfigure integração do Azure AD com SumoLogic, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="130da-111">tooconfigure Azure AD integration with SumoLogic, you need hello following items:</span></span>

- <span data-ttu-id="130da-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="130da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="130da-113">Uma assinatura habilitada para logon único do SumoLogic</span><span class="sxs-lookup"><span data-stu-id="130da-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="130da-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="130da-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="130da-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="130da-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="130da-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="130da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="130da-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="130da-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="130da-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="130da-118">Scenario description</span></span>
<span data-ttu-id="130da-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="130da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="130da-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="130da-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="130da-121">Adicionando SumoLogic da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="130da-121">Adding SumoLogic from hello gallery</span></span>
2. <span data-ttu-id="130da-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="130da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-hello-gallery"></a><span data-ttu-id="130da-123">Adicionando SumoLogic da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="130da-123">Adding SumoLogic from hello gallery</span></span>
<span data-ttu-id="130da-124">integração de saudação tooconfigure do SumoLogic no AD do Azure, você precisa tooadd SumoLogic da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="130da-124">tooconfigure hello integration of SumoLogic into Azure AD, you need tooadd SumoLogic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="130da-125">**tooadd SumoLogic da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="130da-125">**tooadd SumoLogic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="130da-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="130da-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="130da-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="130da-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="130da-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="130da-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="130da-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="130da-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="130da-133">Na caixa de pesquisa hello, digite **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="130da-133">In hello search box, type **SumoLogic**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="130da-135">No painel de resultados de saudação, selecione **SumoLogic**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="130da-135">In hello results panel, select **SumoLogic**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="130da-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="130da-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="130da-138">Nesta seção, você configurará e testará o logon único do Azure AD com o SumoLogic, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="130da-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="130da-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na SumoLogic é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="130da-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SumoLogic is tooa user in Azure AD.</span></span> <span data-ttu-id="130da-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na SumoLogic precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="130da-140">In other words, a link relationship between an Azure AD user and hello related user in SumoLogic needs toobe established.</span></span>

<span data-ttu-id="130da-141">Na SumoLogic, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="130da-141">In SumoLogic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="130da-142">tooconfigure e teste de logon único do Azure AD com SumoLogic, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="130da-142">tooconfigure and test Azure AD single sign-on with SumoLogic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="130da-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="130da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="130da-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="130da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="130da-145">**[Criar um usuário de teste do SumoLogic](#creating-a-sumologic-test-user)**  -toohave um equivalente do Britta Simon na SumoLogic que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="130da-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - toohave a counterpart of Britta Simon in SumoLogic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="130da-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="130da-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="130da-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="130da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="130da-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="130da-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="130da-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="130da-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="130da-150">**tooconfigure AD do Azure-logon único com o SumoLogic, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="130da-150">**tooconfigure Azure AD single sign-on with SumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="130da-151">Em Olá portal do Azure, Olá **SumoLogic** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="130da-151">In hello Azure portal, on hello **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="130da-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="130da-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="130da-155">Em Olá **SumoLogic domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="130da-155">On hello **SumoLogic Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="130da-157">a.</span><span class="sxs-lookup"><span data-stu-id="130da-157">a.</span></span> <span data-ttu-id="130da-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="130da-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="130da-159">b.</span><span class="sxs-lookup"><span data-stu-id="130da-159">b.</span></span> <span data-ttu-id="130da-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="130da-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="130da-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="130da-161">These values are not real.</span></span> <span data-ttu-id="130da-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="130da-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="130da-163">Entre em contato com [equipe de suporte do cliente SumoLogic](https://www.sumologic.com/contact-us/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="130da-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="130da-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="130da-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="130da-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="130da-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="130da-168">Em Olá **SumoLogic configuração** seção, clique em **configurar SumoLogic** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="130da-168">On hello **SumoLogic Configuration** section, click **Configure SumoLogic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="130da-169">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="130da-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="130da-171">Em uma janela de navegador web diferente, faça logon no site da empresa tooyour SumoLogic como um administrador.</span><span class="sxs-lookup"><span data-stu-id="130da-171">In a different web browser window, log in tooyour SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="130da-172">Vá muito**gerenciar \> segurança**.</span><span class="sxs-lookup"><span data-stu-id="130da-172">Go too**Manage \> Security**.</span></span>
   
    <span data-ttu-id="130da-173">![Gerenciar](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Gerenciar")</span><span class="sxs-lookup"><span data-stu-id="130da-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="130da-174">Clique em **SAML**.</span><span class="sxs-lookup"><span data-stu-id="130da-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="130da-175">![Configurações de segurança global](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Configurações de segurança global")</span><span class="sxs-lookup"><span data-stu-id="130da-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="130da-176">De saudação **selecionar uma configuração ou criar um novo** , selecione **AD do Azure**e, em seguida, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="130da-176">From hello **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="130da-177">![Configurar o SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configurar o SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="130da-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="130da-178">Em Olá **configurar SAML 2.0** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="130da-178">On hello **Configure SAML 2.0** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="130da-179">![Configurar o SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configurar o SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="130da-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="130da-180">a.</span><span class="sxs-lookup"><span data-stu-id="130da-180">a.</span></span> <span data-ttu-id="130da-181">Em Olá **nome da configuração** caixa de texto, tipo **AD do Azure**.</span><span class="sxs-lookup"><span data-stu-id="130da-181">In hello **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="130da-182">b.</span><span class="sxs-lookup"><span data-stu-id="130da-182">b.</span></span> <span data-ttu-id="130da-183">Selecione **Modo de Depuração**.</span><span class="sxs-lookup"><span data-stu-id="130da-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="130da-184">c.</span><span class="sxs-lookup"><span data-stu-id="130da-184">c.</span></span> <span data-ttu-id="130da-185">Em hello **emissor** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="130da-185">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="130da-186">d.</span><span class="sxs-lookup"><span data-stu-id="130da-186">d.</span></span> <span data-ttu-id="130da-187">Em Olá **URL de solicitação de autenticação nos quais** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="130da-187">In hello **Authn Request URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="130da-188">e.</span><span class="sxs-lookup"><span data-stu-id="130da-188">e.</span></span> <span data-ttu-id="130da-189">Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e cole Olá certificado inteiro na **certificado x. 509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="130da-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="130da-190">f.</span><span class="sxs-lookup"><span data-stu-id="130da-190">f.</span></span> <span data-ttu-id="130da-191">Para **Atributo de Email**, selecione **Usar entidade do SAML**.</span><span class="sxs-lookup"><span data-stu-id="130da-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="130da-192">g.</span><span class="sxs-lookup"><span data-stu-id="130da-192">g.</span></span> <span data-ttu-id="130da-193">Selecione **Configuração de Logon iniciada pelo SP**.</span><span class="sxs-lookup"><span data-stu-id="130da-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="130da-194">h.</span><span class="sxs-lookup"><span data-stu-id="130da-194">h.</span></span> <span data-ttu-id="130da-195">Em Olá **caminho de logon** caixa de texto, tipo **Azure** e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="130da-195">In hello **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="130da-196">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="130da-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="130da-197">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="130da-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="130da-198">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="130da-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="130da-199">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="130da-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="130da-200">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="130da-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="130da-202">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="130da-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="130da-203">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="130da-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="130da-205">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="130da-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="130da-207">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="130da-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="130da-209">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="130da-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="130da-211">a.</span><span class="sxs-lookup"><span data-stu-id="130da-211">a.</span></span> <span data-ttu-id="130da-212">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="130da-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="130da-213">b.</span><span class="sxs-lookup"><span data-stu-id="130da-213">b.</span></span> <span data-ttu-id="130da-214">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="130da-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="130da-215">c.</span><span class="sxs-lookup"><span data-stu-id="130da-215">c.</span></span> <span data-ttu-id="130da-216">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="130da-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="130da-217">d.</span><span class="sxs-lookup"><span data-stu-id="130da-217">d.</span></span> <span data-ttu-id="130da-218">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="130da-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="130da-219">Criar um usuário de teste do SumoLogic</span><span class="sxs-lookup"><span data-stu-id="130da-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="130da-220">Ordem tooenable AD do Azure usuários toolog em tooSumoLogic, elas devem ser provisionado tooSumoLogic.</span><span class="sxs-lookup"><span data-stu-id="130da-220">In order tooenable Azure AD users toolog in tooSumoLogic, they must be provisioned tooSumoLogic.</span></span>  

* <span data-ttu-id="130da-221">No caso de saudação do SumoLogic, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="130da-221">In hello case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="130da-222">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="130da-222">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="130da-223">Faça logon no tooyour **SumoLogic** locatário.</span><span class="sxs-lookup"><span data-stu-id="130da-223">Log in tooyour **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="130da-224">Vá muito**gerenciar \> usuários**.</span><span class="sxs-lookup"><span data-stu-id="130da-224">Go too**Manage \> Users**.</span></span>
   
    <span data-ttu-id="130da-225">![Usuários](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="130da-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="130da-226">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="130da-226">Click **Add**.</span></span>
   
    <span data-ttu-id="130da-227">![Usuários](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="130da-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="130da-228">Em Olá **novo usuário** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="130da-228">On hello **New User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="130da-229">![Novo Usuário](./media/active-directory-saas-sumologic-tutorial/ic778563.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="130da-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="130da-230">a.</span><span class="sxs-lookup"><span data-stu-id="130da-230">a.</span></span> <span data-ttu-id="130da-231">Informações da conta de saudação do AD do Azure que você deseja tooprovision em Olá relacionadas à saudação do tipo **nome**, **Sobrenome**, e **Email** caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="130da-231">Type hello related information of hello Azure AD account you want tooprovision into hello **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="130da-232">b.</span><span class="sxs-lookup"><span data-stu-id="130da-232">b.</span></span> <span data-ttu-id="130da-233">Selecione uma função.</span><span class="sxs-lookup"><span data-stu-id="130da-233">Select a role.</span></span>
  
    <span data-ttu-id="130da-234">c.</span><span class="sxs-lookup"><span data-stu-id="130da-234">c.</span></span> <span data-ttu-id="130da-235">Para **Status**, selecione **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="130da-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="130da-236">d.</span><span class="sxs-lookup"><span data-stu-id="130da-236">d.</span></span> <span data-ttu-id="130da-237">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="130da-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="130da-238">Você pode usar qualquer ferramenta de criação outros SumoLogic usuário conta ou APIs fornecidas pela SumoLogic tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="130da-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="130da-239">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="130da-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="130da-240">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSumoLogic.</span><span class="sxs-lookup"><span data-stu-id="130da-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSumoLogic.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="130da-242">**tooassign Britta Simon tooSumoLogic, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="130da-242">**tooassign Britta Simon tooSumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="130da-243">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="130da-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="130da-245">Na lista de aplicativos hello, selecione **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="130da-245">In hello applications list, select **SumoLogic**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="130da-247">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="130da-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="130da-249">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="130da-249">Click **Add** button.</span></span> <span data-ttu-id="130da-250">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="130da-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="130da-252">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="130da-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="130da-253">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="130da-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="130da-254">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="130da-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="130da-255">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="130da-255">Testing single sign-on</span></span>

<span data-ttu-id="130da-256">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="130da-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="130da-257">Quando você clica em bloco SumoLogic Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour SumoLogic aplicativo.</span><span class="sxs-lookup"><span data-stu-id="130da-257">When you click hello SumoLogic tile in hello Access Panel, you should get automatically signed-on tooyour SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="130da-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="130da-258">Additional resources</span></span>

* [<span data-ttu-id="130da-259">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="130da-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="130da-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="130da-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

