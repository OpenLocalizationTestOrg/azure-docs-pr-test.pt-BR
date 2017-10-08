---
title: "Tutorial: integração do Azure Active Directory ao PurelyHR | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e PurelyHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: bdc1748ed650cff36b1ef7d7330dd2a17b3bc760
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="8f925-103">Tutorial: integração do Azure Active Directory com o PurelyHR</span><span class="sxs-lookup"><span data-stu-id="8f925-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="8f925-104">Neste tutorial, você aprenderá como toointegrate PurelyHR com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="8f925-104">In this tutorial, you learn how toointegrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f925-105">Integrando PurelyHR com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f925-105">Integrating PurelyHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8f925-106">Você pode controlar no AD do Azure que tenha acesso tooPurelyHR</span><span class="sxs-lookup"><span data-stu-id="8f925-106">You can control in Azure AD who has access tooPurelyHR</span></span>
- <span data-ttu-id="8f925-107">Você pode habilitar seu usuários tooautomatically get conectado tooPurelyHR (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8f925-107">You can enable your users tooautomatically get signed-on tooPurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8f925-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8f925-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8f925-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f925-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f925-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8f925-110">Prerequisites</span></span>

<span data-ttu-id="8f925-111">tooconfigure integração do AD do Azure com PurelyHR, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f925-111">tooconfigure Azure AD integration with PurelyHR, you need hello following items:</span></span>

- <span data-ttu-id="8f925-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8f925-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f925-113">Uma assinatura do PurelyHR com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="8f925-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f925-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8f925-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f925-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8f925-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f925-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8f925-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f925-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f925-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f925-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8f925-118">Scenario description</span></span>
<span data-ttu-id="8f925-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8f925-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f925-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="8f925-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f925-121">Adicionando PurelyHR da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8f925-121">Adding PurelyHR from hello gallery</span></span>
2. <span data-ttu-id="8f925-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8f925-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-hello-gallery"></a><span data-ttu-id="8f925-123">Adicionando PurelyHR da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8f925-123">Adding PurelyHR from hello gallery</span></span>
<span data-ttu-id="8f925-124">integração de saudação tooconfigure de PurelyHR no AD do Azure, você precisa tooadd PurelyHR da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8f925-124">tooconfigure hello integration of PurelyHR into Azure AD, you need tooadd PurelyHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8f925-125">**tooadd PurelyHR da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8f925-125">**tooadd PurelyHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f925-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8f925-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8f925-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8f925-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8f925-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8f925-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8f925-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8f925-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8f925-133">Na caixa de pesquisa hello, digite **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="8f925-133">In hello search box, type **PurelyHR**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="8f925-135">No painel de resultados de saudação, selecione **PurelyHR**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8f925-135">In hello results panel, select **PurelyHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8f925-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8f925-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8f925-138">Nesta seção, você configurará e testará o logon único do Azure AD com o PurelyHR, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="8f925-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8f925-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em PurelyHR é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f925-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PurelyHR is tooa user in Azure AD.</span></span> <span data-ttu-id="8f925-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em PurelyHR precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="8f925-140">In other words, a link relationship between an Azure AD user and hello related user in PurelyHR needs toobe established.</span></span>

<span data-ttu-id="8f925-141">PurelyHR, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f925-141">In PurelyHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8f925-142">tooconfigure e teste de logon único do AD do Azure com PurelyHR, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f925-142">tooconfigure and test Azure AD single sign-on with PurelyHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8f925-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8f925-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8f925-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8f925-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f925-145">**[Criar um usuário de teste PurelyHR](#creating-a-purelyhr-test-user)**  -toohave um equivalente do Britta Simon em PurelyHR é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="8f925-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - toohave a counterpart of Britta Simon in PurelyHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8f925-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="8f925-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f925-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="8f925-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8f925-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f925-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8f925-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="8f925-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="8f925-150">**tooconfigure AD do Azure-logon único com PurelyHR, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8f925-150">**tooconfigure Azure AD single sign-on with PurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f925-151">Em Olá portal do Azure, Olá **PurelyHR** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="8f925-151">In hello Azure portal, on hello **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8f925-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="8f925-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="8f925-155">Em Olá **PurelyHR domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="8f925-155">On hello **PurelyHR Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="8f925-157">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="8f925-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="8f925-158">Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="8f925-158">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="8f925-160">Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="8f925-160">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="8f925-161">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="8f925-161">These values are not hello real.</span></span> <span data-ttu-id="8f925-162">Atualize esses valores com URL de resposta real hello e a URL de logon.</span><span class="sxs-lookup"><span data-stu-id="8f925-162">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="8f925-163">Entre em contato com [equipe de suporte do cliente PurelyHR](http://support.purelyhr.com/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="8f925-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) tooget these values.</span></span> 

5. <span data-ttu-id="8f925-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8f925-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="8f925-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8f925-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="8f925-168">Em Olá **PurelyHR configuração** seção, clique em **configurar PurelyHR** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="8f925-168">On hello **PurelyHR Configuration** section, click **Configure PurelyHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8f925-169">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="8f925-169">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="8f925-171">tooconfigure logon único no **PurelyHR** lado, o site de tootheir logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="8f925-171">tooconfigure single sign-on on **PurelyHR** side, login tootheir website as an administrator.</span></span>

9. <span data-ttu-id="8f925-172">Olá abrir **painel** de opções de saudação na barra de ferramentas hello e clique em **configurações de SSO**.</span><span class="sxs-lookup"><span data-stu-id="8f925-172">Open hello **Dashboard** from hello options in hello toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="8f925-173">Colar Olá valores nas caixas de saudação conforme descrito abaixo-</span><span class="sxs-lookup"><span data-stu-id="8f925-173">Paste hello values in hello boxes as described below-</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="8f925-175">a.</span><span class="sxs-lookup"><span data-stu-id="8f925-175">a.</span></span> <span data-ttu-id="8f925-176">Olá abrir **Certificate(Bas64)** baixados da saudação portal do Azure no bloco de notas e copie valor de certificado hello.</span><span class="sxs-lookup"><span data-stu-id="8f925-176">Open hello **Certificate(Bas64)** downloaded from hello Azure portal in notepad and copy hello certificate value.</span></span> <span data-ttu-id="8f925-177">Olá colar copiado o valor para Olá **certificado x. 509** caixa.</span><span class="sxs-lookup"><span data-stu-id="8f925-177">Paste hello copied value into hello **X.509 Certificate** box.</span></span>

    <span data-ttu-id="8f925-178">b.</span><span class="sxs-lookup"><span data-stu-id="8f925-178">b.</span></span> <span data-ttu-id="8f925-179">Em Olá **URL do emissor Idp** caixa, cole Olá **ID da entidade SAML** copiados da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f925-179">In hello **Idp Issuer URL** box, paste hello **SAML Entity ID** copied from hello Azure portal.</span></span>

    <span data-ttu-id="8f925-180">c.</span><span class="sxs-lookup"><span data-stu-id="8f925-180">c.</span></span> <span data-ttu-id="8f925-181">Em Olá **URL de ponto de extremidade Idp** caixa, cole Olá **Single Sign-On URL do serviço SAML** copiados da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f925-181">In hello **Idp Endpoint URL** box, paste hello **SAML Single Sign-On Service URL** copied from hello Azure portal.</span></span> 

    <span data-ttu-id="8f925-182">d.</span><span class="sxs-lookup"><span data-stu-id="8f925-182">d.</span></span> <span data-ttu-id="8f925-183">Verificar Olá **criação automática de usuários** provisionamento de usuário automático do caixa de seleção tooenable em PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="8f925-183">Check hello **Auto-Create Users** checkbox tooenable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="8f925-184">e.</span><span class="sxs-lookup"><span data-stu-id="8f925-184">e.</span></span> <span data-ttu-id="8f925-185">Clique em **salvar alterações** toosave configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f925-185">Click **Save Changes** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="8f925-186">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="8f925-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8f925-187">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="8f925-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8f925-188">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8f925-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8f925-189">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8f925-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="8f925-190">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f925-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8f925-192">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8f925-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f925-193">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8f925-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8f925-195">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="8f925-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8f925-197">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f925-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8f925-199">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f925-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8f925-201">a.</span><span class="sxs-lookup"><span data-stu-id="8f925-201">a.</span></span> <span data-ttu-id="8f925-202">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8f925-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f925-203">b.</span><span class="sxs-lookup"><span data-stu-id="8f925-203">b.</span></span> <span data-ttu-id="8f925-204">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8f925-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8f925-205">c.</span><span class="sxs-lookup"><span data-stu-id="8f925-205">c.</span></span> <span data-ttu-id="8f925-206">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="8f925-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8f925-207">d.</span><span class="sxs-lookup"><span data-stu-id="8f925-207">d.</span></span> <span data-ttu-id="8f925-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8f925-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="8f925-209">Criar um usuário de teste do PurelyHR</span><span class="sxs-lookup"><span data-stu-id="8f925-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="8f925-210">tooenable AD do Azure usuários toolog em tooPurelyHR, eles devem ser provisionados no PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="8f925-210">tooenable Azure AD users toolog in tooPurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="8f925-211">No PurelyHR, o provisionamento é uma tarefa automática e nenhuma etapa manual é necessária quando o provisionamento de usuários automático está habilitado.</span><span class="sxs-lookup"><span data-stu-id="8f925-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8f925-212">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8f925-212">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8f925-213">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPurelyHR.</span><span class="sxs-lookup"><span data-stu-id="8f925-213">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPurelyHR.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8f925-215">**tooassign Britta Simon tooPurelyHR, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8f925-215">**tooassign Britta Simon tooPurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f925-216">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8f925-216">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8f925-218">Na lista de aplicativos hello, selecione **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="8f925-218">In hello applications list, select **PurelyHR**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="8f925-220">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8f925-220">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8f925-222">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8f925-222">Click **Add** button.</span></span> <span data-ttu-id="8f925-223">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8f925-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8f925-225">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f925-225">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8f925-226">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8f925-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8f925-227">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8f925-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8f925-228">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8f925-228">Testing single sign-on</span></span>

<span data-ttu-id="8f925-229">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f925-229">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8f925-230">Clique em Olá absorver LMS lado a lado no hello painel de acesso, obter o aplicativo de absorver LMS automaticamente assinado em tooyour.</span><span class="sxs-lookup"><span data-stu-id="8f925-230">Click hello Absorb LMS tile in hello Access Panel, you get automatically signed-on tooyour Absorb LMS application.</span></span>

<span data-ttu-id="8f925-231">Para obter mais informações sobre Olá painel de acesso, consulte.</span><span class="sxs-lookup"><span data-stu-id="8f925-231">For more information about hello Access Panel, see.</span></span> <span data-ttu-id="8f925-232">[Introdução toohello painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="8f925-232">[Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f925-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8f925-233">Additional resources</span></span>

* [<span data-ttu-id="8f925-234">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8f925-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f925-235">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8f925-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

