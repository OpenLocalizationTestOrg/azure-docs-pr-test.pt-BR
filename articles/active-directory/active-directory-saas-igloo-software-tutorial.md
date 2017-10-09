---
title: "Tutorial: integração do Azure Active Directory com o Igloo Software | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Igloo Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="ca444-103">Tutorial: integração do Active Directory do Azure ao Igloo Software</span><span class="sxs-lookup"><span data-stu-id="ca444-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="ca444-104">Neste tutorial, você aprenderá como toointegrate Igloo Software com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="ca444-104">In this tutorial, you learn how toointegrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ca444-105">Integrando o Igloo Software com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca444-105">Integrating Igloo Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ca444-106">Você pode controlar no AD do Azure que tenha acesso tooIgloo Software</span><span class="sxs-lookup"><span data-stu-id="ca444-106">You can control in Azure AD who has access tooIgloo Software</span></span>
- <span data-ttu-id="ca444-107">Você pode habilitar seu usuários tooautomatically get conectado tooIgloo Software (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ca444-107">You can enable your users tooautomatically get signed-on tooIgloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ca444-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ca444-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ca444-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ca444-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca444-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ca444-110">Prerequisites</span></span>

<span data-ttu-id="ca444-111">tooconfigure integração do AD do Azure com o Igloo Software, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca444-111">tooconfigure Azure AD integration with Igloo Software, you need hello following items:</span></span>

- <span data-ttu-id="ca444-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ca444-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ca444-113">Uma assinatura do Igloo Software habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="ca444-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ca444-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ca444-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ca444-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ca444-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ca444-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ca444-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ca444-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ca444-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ca444-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ca444-118">Scenario description</span></span>
<span data-ttu-id="ca444-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ca444-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ca444-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="ca444-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ca444-121">Adicionando Igloo Software da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ca444-121">Adding Igloo Software from hello gallery</span></span>
2. <span data-ttu-id="ca444-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ca444-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-hello-gallery"></a><span data-ttu-id="ca444-123">Adicionando Igloo Software da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ca444-123">Adding Igloo Software from hello gallery</span></span>
<span data-ttu-id="ca444-124">integração de saudação tooconfigure do Igloo Software no AD do Azure, você precisa tooadd Igloo Software na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ca444-124">tooconfigure hello integration of Igloo Software into Azure AD, you need tooadd Igloo Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ca444-125">**tooadd Igloo Software da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ca444-125">**tooadd Igloo Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca444-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ca444-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ca444-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ca444-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ca444-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ca444-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ca444-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ca444-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ca444-133">Na caixa de pesquisa hello, digite **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="ca444-133">In hello search box, type **Igloo Software**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="ca444-135">No painel de resultados de saudação, selecione **Igloo Software**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ca444-135">In hello results panel, select **Igloo Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ca444-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ca444-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ca444-138">Nesta seção, você configura e testa o logon único do Azure AD com o Igloo Software com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ca444-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ca444-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Igloo Software é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca444-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Igloo Software is tooa user in Azure AD.</span></span> <span data-ttu-id="ca444-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Igloo Software precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ca444-140">In other words, a link relationship between an Azure AD user and hello related user in Igloo Software needs toobe established.</span></span>

<span data-ttu-id="ca444-141">No Igloo Software, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca444-141">In Igloo Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ca444-142">tooconfigure e teste de logon único do AD do Azure com o Igloo Software, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca444-142">tooconfigure and test Azure AD single sign-on with Igloo Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ca444-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ca444-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ca444-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca444-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ca444-145">**[Criar um usuário de teste do Igloo Software](#creating-an-igloo-software-test-user)**  -toohave um equivalente do Britta Simon no Igloo Software que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="ca444-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - toohave a counterpart of Britta Simon in Igloo Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ca444-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="ca444-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ca444-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="ca444-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ca444-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca444-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ca444-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="ca444-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="ca444-150">**tooconfigure AD do Azure-logon único com o Igloo Software, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ca444-150">**tooconfigure Azure AD single sign-on with Igloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca444-151">Em Olá portal do Azure, Olá **Igloo Software** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="ca444-151">In hello Azure portal, on hello **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ca444-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="ca444-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="ca444-155">Em Olá **Igloo Software domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca444-155">On hello **Igloo Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="ca444-157">a.</span><span class="sxs-lookup"><span data-stu-id="ca444-157">a.</span></span> <span data-ttu-id="ca444-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="ca444-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="ca444-159">b.</span><span class="sxs-lookup"><span data-stu-id="ca444-159">b.</span></span> <span data-ttu-id="ca444-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="ca444-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="ca444-161">c.</span><span class="sxs-lookup"><span data-stu-id="ca444-161">c.</span></span> <span data-ttu-id="ca444-162">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="ca444-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ca444-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="ca444-163">These values are not real.</span></span> <span data-ttu-id="ca444-164">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="ca444-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="ca444-165">Entre em contato com [equipe de suporte do Igloo Software cliente](https://www.igloosoftware.com/services/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="ca444-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="ca444-166">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ca444-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="ca444-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ca444-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ca444-170">Em Olá **Igloo Software configuração** seção, clique em **configurar Igloo Software** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="ca444-170">On hello **Igloo Software Configuration** section, click **Configure Igloo Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ca444-171">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="ca444-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="ca444-173">Em uma janela de navegador web diferente, faça logon no site da empresa tooyour Igloo Software como um administrador.</span><span class="sxs-lookup"><span data-stu-id="ca444-173">In a different web browser window, log in tooyour Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="ca444-174">Vá toohello **painel de controle**.</span><span class="sxs-lookup"><span data-stu-id="ca444-174">Go toohello **Control Panel**.</span></span>
   
     <span data-ttu-id="ca444-175">![Painel de controle](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Painel de controle")</span><span class="sxs-lookup"><span data-stu-id="ca444-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="ca444-176">Em Olá **associação** , clique em **configurações de entrada**.</span><span class="sxs-lookup"><span data-stu-id="ca444-176">In hello **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="ca444-177">![Configurações de entrada](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Configurações de entrada")</span><span class="sxs-lookup"><span data-stu-id="ca444-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="ca444-178">No hello seção de configuração do SAML, clique em **configurar autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="ca444-178">In hello SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="ca444-179">![Configuração SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "configuração SAML")</span><span class="sxs-lookup"><span data-stu-id="ca444-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="ca444-180">Em Olá **configuração geral** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca444-180">In hello **General Configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ca444-181">![Configuração geral](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "Configuração geral")</span><span class="sxs-lookup"><span data-stu-id="ca444-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="ca444-182">a.</span><span class="sxs-lookup"><span data-stu-id="ca444-182">a.</span></span> <span data-ttu-id="ca444-183">Em Olá **nome de Conexão** caixa de texto, digite um nome personalizado para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="ca444-183">In hello **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="ca444-184">b.</span><span class="sxs-lookup"><span data-stu-id="ca444-184">b.</span></span> <span data-ttu-id="ca444-185">Em Olá **URL de logon IdP** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca444-185">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="ca444-186">c.</span><span class="sxs-lookup"><span data-stu-id="ca444-186">c.</span></span> <span data-ttu-id="ca444-187">Em Olá **URL de Logout IdP** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca444-187">In hello **IdP Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="ca444-188">d.</span><span class="sxs-lookup"><span data-stu-id="ca444-188">d.</span></span> <span data-ttu-id="ca444-189">Selecione **Tipo HTTP de Solicitação e Resposta de Logoff** como **POST**.</span><span class="sxs-lookup"><span data-stu-id="ca444-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="ca444-190">e.</span><span class="sxs-lookup"><span data-stu-id="ca444-190">e.</span></span> <span data-ttu-id="ca444-191">Abra seu **base 64** codificado certificado baixado do portal do Azure, Olá de copiar conteúdo dele para sua área de transferência, o bloco de notas e, em seguida, cole-o toohello **certificado público** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="ca444-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="ca444-192">Em Olá **resposta e a configuração de autenticação**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca444-192">In hello **Response and Authentication Configuration**, perform hello following steps:</span></span>
    
    <span data-ttu-id="ca444-193">![Configuração de autenticação e resposta](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Configuração de autenticação e resposta")</span><span class="sxs-lookup"><span data-stu-id="ca444-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="ca444-194">a.</span><span class="sxs-lookup"><span data-stu-id="ca444-194">a.</span></span> <span data-ttu-id="ca444-195">Para **Provedor de Identidade**, selecione **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="ca444-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="ca444-196">b.</span><span class="sxs-lookup"><span data-stu-id="ca444-196">b.</span></span> <span data-ttu-id="ca444-197">Para **Tipo de Identificador**, selecione **Endereço de Email**.</span><span class="sxs-lookup"><span data-stu-id="ca444-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="ca444-198">c.</span><span class="sxs-lookup"><span data-stu-id="ca444-198">c.</span></span> <span data-ttu-id="ca444-199">Em Olá **Email atributo** caixa de texto, tipo **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="ca444-199">In hello **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="ca444-200">d.</span><span class="sxs-lookup"><span data-stu-id="ca444-200">d.</span></span> <span data-ttu-id="ca444-201">Em Olá **atributo de nome** caixa de texto, tipo **givenname**.</span><span class="sxs-lookup"><span data-stu-id="ca444-201">In hello **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="ca444-202">e.</span><span class="sxs-lookup"><span data-stu-id="ca444-202">e.</span></span> <span data-ttu-id="ca444-203">Em Olá **último nome de atributo** caixa de texto, tipo **Sobrenome**.</span><span class="sxs-lookup"><span data-stu-id="ca444-203">In hello **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="ca444-204">Execute Olá configuração de saudação do toocomplete as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca444-204">Perform hello following steps toocomplete hello configuration:</span></span>
    
    <span data-ttu-id="ca444-205">![Criação de usuário na entrada](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "Criação de usuário na entrada")</span><span class="sxs-lookup"><span data-stu-id="ca444-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="ca444-206">a.</span><span class="sxs-lookup"><span data-stu-id="ca444-206">a.</span></span> <span data-ttu-id="ca444-207">Para **Criação de usuário na Entrada**, selecione **Criar um novo usuário em seu site ao entrar**.</span><span class="sxs-lookup"><span data-stu-id="ca444-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="ca444-208">b.</span><span class="sxs-lookup"><span data-stu-id="ca444-208">b.</span></span> <span data-ttu-id="ca444-209">Para **Configurações de Entrada**, selecione **Usar botão do SAML na tela “Entrar”**.</span><span class="sxs-lookup"><span data-stu-id="ca444-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="ca444-210">c.</span><span class="sxs-lookup"><span data-stu-id="ca444-210">c.</span></span> <span data-ttu-id="ca444-211">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ca444-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ca444-212">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="ca444-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ca444-213">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ca444-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ca444-214">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ca444-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ca444-215">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ca444-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="ca444-216">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca444-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ca444-218">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ca444-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca444-219">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ca444-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ca444-221">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="ca444-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ca444-223">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca444-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ca444-225">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca444-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ca444-227">a.</span><span class="sxs-lookup"><span data-stu-id="ca444-227">a.</span></span> <span data-ttu-id="ca444-228">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ca444-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ca444-229">b.</span><span class="sxs-lookup"><span data-stu-id="ca444-229">b.</span></span> <span data-ttu-id="ca444-230">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ca444-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ca444-231">c.</span><span class="sxs-lookup"><span data-stu-id="ca444-231">c.</span></span> <span data-ttu-id="ca444-232">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="ca444-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ca444-233">d.</span><span class="sxs-lookup"><span data-stu-id="ca444-233">d.</span></span> <span data-ttu-id="ca444-234">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ca444-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="ca444-235">Como criar um usuário de teste do Igloo Software</span><span class="sxs-lookup"><span data-stu-id="ca444-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="ca444-236">Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooIgloo Software.</span><span class="sxs-lookup"><span data-stu-id="ca444-236">There is no action item for you tooconfigure user provisioning tooIgloo Software.</span></span>  

<span data-ttu-id="ca444-237">Quando um usuário atribuído tenta toolog em tooIgloo Software usando o painel de acesso hello, Igloo Software verifica se o usuário Olá existe.</span><span class="sxs-lookup"><span data-stu-id="ca444-237">When an assigned user tries toolog in tooIgloo Software using hello access panel, Igloo Software checks whether hello user exists.</span></span>  <span data-ttu-id="ca444-238">Se ainda não houver conta de usuário, ela será criada automaticamente pelo Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="ca444-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ca444-239">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ca444-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ca444-240">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooIgloo Software.</span><span class="sxs-lookup"><span data-stu-id="ca444-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIgloo Software.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ca444-242">**tooassign Britta Simon tooIgloo Software, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ca444-242">**tooassign Britta Simon tooIgloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca444-243">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ca444-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ca444-245">Na lista de aplicativos hello, selecione **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="ca444-245">In hello applications list, select **Igloo Software**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="ca444-247">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ca444-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ca444-249">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ca444-249">Click **Add** button.</span></span> <span data-ttu-id="ca444-250">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ca444-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ca444-252">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca444-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ca444-253">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ca444-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ca444-254">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ca444-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ca444-255">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ca444-255">Testing single sign-on</span></span>

<span data-ttu-id="ca444-256">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca444-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ca444-257">Quando você clica em bloco Igloo Software Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="ca444-257">When you click hello Igloo Software tile in hello Access Panel, you should get automatically signed-on tooyour Igloo Software application.</span></span>
<span data-ttu-id="ca444-258">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ca444-258">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ca444-259">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ca444-259">Additional resources</span></span>

* [<span data-ttu-id="ca444-260">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ca444-260">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ca444-261">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ca444-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

