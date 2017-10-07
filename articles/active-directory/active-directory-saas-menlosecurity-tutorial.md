---
title: "Tutorial: Integração do Azure Active Directory com o Menlo Security | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Menlo segurança."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 193d12eedf31f4f08e1d141936d6e918c36a2109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="a4cb5-103">Tutorial: Integração do Azure Active Directory com o Menlo Security</span><span class="sxs-lookup"><span data-stu-id="a4cb5-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="a4cb5-104">Neste tutorial, você aprenderá como toointegrate Menlo segurança com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="a4cb5-104">In this tutorial, you learn how toointegrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a4cb5-105">Integração de segurança Menlo com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4cb5-105">Integrating Menlo Security with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a4cb5-106">Você pode controlar no AD do Azure que tenha acesso tooMenlo segurança</span><span class="sxs-lookup"><span data-stu-id="a4cb5-106">You can control in Azure AD who has access tooMenlo Security</span></span>
- <span data-ttu-id="a4cb5-107">Você pode habilitar seu usuários tooautomatically get conectado tooMenlo segurança (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a4cb5-107">You can enable your users tooautomatically get signed-on tooMenlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a4cb5-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a4cb5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a4cb5-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="a4cb5-110">[O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a4cb5-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4cb5-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a4cb5-111">Prerequisites</span></span>

<span data-ttu-id="a4cb5-112">tooconfigure integração do AD do Azure com segurança Menlo, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4cb5-112">tooconfigure Azure AD integration with Menlo Security, you need hello following items:</span></span>

- <span data-ttu-id="a4cb5-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a4cb5-113">An Azure AD subscription</span></span>
- <span data-ttu-id="a4cb5-114">Uma assinatura do Menlo Security habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="a4cb5-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a4cb5-115">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a4cb5-116">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a4cb5-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a4cb5-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a4cb5-118">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4cb5-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a4cb5-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a4cb5-119">Scenario description</span></span>
<span data-ttu-id="a4cb5-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a4cb5-121">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="a4cb5-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a4cb5-122">Adicionando segurança Menlo da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a4cb5-122">Adding Menlo Security from hello gallery</span></span>
2. <span data-ttu-id="a4cb5-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a4cb5-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-hello-gallery"></a><span data-ttu-id="a4cb5-124">Adicionando segurança Menlo da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a4cb5-124">Adding Menlo Security from hello gallery</span></span>
<span data-ttu-id="a4cb5-125">integração de Olá tooconfigure de Menlo segurança no AD do Azure, você precisa tooadd Menlo segurança da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-125">tooconfigure hello integration of Menlo Security into Azure AD, you need tooadd Menlo Security from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a4cb5-126">**tooadd segurança Menlo da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a4cb5-126">**tooadd Menlo Security from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4cb5-127">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a4cb5-129">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a4cb5-130">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-130">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a4cb5-132">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a4cb5-134">Na caixa de pesquisa hello, digite **Menlo segurança**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-134">In hello search box, type **Menlo Security**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="a4cb5-136">No painel de resultados de saudação, selecione **Menlo segurança**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-136">In hello results panel, select **Menlo Security**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a4cb5-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a4cb5-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a4cb5-139">Nesta seção, você configura e testa o logon único do Azure AD com o Menlo Security com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a4cb5-140">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em segurança Menlo é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Menlo Security is tooa user in Azure AD.</span></span> <span data-ttu-id="a4cb5-141">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em segurança Menlo precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-141">In other words, a link relationship between an Azure AD user and hello related user in Menlo Security needs toobe established.</span></span>

<span data-ttu-id="a4cb5-142">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em segurança Menlo.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Menlo Security.</span></span>

<span data-ttu-id="a4cb5-143">tooconfigure e teste de logon único do AD do Azure com segurança Menlo, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4cb5-143">tooconfigure and test Azure AD single sign-on with Menlo Security, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a4cb5-144">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a4cb5-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a4cb5-146">**[Criar um usuário de teste de segurança Menlo](#creating-a-menlo-security-test-user)**  -toohave um equivalente do Britta Simon em segurança Menlo toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - toohave a counterpart of Britta Simon in Menlo Security that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a4cb5-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a4cb5-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a4cb5-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4cb5-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a4cb5-150">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de segurança de Menlo.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="a4cb5-151">**tooconfigure AD do Azure-logon único com segurança Menlo, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a4cb5-151">**tooconfigure Azure AD single sign-on with Menlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4cb5-152">Em Olá portal do Azure, Olá **Menlo segurança** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-152">In hello Azure portal, on hello **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a4cb5-154">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="a4cb5-156">Em Olá **Menlo domínio de segurança e as URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4cb5-156">On hello **Menlo Security Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="a4cb5-158">a.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-158">a.</span></span> <span data-ttu-id="a4cb5-159">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="a4cb5-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="a4cb5-160">b.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-160">b.</span></span> <span data-ttu-id="a4cb5-161">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="a4cb5-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a4cb5-162">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-162">These values are not hello real.</span></span> <span data-ttu-id="a4cb5-163">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a4cb5-164">Entre em contato com [equipe de suporte de cliente de segurança Menlo](https://www.menlosecurity.com/menlo-contact) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="a4cb5-165">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="a4cb5-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a4cb5-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a4cb5-169">Em hello **a configuração de segurança Menlo** seção, clique em **configurar segurança de Menlo** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-169">On hello **Menlo Security Configuration** section, click **Configure Menlo Security** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a4cb5-170">Saudação de cópia **ID da entidade SAML**, e **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="a4cb5-170">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="a4cb5-172">tooconfigure logon único no **Menlo segurança** lado, o logon toohello **Menlo segurança** site como um administrador.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-172">tooconfigure single sign-on on **Menlo Security** side, login toohello **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="a4cb5-173">Em **configurações** ir muito**autenticação** e executar as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="a4cb5-173">Under **Settings** go too**Authentication** and perform following actions:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="a4cb5-175">a.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-175">a.</span></span> <span data-ttu-id="a4cb5-176">Caixa de seleção de saudação de escala **habilitar a autenticação do usuário usando SAML**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-176">Tick hello checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="a4cb5-177">b.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-177">b.</span></span> <span data-ttu-id="a4cb5-178">Selecione **permitir acesso externo** muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-178">Select **Allow External Access** too**Yes**.</span></span>

    <span data-ttu-id="a4cb5-179">c.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-179">c.</span></span> <span data-ttu-id="a4cb5-180">Em **Provedor SAML**, selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="a4cb5-181">d.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-181">d.</span></span> <span data-ttu-id="a4cb5-182">**O ponto de extremidade do SAML 2.0** : Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-182">**SAML 2.0 Endpoint** : Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a4cb5-183">e.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-183">e.</span></span> <span data-ttu-id="a4cb5-184">**Identificador de serviço (emissor)** : Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-184">**Service Identifier (Issuer)** : Paste hello **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a4cb5-185">f.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-185">f.</span></span> <span data-ttu-id="a4cb5-186">**Certificado x. 509** : Olá abrir **certificado (Base64)** baixado da saudação Portal do Azure no bloco de notas e cole-o nesta caixa.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-186">**X.509 Certificate** : Open hello **Certificate (Base64)** downloaded from hello Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="a4cb5-187">g.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-187">g.</span></span> <span data-ttu-id="a4cb5-188">Clique em **salvar** toosave configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-188">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="a4cb5-189">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="a4cb5-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a4cb5-190">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a4cb5-191">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a4cb5-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a4cb5-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a4cb5-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="a4cb5-193">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a4cb5-195">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a4cb5-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4cb5-196">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a4cb5-198">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a4cb5-200">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a4cb5-202">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4cb5-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a4cb5-204">a.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-204">a.</span></span> <span data-ttu-id="a4cb5-205">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a4cb5-206">b.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-206">b.</span></span> <span data-ttu-id="a4cb5-207">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a4cb5-208">c.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-208">c.</span></span> <span data-ttu-id="a4cb5-209">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a4cb5-210">d.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-210">d.</span></span> <span data-ttu-id="a4cb5-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="a4cb5-212">Criar um usuário de teste do Menlo Security</span><span class="sxs-lookup"><span data-stu-id="a4cb5-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="a4cb5-213">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="a4cb5-214">Trabalhar com [equipe de suporte de cliente de segurança Menlo](https://www.menlosecurity.com/menlo-contact) tooadd usuários de saudação na plataforma de segurança Menlo hello.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooadd hello users in hello Menlo Security platform.</span></span> <span data-ttu-id="a4cb5-215">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a4cb5-216">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a4cb5-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a4cb5-217">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMenlo segurança.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMenlo Security.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a4cb5-219">**tooassign Britta Simon tooMenlo segurança, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a4cb5-219">**tooassign Britta Simon tooMenlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4cb5-220">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a4cb5-222">Na lista de aplicativos hello, selecione **Menlo segurança**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-222">In hello applications list, select **Menlo Security**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="a4cb5-224">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a4cb5-226">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-226">Click **Add** button.</span></span> <span data-ttu-id="a4cb5-227">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a4cb5-229">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a4cb5-230">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a4cb5-231">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a4cb5-232">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a4cb5-232">Testing single sign-on</span></span>

<span data-ttu-id="a4cb5-233">Nesta seção, você testará sua configuração de logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="a4cb5-234">Abra uma janela de navegador em um tootrigger de modo "InPrivate" ou "Incognito" uma nova autenticação.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-234">Open a browser window in an "InPrivate" or "Incognito" mode tootrigger a new authentication.</span></span>  <span data-ttu-id="a4cb5-235">No Internet Explorer, use Ctrl + Shift + P.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="a4cb5-236">No Chrome, use Ctrl + Shift + N.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="a4cb5-237">Na janela de navegação particular hello, procurar tooa recurso protegido e executar um logon do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-237">In hello private browsing window, browse tooa protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="a4cb5-238">Após o logon bem-sucedido, será o site solicitado toohello feito em uma sessão de isolamento.</span><span class="sxs-lookup"><span data-stu-id="a4cb5-238">Upon successful login, you will be taken toohello requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a4cb5-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a4cb5-239">Additional resources</span></span>

* [<span data-ttu-id="a4cb5-240">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a4cb5-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a4cb5-241">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a4cb5-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

