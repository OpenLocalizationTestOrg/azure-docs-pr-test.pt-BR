---
title: "Tutorial: Integração do Azure Active Directory ao Boomi | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="18f10-103">Tutorial: Integração do Active Directory do Azure ao Boomi</span><span class="sxs-lookup"><span data-stu-id="18f10-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="18f10-104">Neste tutorial, você aprenderá como toointegrate Boomi com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="18f10-104">In this tutorial, you learn how toointegrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18f10-105">Integrando o Boomi com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="18f10-105">Integrating Boomi with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="18f10-106">Você pode controlar no AD do Azure que tenha acesso tooBoomi</span><span class="sxs-lookup"><span data-stu-id="18f10-106">You can control in Azure AD who has access tooBoomi</span></span>
- <span data-ttu-id="18f10-107">Você pode habilitar seu usuários tooautomatically get conectado tooBoomi (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="18f10-107">You can enable your users tooautomatically get signed-on tooBoomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="18f10-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="18f10-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="18f10-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="18f10-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18f10-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="18f10-110">Prerequisites</span></span>

<span data-ttu-id="18f10-111">tooconfigure integração do AD do Azure com Boomi, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="18f10-111">tooconfigure Azure AD integration with Boomi, you need hello following items:</span></span>

- <span data-ttu-id="18f10-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="18f10-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18f10-113">Uma assinatura habilitada para logon único do Boomi</span><span class="sxs-lookup"><span data-stu-id="18f10-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18f10-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="18f10-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18f10-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="18f10-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18f10-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="18f10-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18f10-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18f10-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18f10-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="18f10-118">Scenario description</span></span>
<span data-ttu-id="18f10-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="18f10-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18f10-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="18f10-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18f10-121">Adicionando Boomi da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="18f10-121">Adding Boomi from hello gallery</span></span>
2. <span data-ttu-id="18f10-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="18f10-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-hello-gallery"></a><span data-ttu-id="18f10-123">Adicionando Boomi da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="18f10-123">Adding Boomi from hello gallery</span></span>
<span data-ttu-id="18f10-124">integração de saudação tooconfigure do Boomi no AD do Azure, você precisa tooadd Boomi da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="18f10-124">tooconfigure hello integration of Boomi into Azure AD, you need tooadd Boomi from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="18f10-125">**tooadd Boomi da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="18f10-125">**tooadd Boomi from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="18f10-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="18f10-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="18f10-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="18f10-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="18f10-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="18f10-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="18f10-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="18f10-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="18f10-133">Na caixa de pesquisa hello, digite **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="18f10-133">In hello search box, type **Boomi**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="18f10-135">No painel de resultados de saudação, selecione **Boomi**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="18f10-135">In hello results panel, select **Boomi**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="18f10-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="18f10-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="18f10-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Boomi, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="18f10-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="18f10-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Boomi é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="18f10-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Boomi is tooa user in Azure AD.</span></span> <span data-ttu-id="18f10-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Boomi precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="18f10-140">In other words, a link relationship between an Azure AD user and hello related user in Boomi needs toobe established.</span></span>

<span data-ttu-id="18f10-141">No Boomi, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="18f10-141">In Boomi, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="18f10-142">tooconfigure e teste de logon único do AD do Azure com Boomi, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="18f10-142">tooconfigure and test Azure AD single sign-on with Boomi, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="18f10-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="18f10-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="18f10-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18f10-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18f10-145">**[Criar um usuário de teste do Boomi](#creating-a-boomi-test-user)**  -toohave um equivalente do Britta Simon no Boomi é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="18f10-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - toohave a counterpart of Britta Simon in Boomi that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="18f10-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="18f10-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18f10-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="18f10-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="18f10-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="18f10-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="18f10-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Boomi.</span><span class="sxs-lookup"><span data-stu-id="18f10-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="18f10-150">**tooconfigure AD do Azure-logon único com Boomi, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="18f10-150">**tooconfigure Azure AD single sign-on with Boomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="18f10-151">Em Olá portal do Azure, Olá **Boomi** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="18f10-151">In hello Azure portal, on hello **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="18f10-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="18f10-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="18f10-155">Em Olá **Boomi domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="18f10-155">On hello **Boomi Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="18f10-157">a.</span><span class="sxs-lookup"><span data-stu-id="18f10-157">a.</span></span> <span data-ttu-id="18f10-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="18f10-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="18f10-159">b.</span><span class="sxs-lookup"><span data-stu-id="18f10-159">b.</span></span> <span data-ttu-id="18f10-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="18f10-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="18f10-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="18f10-161">These values are not real.</span></span> <span data-ttu-id="18f10-162">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="18f10-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="18f10-163">Entre em contato com [equipe de suporte do Boomi](https://boomi.com/company/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="18f10-163">Contact [Boomi support team](https://boomi.com/company/contact/) tooget these values.</span></span>

4. <span data-ttu-id="18f10-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="18f10-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="18f10-166">Aplicativo do Boomi espera asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="18f10-166">Boomi application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="18f10-167">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="18f10-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="18f10-168">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="18f10-168">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="18f10-169">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="18f10-169">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="18f10-171">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, para cada linha mostrada na tabela abaixo, a saudação execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="18f10-171">In hello **User Attributes** section on hello **Single sign-on** dialog, for each row shown in hello table below, perform hello following steps:</span></span>

    | <span data-ttu-id="18f10-172">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="18f10-172">Attribute Name</span></span> | <span data-ttu-id="18f10-173">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="18f10-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="18f10-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="18f10-174">FEDERATION_ID</span></span> | <span data-ttu-id="18f10-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="18f10-175">user.mail</span></span> |
    
    <span data-ttu-id="18f10-176">a.</span><span class="sxs-lookup"><span data-stu-id="18f10-176">a.</span></span> <span data-ttu-id="18f10-177">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="18f10-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="18f10-180">b.</span><span class="sxs-lookup"><span data-stu-id="18f10-180">b.</span></span> <span data-ttu-id="18f10-181">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="18f10-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="18f10-182">c.</span><span class="sxs-lookup"><span data-stu-id="18f10-182">c.</span></span> <span data-ttu-id="18f10-183">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="18f10-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="18f10-184">d.</span><span class="sxs-lookup"><span data-stu-id="18f10-184">d.</span></span> <span data-ttu-id="18f10-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="18f10-185">Click **Ok**.</span></span>

6. <span data-ttu-id="18f10-186">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="18f10-186">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="18f10-188">Em Olá **Boomi configuração** seção, clique em **configurar Boomi** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="18f10-188">On hello **Boomi Configuration** section, click **Configure Boomi** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="18f10-189">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="18f10-189">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="18f10-191">Em outra janela do navegador da Web, faça logon em seu site de empresa Boomi como um administrador.</span><span class="sxs-lookup"><span data-stu-id="18f10-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="18f10-192">Navegue muito**nome da empresa** e vá muito**configurar**.</span><span class="sxs-lookup"><span data-stu-id="18f10-192">Navigate too**Company Name** and go too**Set up**.</span></span>

10. <span data-ttu-id="18f10-193">Clique em Olá **opções SSO** guia e executar etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="18f10-193">Click hello **SSO Options** tab and perform below steps.</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="18f10-195">a.</span><span class="sxs-lookup"><span data-stu-id="18f10-195">a.</span></span> <span data-ttu-id="18f10-196">Marque a caixa de seleção **Habilitar Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="18f10-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="18f10-197">b.</span><span class="sxs-lookup"><span data-stu-id="18f10-197">b.</span></span> <span data-ttu-id="18f10-198">Clique em **importação** Olá tooupload baixado certificado do AD do Azure muito**certificado do provedor de identidade**.</span><span class="sxs-lookup"><span data-stu-id="18f10-198">Click **Import** tooupload hello downloaded certificate from Azure AD too**Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="18f10-199">c.</span><span class="sxs-lookup"><span data-stu-id="18f10-199">c.</span></span> <span data-ttu-id="18f10-200">Em Olá **URL de logon do provedor de identidade** caixa de texto, coloque o valor de saudação do **Single Sign-On URL do serviço SAML** da janela de configuração de aplicativo do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="18f10-200">In hello **Identity Provider Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="18f10-201">d.</span><span class="sxs-lookup"><span data-stu-id="18f10-201">d.</span></span> <span data-ttu-id="18f10-202">Para **Local do ID de Federação**, selecione o botão de opção **A Id de Federação está contida no elemento Atributo FEDERATION_ID**.</span><span class="sxs-lookup"><span data-stu-id="18f10-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="18f10-203">e.</span><span class="sxs-lookup"><span data-stu-id="18f10-203">e.</span></span> <span data-ttu-id="18f10-204">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="18f10-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="18f10-205">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="18f10-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="18f10-206">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="18f10-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="18f10-207">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="18f10-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="18f10-208">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="18f10-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="18f10-209">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="18f10-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="18f10-211">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="18f10-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="18f10-212">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="18f10-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18f10-214">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="18f10-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="18f10-216">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="18f10-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18f10-218">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="18f10-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18f10-220">a.</span><span class="sxs-lookup"><span data-stu-id="18f10-220">a.</span></span> <span data-ttu-id="18f10-221">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18f10-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18f10-222">b.</span><span class="sxs-lookup"><span data-stu-id="18f10-222">b.</span></span> <span data-ttu-id="18f10-223">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="18f10-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="18f10-224">c.</span><span class="sxs-lookup"><span data-stu-id="18f10-224">c.</span></span> <span data-ttu-id="18f10-225">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="18f10-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="18f10-226">d.</span><span class="sxs-lookup"><span data-stu-id="18f10-226">d.</span></span> <span data-ttu-id="18f10-227">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="18f10-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="18f10-228">Criar um usuário de teste do Boomi</span><span class="sxs-lookup"><span data-stu-id="18f10-228">Creating a Boomi test user</span></span>

<span data-ttu-id="18f10-229">Em ordem tooenable AD do Azure usuários toolog em tooBoomi, eles devem ser provisionados no Boomi.</span><span class="sxs-lookup"><span data-stu-id="18f10-229">In order tooenable Azure AD users toolog in tooBoomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="18f10-230">No caso de saudação do Boomi, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="18f10-230">In hello case of Boomi, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="18f10-231">tooprovision uma conta de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="18f10-231">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="18f10-232">Faça logon no tooyour site da empresa Boomi como um administrador.</span><span class="sxs-lookup"><span data-stu-id="18f10-232">Log in tooyour Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="18f10-233">Após o logon, navegue muito**gerenciamento de usuários** e vá muito**usuários**.</span><span class="sxs-lookup"><span data-stu-id="18f10-233">After logging in, navigate too**User Management** and go too**Users**.</span></span>

    <span data-ttu-id="18f10-234">![Usuários](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="18f10-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="18f10-235">Clique em  **+**  ícone e hello **adicionar/manter as funções de usuário** caixa de diálogo é aberta.</span><span class="sxs-lookup"><span data-stu-id="18f10-235">Click **+**  icon and hello **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="18f10-236">![Usuários](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="18f10-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="18f10-237">![Usuários](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="18f10-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="18f10-238">a.</span><span class="sxs-lookup"><span data-stu-id="18f10-238">a.</span></span> <span data-ttu-id="18f10-239">Em Olá **endereço de email do usuário** caixa de texto, como o email de saudação do tipo de usuário BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="18f10-239">In hello **User e-mail address** textbox, type hello email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="18f10-240">b.</span><span class="sxs-lookup"><span data-stu-id="18f10-240">b.</span></span> <span data-ttu-id="18f10-241">Em Olá **nome** caixa de texto, tipo hello primeiro nome do usuário, como Britta.</span><span class="sxs-lookup"><span data-stu-id="18f10-241">In hello **First name** textbox, type hello First name of user like Britta.</span></span>

    <span data-ttu-id="18f10-242">c.</span><span class="sxs-lookup"><span data-stu-id="18f10-242">c.</span></span> <span data-ttu-id="18f10-243">Em Olá **Sobrenome** caixa de texto, digite Olá sobrenome do usuário como Simon.</span><span class="sxs-lookup"><span data-stu-id="18f10-243">In hello **Last name** textbox, type hello Last name of user like Simon.</span></span>
    
    <span data-ttu-id="18f10-244">d.</span><span class="sxs-lookup"><span data-stu-id="18f10-244">d.</span></span> <span data-ttu-id="18f10-245">Insira saudação do usuário **ID da federação**.</span><span class="sxs-lookup"><span data-stu-id="18f10-245">Enter hello user's **Federation ID**.</span></span> <span data-ttu-id="18f10-246">Cada usuário deve ter uma ID de federação que identifica exclusivamente o usuário Olá na conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="18f10-246">Each user must have a Federation ID that uniquely identifies hello user within hello account.</span></span>
    
    <span data-ttu-id="18f10-247">e.</span><span class="sxs-lookup"><span data-stu-id="18f10-247">e.</span></span> <span data-ttu-id="18f10-248">Atribuir Olá **usuário padrão** usuário de toohello de função.</span><span class="sxs-lookup"><span data-stu-id="18f10-248">Assign hello **Standard User** role toohello user.</span></span> <span data-ttu-id="18f10-249">Não atribua a função de administrador de saudação porque que poderia dar a ele acesso atmosfera normal, bem como acesso de logon único.</span><span class="sxs-lookup"><span data-stu-id="18f10-249">Do not assign hello Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="18f10-250">f.</span><span class="sxs-lookup"><span data-stu-id="18f10-250">f.</span></span> <span data-ttu-id="18f10-251">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="18f10-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="18f10-252">usuário de saudação não receberá um email de notificação de boas-vindas contendo uma senha que pode ser usado toolog em toohello AtomSphere conta porque sua senha é gerenciada por meio do provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="18f10-252">hello user will not receive a welcome notification email containing a password that can be used toolog in toohello AtomSphere account because his password is managed through hello identity provider.</span></span> <span data-ttu-id="18f10-253">Você pode usar qualquer ferramenta de criação outros Boomi usuário conta ou APIs fornecidas pelo Boomi tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="18f10-253">You may use any other Boomi user account creation tools or APIs provided by Boomi tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="18f10-254">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="18f10-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="18f10-255">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBoomi.</span><span class="sxs-lookup"><span data-stu-id="18f10-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBoomi.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="18f10-257">**tooassign Britta Simon tooBoomi, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="18f10-257">**tooassign Britta Simon tooBoomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="18f10-258">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="18f10-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="18f10-260">Na lista de aplicativos hello, selecione **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="18f10-260">In hello applications list, select **Boomi**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="18f10-262">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="18f10-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="18f10-264">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="18f10-264">Click **Add** button.</span></span> <span data-ttu-id="18f10-265">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="18f10-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="18f10-267">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="18f10-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="18f10-268">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="18f10-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18f10-269">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="18f10-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="18f10-270">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="18f10-270">Testing single sign-on</span></span>

<span data-ttu-id="18f10-271">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="18f10-271">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="18f10-272">Quando você clica em bloco Boomi Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Boomi aplicativo.</span><span class="sxs-lookup"><span data-stu-id="18f10-272">When you click hello Boomi tile in hello Access Panel, you should get automatically signed-on tooyour Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18f10-273">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="18f10-273">Additional resources</span></span>

* [<span data-ttu-id="18f10-274">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="18f10-274">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18f10-275">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="18f10-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

