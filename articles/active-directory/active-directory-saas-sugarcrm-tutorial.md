---
title: "Tutorial: integração do Azure Active Directory ao Sugar CRM | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Sugar CRM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 108d2f8125e410743ee7bc48883a1d0b00602615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="1bba7-103">Tutorial: integração do Azure Active Directory ao Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="1bba7-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="1bba7-104">Neste tutorial, você aprenderá como toointegrate Sugar CRM com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="1bba7-104">In this tutorial, you learn how toointegrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1bba7-105">Integrando o Sugar CRM com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bba7-105">Integrating Sugar CRM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1bba7-106">Você pode controlar no AD do Azure que tenha acesso tooSugar CRM</span><span class="sxs-lookup"><span data-stu-id="1bba7-106">You can control in Azure AD who has access tooSugar CRM</span></span>
- <span data-ttu-id="1bba7-107">Você pode habilitar seu usuários tooautomatically get conectado tooSugar CRM (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1bba7-107">You can enable your users tooautomatically get signed-on tooSugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1bba7-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1bba7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1bba7-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1bba7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bba7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1bba7-110">Prerequisites</span></span>

<span data-ttu-id="1bba7-111">tooconfigure integração do AD do Azure com o Sugar CRM, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bba7-111">tooconfigure Azure AD integration with Sugar CRM, you need hello following items:</span></span>

- <span data-ttu-id="1bba7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1bba7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1bba7-113">Uma assinatura do Sugar CRM habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="1bba7-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1bba7-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1bba7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1bba7-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1bba7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1bba7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1bba7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1bba7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1bba7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1bba7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1bba7-118">Scenario description</span></span>
<span data-ttu-id="1bba7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1bba7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1bba7-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="1bba7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1bba7-121">Adicionando Sugar CRM da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1bba7-121">Adding Sugar CRM from hello gallery</span></span>
2. <span data-ttu-id="1bba7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1bba7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-hello-gallery"></a><span data-ttu-id="1bba7-123">Adicionando Sugar CRM da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1bba7-123">Adding Sugar CRM from hello gallery</span></span>
<span data-ttu-id="1bba7-124">integração de saudação tooconfigure do Sugar CRM no AD do Azure, você precisa tooadd Sugar CRM na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1bba7-124">tooconfigure hello integration of Sugar CRM into Azure AD, you need tooadd Sugar CRM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1bba7-125">**tooadd Sugar CRM da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1bba7-125">**tooadd Sugar CRM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bba7-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1bba7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1bba7-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1bba7-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1bba7-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1bba7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1bba7-133">Na caixa de pesquisa hello, digite **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-133">In hello search box, type **Sugar CRM**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="1bba7-135">No painel de resultados de saudação, selecione **Sugar CRM**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1bba7-135">In hello results panel, select **Sugar CRM**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1bba7-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1bba7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1bba7-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Sugar CRM, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="1bba7-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1bba7-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Sugar CRM é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1bba7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sugar CRM is tooa user in Azure AD.</span></span> <span data-ttu-id="1bba7-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação do Sugar CRM precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1bba7-140">In other words, a link relationship between an Azure AD user and hello related user in Sugar CRM needs toobe established.</span></span>

<span data-ttu-id="1bba7-141">No Sugar CRM, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bba7-141">In Sugar CRM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1bba7-142">tooconfigure e teste de logon único do AD do Azure com o Sugar CRM, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bba7-142">tooconfigure and test Azure AD single sign-on with Sugar CRM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1bba7-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1bba7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1bba7-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1bba7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1bba7-145">**[Criar um usuário de teste do Sugar CRM](#creating-a-sugar-crm-test-user)**  -toohave um equivalente do Britta Simon no Sugar CRM é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="1bba7-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - toohave a counterpart of Britta Simon in Sugar CRM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1bba7-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="1bba7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1bba7-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="1bba7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1bba7-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bba7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1bba7-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="1bba7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="1bba7-150">**tooconfigure AD do Azure-logon único com o Sugar CRM, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1bba7-150">**tooconfigure Azure AD single sign-on with Sugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bba7-151">Em Olá portal do Azure, Olá **Sugar CRM** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-151">In hello Azure portal, on hello **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1bba7-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="1bba7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="1bba7-155">Em Olá **Sugar CRM domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bba7-155">On hello **Sugar CRM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="1bba7-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bba7-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="1bba7-158">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="1bba7-158">hello value is not real.</span></span> <span data-ttu-id="1bba7-159">Valor de saudação de atualização com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="1bba7-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1bba7-160">Entre em contato com [equipe de suporte do Sugar CRM cliente](https://support.sugarcrm.com/) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bba7-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="1bba7-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1bba7-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="1bba7-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1bba7-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1bba7-165">Em Olá **Sugar CRM configuração** seção, clique em **configurar Sugar CRM** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="1bba7-165">On hello **Sugar CRM Configuration** section, click **Configure Sugar CRM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1bba7-166">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="1bba7-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="1bba7-168">Em uma janela de navegador web diferente, faça logon no site da empresa tooyour Sugar CRM como um administrador.</span><span class="sxs-lookup"><span data-stu-id="1bba7-168">In a different web browser window, log in tooyour Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="1bba7-169">Vá muito**Admin**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-169">Go too**Admin**.</span></span>
   
    <span data-ttu-id="1bba7-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="1bba7-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="1bba7-171">Em Olá **administração** seção, clique em **gerenciamento de senha**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-171">In hello **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="1bba7-172">![Administração](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="1bba7-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="1bba7-173">Selecione **Habilitar Autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="1bba7-174">![Administração](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="1bba7-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="1bba7-175">Em Olá **autenticação SAML** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bba7-175">In hello **SAML Authentication** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1bba7-176">![Autenticação SAML](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "Autenticação SAML")</span><span class="sxs-lookup"><span data-stu-id="1bba7-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="1bba7-177">a.</span><span class="sxs-lookup"><span data-stu-id="1bba7-177">a.</span></span> <span data-ttu-id="1bba7-178">Em Olá **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1bba7-178">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="1bba7-179">b.</span><span class="sxs-lookup"><span data-stu-id="1bba7-179">b.</span></span> <span data-ttu-id="1bba7-180">Em Olá **URL de SLO** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1bba7-180">In hello **SLO URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="1bba7-181">c.</span><span class="sxs-lookup"><span data-stu-id="1bba7-181">c.</span></span> <span data-ttu-id="1bba7-182">Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e cole Olá certificado inteiro na **certificado x. 509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="1bba7-182">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="1bba7-183">d.</span><span class="sxs-lookup"><span data-stu-id="1bba7-183">d.</span></span> <span data-ttu-id="1bba7-184">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1bba7-185">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="1bba7-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1bba7-186">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="1bba7-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1bba7-187">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1bba7-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1bba7-188">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1bba7-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="1bba7-189">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1bba7-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1bba7-191">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1bba7-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bba7-192">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1bba7-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1bba7-194">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1bba7-196">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bba7-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1bba7-198">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bba7-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1bba7-200">a.</span><span class="sxs-lookup"><span data-stu-id="1bba7-200">a.</span></span> <span data-ttu-id="1bba7-201">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1bba7-202">b.</span><span class="sxs-lookup"><span data-stu-id="1bba7-202">b.</span></span> <span data-ttu-id="1bba7-203">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1bba7-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1bba7-204">c.</span><span class="sxs-lookup"><span data-stu-id="1bba7-204">c.</span></span> <span data-ttu-id="1bba7-205">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1bba7-206">d.</span><span class="sxs-lookup"><span data-stu-id="1bba7-206">d.</span></span> <span data-ttu-id="1bba7-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="1bba7-208">Criar um usuário de teste do Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="1bba7-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="1bba7-209">Ordem tooenable AD do Azure usuários toolog em tooSugar CRM, elas devem ser provisionado tooSugar CRM.</span><span class="sxs-lookup"><span data-stu-id="1bba7-209">In order tooenable Azure AD users toolog in tooSugar CRM, they must be provisioned tooSugar CRM.</span></span>

<span data-ttu-id="1bba7-210">No caso de saudação do Sugar CRM, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="1bba7-210">In hello case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="1bba7-211">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1bba7-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bba7-212">Faça logon no tooyour **Sugar CRM** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="1bba7-212">Log in tooyour **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="1bba7-213">Vá muito**Admin**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-213">Go too**Admin**.</span></span>
   
    <span data-ttu-id="1bba7-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="1bba7-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="1bba7-215">Em Olá **administração** seção, clique em **gerenciamento de usuário**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-215">In hello **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="1bba7-216">![Administração](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="1bba7-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="1bba7-217">Vá muito**usuários \> criar novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-217">Go too**Users \> Create New User**.</span></span>
   
    <span data-ttu-id="1bba7-218">![Criar Novo Usuário](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Criar Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="1bba7-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="1bba7-219">Em Olá **perfil de usuário** guia, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bba7-219">On hello **User Profile** tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="1bba7-220">![Novo Usuário](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="1bba7-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="1bba7-221">a.</span><span class="sxs-lookup"><span data-stu-id="1bba7-221">a.</span></span> <span data-ttu-id="1bba7-222">Saudação de tipo **nome de usuário**, **Sobrenome**, e **endereço de email** de um usuário válido do Active Directory do Azure em Olá relacionados caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="1bba7-222">Type hello **user name**, **last name**, and **email address** of a valid Azure Active Directory user into hello related textboxes.</span></span>
  
6. <span data-ttu-id="1bba7-223">Para **Status**, selecione **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="1bba7-224">Na guia de senha hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bba7-224">On hello Password tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="1bba7-225">![Novo Usuário](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="1bba7-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="1bba7-226">a.</span><span class="sxs-lookup"><span data-stu-id="1bba7-226">a.</span></span> <span data-ttu-id="1bba7-227">Digite a senha em Olá Olá relacionadas a caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="1bba7-227">Type hello password into hello related textbox.</span></span>

    <span data-ttu-id="1bba7-228">b.</span><span class="sxs-lookup"><span data-stu-id="1bba7-228">b.</span></span> <span data-ttu-id="1bba7-229">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="1bba7-230">Você pode usar qualquer ferramenta de criação outros Sugar CRM usuário conta ou APIs fornecidas pelo Sugar CRM tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="1bba7-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1bba7-231">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1bba7-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1bba7-232">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSugar CRM.</span><span class="sxs-lookup"><span data-stu-id="1bba7-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSugar CRM.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1bba7-234">**tooassign Britta Simon tooSugar CRM, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1bba7-234">**tooassign Britta Simon tooSugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bba7-235">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1bba7-237">Na lista de aplicativos hello, selecione **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-237">In hello applications list, select **Sugar CRM**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="1bba7-239">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1bba7-241">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1bba7-241">Click **Add** button.</span></span> <span data-ttu-id="1bba7-242">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1bba7-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1bba7-244">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="1bba7-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1bba7-245">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1bba7-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1bba7-246">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1bba7-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1bba7-247">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1bba7-247">Testing single sign-on</span></span>

<span data-ttu-id="1bba7-248">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="1bba7-248">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1bba7-249">Quando você clica em bloco Sugar CRM Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="1bba7-249">When you click hello Sugar CRM tile in hello Access Panel, you should get automatically signed-on tooyour Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1bba7-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1bba7-250">Additional resources</span></span>

* [<span data-ttu-id="1bba7-251">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1bba7-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1bba7-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1bba7-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

