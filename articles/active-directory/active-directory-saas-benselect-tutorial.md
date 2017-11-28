---
title: "Tutorial: Integração do Azure Active Directory com o BenSelect | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e BenSelect."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c3705da337bf8f6e76de58cd21c5b047c8f5e12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="72e5f-103">Tutorial: Integração do Azure Active Directory ao BenSelect</span><span class="sxs-lookup"><span data-stu-id="72e5f-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="72e5f-104">Neste tutorial, você aprenderá como toointegrate BenSelect com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="72e5f-104">In this tutorial, you learn how toointegrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72e5f-105">Integrando BenSelect com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="72e5f-105">Integrating BenSelect with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="72e5f-106">Você pode controlar no AD do Azure que tenha acesso tooBenSelect</span><span class="sxs-lookup"><span data-stu-id="72e5f-106">You can control in Azure AD who has access tooBenSelect</span></span>
- <span data-ttu-id="72e5f-107">Você pode habilitar seu usuários tooautomatically get conectado tooBenSelect (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72e5f-107">You can enable your users tooautomatically get signed-on tooBenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="72e5f-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="72e5f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="72e5f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="72e5f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72e5f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="72e5f-110">Prerequisites</span></span>

<span data-ttu-id="72e5f-111">tooconfigure integração do AD do Azure com BenSelect, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="72e5f-111">tooconfigure Azure AD integration with BenSelect, you need hello following items:</span></span>

- <span data-ttu-id="72e5f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72e5f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="72e5f-113">Uma assinatura habilitada para logon único do BenSelect</span><span class="sxs-lookup"><span data-stu-id="72e5f-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72e5f-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="72e5f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="72e5f-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="72e5f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="72e5f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="72e5f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72e5f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72e5f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72e5f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="72e5f-118">Scenario description</span></span>
<span data-ttu-id="72e5f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="72e5f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="72e5f-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="72e5f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="72e5f-121">Adicionando BenSelect da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="72e5f-121">Adding BenSelect from hello gallery</span></span>
2. <span data-ttu-id="72e5f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72e5f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-hello-gallery"></a><span data-ttu-id="72e5f-123">Adicionando BenSelect da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="72e5f-123">Adding BenSelect from hello gallery</span></span>
<span data-ttu-id="72e5f-124">integração de saudação tooconfigure de BenSelect no AD do Azure, você precisa tooadd BenSelect da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="72e5f-124">tooconfigure hello integration of BenSelect into Azure AD, you need tooadd BenSelect from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="72e5f-125">**tooadd BenSelect da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72e5f-125">**tooadd BenSelect from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="72e5f-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="72e5f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="72e5f-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="72e5f-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="72e5f-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72e5f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="72e5f-133">Na caixa de pesquisa hello, digite **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-133">In hello search box, type **BenSelect**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="72e5f-135">No painel de resultados de saudação, selecione **BenSelect**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="72e5f-135">In hello results panel, select **BenSelect**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="72e5f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72e5f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="72e5f-138">Nesta seção, você configura e testa o logon único do Azure AD com o BenSelect, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="72e5f-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="72e5f-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em BenSelect é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="72e5f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenSelect is tooa user in Azure AD.</span></span> <span data-ttu-id="72e5f-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em BenSelect precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="72e5f-140">In other words, a link relationship between an Azure AD user and hello related user in BenSelect needs toobe established.</span></span>

<span data-ttu-id="72e5f-141">BenSelect, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="72e5f-141">In BenSelect, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="72e5f-142">tooconfigure e teste de logon único do AD do Azure com BenSelect, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="72e5f-142">tooconfigure and test Azure AD single sign-on with BenSelect, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="72e5f-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="72e5f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="72e5f-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="72e5f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="72e5f-145">**[Criar um usuário de teste BenSelect](#creating-a-benselect-test-user)**  -toohave um equivalente do Britta Simon em BenSelect é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="72e5f-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - toohave a counterpart of Britta Simon in BenSelect that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="72e5f-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="72e5f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="72e5f-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="72e5f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="72e5f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="72e5f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="72e5f-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo BenSelect.</span><span class="sxs-lookup"><span data-stu-id="72e5f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="72e5f-150">**tooconfigure AD do Azure-logon único com BenSelect, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72e5f-150">**tooconfigure Azure AD single sign-on with BenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="72e5f-151">Em Olá portal do Azure, Olá **BenSelect** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-151">In hello Azure portal, on hello **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="72e5f-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="72e5f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="72e5f-155">Em Olá **BenSelect domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="72e5f-155">On hello **BenSelect Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="72e5f-157">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="72e5f-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="72e5f-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="72e5f-158">This value is not real.</span></span> <span data-ttu-id="72e5f-159">Atualize esse valor com hello URL de resposta real.</span><span class="sxs-lookup"><span data-stu-id="72e5f-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="72e5f-160">Entre em contato com [BenSelect a equipe de suporte](mailto:support@selerix.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="72e5f-160">Contact [BenSelect support team](mailto:support@selerix.com) tooget this value.</span></span>
 
4. <span data-ttu-id="72e5f-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Raw)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="72e5f-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="72e5f-163">Aplicativo de BenSelect espera asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="72e5f-163">BenSelect application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="72e5f-164">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="72e5f-164">Configure hello following claims for this application.</span></span> <span data-ttu-id="72e5f-165">Você pode gerenciar os valores hello desses atributos de saudação **atributos de usuário** seção na página de integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="72e5f-165">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="72e5f-166">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="72e5f-166">hello following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="72e5f-168">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="72e5f-168">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="72e5f-169">a.</span><span class="sxs-lookup"><span data-stu-id="72e5f-169">a.</span></span> <span data-ttu-id="72e5f-170">Em Olá **identificador de usuário** lista suspensa, selecione **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-170">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="72e5f-171">b.</span><span class="sxs-lookup"><span data-stu-id="72e5f-171">b.</span></span> <span data-ttu-id="72e5f-172">Em Olá **Mail** lista suspensa, selecione **User**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-172">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="72e5f-173">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="72e5f-173">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="72e5f-175">Em Olá **BenSelect configuração** seção, clique em **configurar BenSelect** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="72e5f-175">On hello **BenSelect Configuration** section, click **Configure BenSelect** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="72e5f-176">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="72e5f-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="72e5f-178">tooconfigure logon único no **BenSelect** lado, você precisa toosend Olá baixado **Certificate(Raw)** e **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML**muito[a equipe de suporte BenSelect](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="72e5f-178">tooconfigure single sign-on on **BenSelect** side, you need toosend hello downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="72e5f-179">Você precisa toomention esta integração exige algoritmo Olá SHA256 (não há suporte para SHA1) tooset Olá SSO no servidor apropriado do hello como app2101 etc.</span><span class="sxs-lookup"><span data-stu-id="72e5f-179">You need toomention that this integration requires hello SHA256 algorithm (SHA1 is not supported) tooset hello SSO on hello appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="72e5f-180">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="72e5f-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="72e5f-181">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="72e5f-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="72e5f-182">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="72e5f-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="72e5f-183">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72e5f-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="72e5f-184">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="72e5f-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="72e5f-186">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72e5f-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="72e5f-187">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="72e5f-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="72e5f-189">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="72e5f-191">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="72e5f-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="72e5f-193">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="72e5f-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="72e5f-195">a.</span><span class="sxs-lookup"><span data-stu-id="72e5f-195">a.</span></span> <span data-ttu-id="72e5f-196">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72e5f-197">b.</span><span class="sxs-lookup"><span data-stu-id="72e5f-197">b.</span></span> <span data-ttu-id="72e5f-198">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="72e5f-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="72e5f-199">c.</span><span class="sxs-lookup"><span data-stu-id="72e5f-199">c.</span></span> <span data-ttu-id="72e5f-200">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="72e5f-201">d.</span><span class="sxs-lookup"><span data-stu-id="72e5f-201">d.</span></span> <span data-ttu-id="72e5f-202">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="72e5f-203">Criando um usuário de teste do BenSelect</span><span class="sxs-lookup"><span data-stu-id="72e5f-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="72e5f-204">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no BenSelect.</span><span class="sxs-lookup"><span data-stu-id="72e5f-204">hello objective of this section is toocreate a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="72e5f-205">Trabalhar com [BenSelect a equipe de suporte](mailto:support@selerix.com) tooadd usuários Olá Olá BenSelect conta.</span><span class="sxs-lookup"><span data-stu-id="72e5f-205">Work with [BenSelect support team](mailto:support@selerix.com) tooadd hello users in hello BenSelect account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="72e5f-206">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72e5f-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="72e5f-207">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBenSelect.</span><span class="sxs-lookup"><span data-stu-id="72e5f-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenSelect.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="72e5f-209">**tooassign Britta Simon tooBenSelect, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72e5f-209">**tooassign Britta Simon tooBenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="72e5f-210">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="72e5f-212">Na lista de aplicativos hello, selecione **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-212">In hello applications list, select **BenSelect**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="72e5f-214">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="72e5f-216">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="72e5f-216">Click **Add** button.</span></span> <span data-ttu-id="72e5f-217">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72e5f-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="72e5f-219">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="72e5f-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="72e5f-220">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72e5f-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="72e5f-221">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72e5f-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="72e5f-222">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="72e5f-222">Testing single sign-on</span></span>

<span data-ttu-id="72e5f-223">Nesta seção, você deve testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="72e5f-223">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="72e5f-224">Quando você clica em bloco BenSelect Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour BenSelect aplicativo.</span><span class="sxs-lookup"><span data-stu-id="72e5f-224">When you click hello BenSelect tile in hello Access Panel, you should get automatically signed-on tooyour BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="72e5f-225">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="72e5f-225">Additional resources</span></span>

* [<span data-ttu-id="72e5f-226">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="72e5f-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="72e5f-227">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="72e5f-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

