---
title: "Tutorial: integração do Azure Active Directory com o Adaptive Suite | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o pacote adaptável."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="95a71-103">Tutorial: Integração do Active Directory do Azure ao Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="95a71-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="95a71-104">Neste tutorial, você aprenderá como toointegrate pacote adaptável com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="95a71-104">In this tutorial, you learn how toointegrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="95a71-105">Pacote adaptável integrando o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a71-105">Integrating Adaptive Suite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="95a71-106">Você pode controlar no AD do Azure que tenha acesso tooAdaptive Suite</span><span class="sxs-lookup"><span data-stu-id="95a71-106">You can control in Azure AD who has access tooAdaptive Suite</span></span>
- <span data-ttu-id="95a71-107">Você pode habilitar seu usuários tooautomatically get conectado tooAdaptive Suite (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95a71-107">You can enable your users tooautomatically get signed-on tooAdaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="95a71-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="95a71-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="95a71-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="95a71-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95a71-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="95a71-110">Prerequisites</span></span>

<span data-ttu-id="95a71-111">tooconfigure integração do AD do Azure com o pacote adaptável, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a71-111">tooconfigure Azure AD integration with Adaptive Suite, you need hello following items:</span></span>

- <span data-ttu-id="95a71-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95a71-112">An Azure AD subscription</span></span>
- <span data-ttu-id="95a71-113">Uma assinatura habilitada para logon único do Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="95a71-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="95a71-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="95a71-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="95a71-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="95a71-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="95a71-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="95a71-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="95a71-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95a71-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="95a71-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="95a71-118">Scenario description</span></span>
<span data-ttu-id="95a71-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="95a71-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="95a71-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="95a71-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="95a71-121">Adicionando pacote adaptável da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="95a71-121">Adding Adaptive Suite from hello gallery</span></span>
2. <span data-ttu-id="95a71-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95a71-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-hello-gallery"></a><span data-ttu-id="95a71-123">Adicionando pacote adaptável da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="95a71-123">Adding Adaptive Suite from hello gallery</span></span>
<span data-ttu-id="95a71-124">integração de saudação tooconfigure do pacote adaptável no AD do Azure, você precisa tooadd pacote adaptável de lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="95a71-124">tooconfigure hello integration of Adaptive Suite into Azure AD, you need tooadd Adaptive Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="95a71-125">**tooadd pacote adaptável da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95a71-125">**tooadd Adaptive Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a71-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="95a71-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="95a71-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="95a71-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="95a71-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="95a71-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="95a71-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95a71-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="95a71-133">Na caixa de pesquisa hello, digite **pacote adaptável**.</span><span class="sxs-lookup"><span data-stu-id="95a71-133">In hello search box, type **Adaptive Suite**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="95a71-135">No painel de resultados de saudação, selecione **pacote adaptável**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="95a71-135">In hello results panel, select **Adaptive Suite**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="95a71-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95a71-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="95a71-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Adaptive Suite, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="95a71-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="95a71-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no pacote adaptável é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="95a71-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adaptive Suite is tooa user in Azure AD.</span></span> <span data-ttu-id="95a71-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no pacote adaptável precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="95a71-140">In other words, a link relationship between an Azure AD user and hello related user in Adaptive Suite needs toobe established.</span></span>

<span data-ttu-id="95a71-141">Pacote adaptável, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="95a71-141">In Adaptive Suite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="95a71-142">tooconfigure e teste de logon único do AD do Azure com o pacote adaptável, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a71-142">tooconfigure and test Azure AD single sign-on with Adaptive Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="95a71-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="95a71-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="95a71-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95a71-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="95a71-145">**[Criar um usuário de teste do pacote adaptável](#creating-an-adaptive-suite-test-user)**  -toohave um equivalente do Britta Simon no pacote adaptável que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="95a71-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - toohave a counterpart of Britta Simon in Adaptive Suite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="95a71-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="95a71-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="95a71-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="95a71-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="95a71-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="95a71-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="95a71-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de pacote adaptável.</span><span class="sxs-lookup"><span data-stu-id="95a71-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="95a71-150">**tooconfigure AD do Azure-logon único com o pacote adaptável, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95a71-150">**tooconfigure Azure AD single sign-on with Adaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a71-151">Em Olá portal do Azure, Olá **pacote adaptável** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="95a71-151">In hello Azure portal, on hello **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="95a71-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="95a71-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="95a71-155">Em Olá **domínio adaptável de pacote e as URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a71-155">On hello **Adaptive Suite Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="95a71-157">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="95a71-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="95a71-158">Você pode obter esse valor de saudação pacote adaptável **configurações de SSO do SAML** página.</span><span class="sxs-lookup"><span data-stu-id="95a71-158">You can get this value from hello Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="95a71-159">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="95a71-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="95a71-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="95a71-161">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="95a71-163">Em Olá **adaptável configuração do conjunto** seção, clique em **configurar pacote adaptável** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="95a71-163">On hello **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="95a71-164">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="95a71-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="95a71-166">Em uma janela de navegador web diferente, faça logon no site da empresa tooyour pacote adaptável como um administrador.</span><span class="sxs-lookup"><span data-stu-id="95a71-166">In a different web browser window, log in tooyour Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="95a71-167">Vá muito**Admin**.</span><span class="sxs-lookup"><span data-stu-id="95a71-167">Go too**Admin**.</span></span>
   
    <span data-ttu-id="95a71-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="95a71-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="95a71-169">Em Olá **usuários e funções** seção, clique em **gerenciar configurações de SSO de SAML**.</span><span class="sxs-lookup"><span data-stu-id="95a71-169">In hello **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="95a71-170">![Gerenciar Configurações de SSO do SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Gerenciar Configurações de SSO do SAML")</span><span class="sxs-lookup"><span data-stu-id="95a71-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="95a71-171">Em Olá **configurações de SSO do SAML** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a71-171">On hello **SAML SSO Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="95a71-172">![Configurações de SSO do SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "Configurações de SSO do SAML")</span><span class="sxs-lookup"><span data-stu-id="95a71-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="95a71-173">a.</span><span class="sxs-lookup"><span data-stu-id="95a71-173">a.</span></span> <span data-ttu-id="95a71-174">Em Olá **nome do provedor de identidade** caixa de texto, digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="95a71-174">In hello **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="95a71-175">b.</span><span class="sxs-lookup"><span data-stu-id="95a71-175">b.</span></span> <span data-ttu-id="95a71-176">Saudação de colar **ID da entidade SAML** valor copiado do portal do Azure para Olá **ID da entidade do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="95a71-176">Paste hello **SAML Entity ID** value copied from Azure portal into hello **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="95a71-177">c.</span><span class="sxs-lookup"><span data-stu-id="95a71-177">c.</span></span> <span data-ttu-id="95a71-178">Saudação de colar **Single Sign-On URL do serviço SAML** valor copiado do portal do Azure para Olá **URL do SSO do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="95a71-178">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="95a71-179">d.</span><span class="sxs-lookup"><span data-stu-id="95a71-179">d.</span></span> <span data-ttu-id="95a71-180">Saudação de colar **Single Sign-On URL do serviço SAML** valor copiado do portal do Azure para Olá **URL personalizada do logout** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="95a71-180">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="95a71-181">e.</span><span class="sxs-lookup"><span data-stu-id="95a71-181">e.</span></span> <span data-ttu-id="95a71-182">tooupload seu certificado baixado, clique em **Escolher arquivo**.</span><span class="sxs-lookup"><span data-stu-id="95a71-182">tooupload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="95a71-183">f.</span><span class="sxs-lookup"><span data-stu-id="95a71-183">f.</span></span> <span data-ttu-id="95a71-184">Selecione o seguinte hello, para:</span><span class="sxs-lookup"><span data-stu-id="95a71-184">Select hello following, for:</span></span>
    * <span data-ttu-id="95a71-185">**ID de usuário do SAML**, selecione **Nome de usuário do Adaptive Insights do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="95a71-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="95a71-186">**Local da ID de usuário do SAML**, selecione **ID de usuário em NameID da Entidade**.</span><span class="sxs-lookup"><span data-stu-id="95a71-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="95a71-187">**Formato de NameID do SAML**, selecione **Endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="95a71-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="95a71-188">**Habilitar SAML**, selecione **Permitir SSO do SAML e direcionar logon do Adaptive Insights**.</span><span class="sxs-lookup"><span data-stu-id="95a71-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="95a71-189">g.</span><span class="sxs-lookup"><span data-stu-id="95a71-189">g.</span></span> <span data-ttu-id="95a71-190">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="95a71-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="95a71-191">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="95a71-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="95a71-192">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="95a71-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="95a71-193">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="95a71-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="95a71-194">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95a71-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="95a71-195">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="95a71-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="95a71-197">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95a71-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a71-198">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="95a71-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="95a71-200">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="95a71-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="95a71-202">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="95a71-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="95a71-204">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a71-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="95a71-206">a.</span><span class="sxs-lookup"><span data-stu-id="95a71-206">a.</span></span> <span data-ttu-id="95a71-207">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="95a71-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="95a71-208">b.</span><span class="sxs-lookup"><span data-stu-id="95a71-208">b.</span></span> <span data-ttu-id="95a71-209">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="95a71-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="95a71-210">c.</span><span class="sxs-lookup"><span data-stu-id="95a71-210">c.</span></span> <span data-ttu-id="95a71-211">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="95a71-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="95a71-212">d.</span><span class="sxs-lookup"><span data-stu-id="95a71-212">d.</span></span> <span data-ttu-id="95a71-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="95a71-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="95a71-214">Criando de um usuário de teste do Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="95a71-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="95a71-215">tooenable AD do Azure usuários toolog em tooAdaptive Suite, eles devem ser provisionados no pacote adaptável.</span><span class="sxs-lookup"><span data-stu-id="95a71-215">tooenable Azure AD users toolog in tooAdaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="95a71-216">No caso de saudação do pacote adaptável, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="95a71-216">In hello case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="95a71-217">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95a71-217">**tooconfigure user provisioning, perform hello following steps:**</span></span> 

1. <span data-ttu-id="95a71-218">Faça logon no tooyour **pacote adaptável** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="95a71-218">Log in tooyour **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="95a71-219">Vá muito**Admin**.</span><span class="sxs-lookup"><span data-stu-id="95a71-219">Go too**Admin**.</span></span>
   
   <span data-ttu-id="95a71-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="95a71-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="95a71-221">Em Olá **usuários e funções** seção, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="95a71-221">In hello **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="95a71-222">![Adicionar Usuário](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="95a71-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="95a71-223">Em Olá **novo usuário** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95a71-223">In hello **New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="95a71-224">![Enviar](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Enviar")</span><span class="sxs-lookup"><span data-stu-id="95a71-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="95a71-225">a.</span><span class="sxs-lookup"><span data-stu-id="95a71-225">a.</span></span> <span data-ttu-id="95a71-226">Saudação de tipo **nome**, **Login**, **Email**, **senha** de um usuário válido do Active Directory do Azure que você deseja tooprovision em Olá relacionado caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="95a71-226">Type hello **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
  
   <span data-ttu-id="95a71-227">b.</span><span class="sxs-lookup"><span data-stu-id="95a71-227">b.</span></span> <span data-ttu-id="95a71-228">Selecione uma **Função**.</span><span class="sxs-lookup"><span data-stu-id="95a71-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="95a71-229">c.</span><span class="sxs-lookup"><span data-stu-id="95a71-229">c.</span></span> <span data-ttu-id="95a71-230">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="95a71-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="95a71-231">Você pode usar qualquer ferramenta de criação outro pacote adaptável usuário conta ou APIs fornecidas pelo pacote adaptável tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="95a71-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="95a71-232">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95a71-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="95a71-233">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAdaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="95a71-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdaptive Suite.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="95a71-235">**tooassign Britta Simon tooAdaptive Suite, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95a71-235">**tooassign Britta Simon tooAdaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="95a71-236">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="95a71-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="95a71-238">Na lista de aplicativos hello, selecione **pacote adaptável**.</span><span class="sxs-lookup"><span data-stu-id="95a71-238">In hello applications list, select **Adaptive Suite**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="95a71-240">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="95a71-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="95a71-242">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="95a71-242">Click **Add** button.</span></span> <span data-ttu-id="95a71-243">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95a71-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="95a71-245">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="95a71-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="95a71-246">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95a71-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="95a71-247">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95a71-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="95a71-248">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="95a71-248">Testing single sign-on</span></span>

<span data-ttu-id="95a71-249">Olá o objetivo desta seção é tootest seu AD do Microsoft Azure Single Sign-On configuração usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="95a71-249">hello objective of this section is tootest your Microsoft Azure AD Single Sign-On configuration using hello Access Panel.</span></span>

<span data-ttu-id="95a71-250">Quando você clica em um bloco de pacote adaptável Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de pacote adaptável.</span><span class="sxs-lookup"><span data-stu-id="95a71-250">When you click hello Adaptive Suite tile in hello Access Panel, you should get automatically signed-on tooyour Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="95a71-251">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="95a71-251">Additional resources</span></span>

* [<span data-ttu-id="95a71-252">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="95a71-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="95a71-253">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="95a71-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

