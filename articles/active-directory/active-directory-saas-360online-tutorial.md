---
title: "Tutorial: integração do Azure Active Directory com o 360 Online | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e 360 Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cda8eba6-843f-4a09-8c55-0aaf6e593d75
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 413e4e2c41336f99e1999857c788c5dac15be4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-360-online"></a><span data-ttu-id="80bc3-103">Tutorial: Integração do Azure Active Directory com o 360 Online</span><span class="sxs-lookup"><span data-stu-id="80bc3-103">Tutorial: Azure Active Directory integration with 360 Online</span></span>

<span data-ttu-id="80bc3-104">Neste tutorial, você aprenderá como toointegrate 360 Online com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="80bc3-104">In this tutorial, you learn how toointegrate 360 Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="80bc3-105">Integrando 360 Online com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="80bc3-105">Integrating 360 Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="80bc3-106">Você pode controlar no AD do Azure que tenha acesso too360 Online</span><span class="sxs-lookup"><span data-stu-id="80bc3-106">You can control in Azure AD who has access too360 Online</span></span>
- <span data-ttu-id="80bc3-107">Você pode habilitar seus usuários tooautomatically get conectado too360 on-line (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80bc3-107">You can enable your users tooautomatically get signed-on too360 Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="80bc3-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="80bc3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="80bc3-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80bc3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80bc3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="80bc3-110">Prerequisites</span></span>

<span data-ttu-id="80bc3-111">tooconfigure integração do AD do Azure com 360 Online, você precisará Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="80bc3-111">tooconfigure Azure AD integration with 360 Online, you need hello following items:</span></span>

- <span data-ttu-id="80bc3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80bc3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="80bc3-113">Uma assinatura habilitada para logon único do 360 Online</span><span class="sxs-lookup"><span data-stu-id="80bc3-113">A 360 Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="80bc3-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="80bc3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="80bc3-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="80bc3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="80bc3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="80bc3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="80bc3-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="80bc3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="80bc3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="80bc3-118">Scenario description</span></span>
<span data-ttu-id="80bc3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="80bc3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="80bc3-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="80bc3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="80bc3-121">Adicionando 360 Online da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="80bc3-121">Adding 360 Online from hello gallery</span></span>
2. <span data-ttu-id="80bc3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80bc3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-360-online-from-hello-gallery"></a><span data-ttu-id="80bc3-123">Adicionando 360 Online da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="80bc3-123">Adding 360 Online from hello gallery</span></span>
<span data-ttu-id="80bc3-124">integração de saudação tooconfigure de 360 Online no AD do Azure, você precisa tooadd 360 Online na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="80bc3-124">tooconfigure hello integration of 360 Online into Azure AD, you need tooadd 360 Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="80bc3-125">**tooadd 360 Online da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="80bc3-125">**tooadd 360 Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="80bc3-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="80bc3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="80bc3-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="80bc3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="80bc3-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="80bc3-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="80bc3-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80bc3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="80bc3-133">Na caixa de pesquisa hello, digite **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="80bc3-133">In hello search box, type **360 Online**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-360online-tutorial/tutorial_360online_search.png)

5. <span data-ttu-id="80bc3-135">No painel de resultados de saudação, selecione **360 Online**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="80bc3-135">In hello results panel, select **360 Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-360online-tutorial/tutorial_360online_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="80bc3-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80bc3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="80bc3-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o 360 Online, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="80bc3-138">In this section, you configure and test Azure AD single sign-on with 360 Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="80bc3-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em 360 Online é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="80bc3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 360 Online is tooa user in Azure AD.</span></span> <span data-ttu-id="80bc3-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em 360 Online precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="80bc3-140">In other words, a link relationship between an Azure AD user and hello related user in 360 Online needs toobe established.</span></span>

<span data-ttu-id="80bc3-141">360 Online, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="80bc3-141">In 360 Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="80bc3-142">tooconfigure e teste de logon único do AD do Azure com 360 Online, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="80bc3-142">tooconfigure and test Azure AD single sign-on with 360 Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="80bc3-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="80bc3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="80bc3-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80bc3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="80bc3-145">**[Criar um usuário de teste Online 360](#creating-a-360-online-test-user)**  -toohave um equivalente do Britta Simon em 360 Online que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="80bc3-145">**[Creating a 360 Online test user](#creating-a-360-online-test-user)** - toohave a counterpart of Britta Simon in 360 Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="80bc3-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="80bc3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="80bc3-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="80bc3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="80bc3-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="80bc3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="80bc3-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Online 360.</span><span class="sxs-lookup"><span data-stu-id="80bc3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 360 Online application.</span></span>

<span data-ttu-id="80bc3-150">**tooconfigure AD do Azure-logon único com 360 Online, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="80bc3-150">**tooconfigure Azure AD single sign-on with 360 Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="80bc3-151">Em Olá portal do Azure, Olá **360 Online** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="80bc3-151">In hello Azure portal, on hello **360 Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="80bc3-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="80bc3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-360online-tutorial/tutorial_360online_samlbase.png)

3. <span data-ttu-id="80bc3-155">Em Olá **360 domínio on-line e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="80bc3-155">On hello **360 Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-360online-tutorial/tutorial_360online_url.png)

    <span data-ttu-id="80bc3-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.public360online.com`</span><span class="sxs-lookup"><span data-stu-id="80bc3-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.public360online.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="80bc3-158">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="80bc3-158">hello value is not real.</span></span> <span data-ttu-id="80bc3-159">Valor de saudação de atualização com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="80bc3-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="80bc3-160">Entre em contato com [360 equipe de suporte do cliente Online](mailto:360online@software-innovation.com) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="80bc3-160">Contact [360 Online Client support team](mailto:360online@software-innovation.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="80bc3-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="80bc3-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-360online-tutorial/tutorial_360online_certificate.png) 

5. <span data-ttu-id="80bc3-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="80bc3-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-360online-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="80bc3-165">tooconfigure logon único no **360 Online** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte de 360 Online](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="80bc3-165">tooconfigure single sign-on on **360 Online** side, you need toosend hello downloaded **Metadata XML** too[360 Online support team](mailto:360online@software-innovation.com).</span></span> 

> [!TIP]
> <span data-ttu-id="80bc3-166">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="80bc3-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="80bc3-167">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="80bc3-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="80bc3-168">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="80bc3-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="80bc3-169">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80bc3-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="80bc3-170">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="80bc3-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="80bc3-172">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="80bc3-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="80bc3-173">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="80bc3-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-360online-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="80bc3-175">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="80bc3-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-360online-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="80bc3-177">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="80bc3-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-360online-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="80bc3-179">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="80bc3-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-360online-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="80bc3-181">a.</span><span class="sxs-lookup"><span data-stu-id="80bc3-181">a.</span></span> <span data-ttu-id="80bc3-182">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="80bc3-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="80bc3-183">b.</span><span class="sxs-lookup"><span data-stu-id="80bc3-183">b.</span></span> <span data-ttu-id="80bc3-184">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="80bc3-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="80bc3-185">c.</span><span class="sxs-lookup"><span data-stu-id="80bc3-185">c.</span></span> <span data-ttu-id="80bc3-186">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="80bc3-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="80bc3-187">d.</span><span class="sxs-lookup"><span data-stu-id="80bc3-187">d.</span></span> <span data-ttu-id="80bc3-188">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="80bc3-188">Click **Create**.</span></span>
 
### <a name="creating-a-360-online-test-user"></a><span data-ttu-id="80bc3-189">Criar um usuário de teste do 360 Online</span><span class="sxs-lookup"><span data-stu-id="80bc3-189">Creating a 360 Online test user</span></span>

<span data-ttu-id="80bc3-190">Nesta seção, você criará uma usuária chamada Brenda Fernandes no 360 Online.</span><span class="sxs-lookup"><span data-stu-id="80bc3-190">In this section, you create a user called Britta Simon in 360 Online.</span></span> <span data-ttu-id="80bc3-191">Você precisa toocontact [equipe de suporte de 360 Online](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="80bc3-191">you need toocontact [360 Online support team](mailto:360online@software-innovation.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="80bc3-192">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80bc3-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="80bc3-193">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso too360 on-line.</span><span class="sxs-lookup"><span data-stu-id="80bc3-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too360 Online.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="80bc3-195">**tooassign Britta Simon too360 Online, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="80bc3-195">**tooassign Britta Simon too360 Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="80bc3-196">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="80bc3-196">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="80bc3-198">Na lista de aplicativos hello, selecione **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="80bc3-198">In hello applications list, select **360 Online**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-360online-tutorial/tutorial_360online_app.png) 

3. <span data-ttu-id="80bc3-200">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="80bc3-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="80bc3-202">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="80bc3-202">Click **Add** button.</span></span> <span data-ttu-id="80bc3-203">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80bc3-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="80bc3-205">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="80bc3-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="80bc3-206">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80bc3-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="80bc3-207">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80bc3-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="80bc3-208">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="80bc3-208">Testing single sign-on</span></span>

<span data-ttu-id="80bc3-209">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="80bc3-209">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="80bc3-210">Quando você clica em Olá 360 Online bloco no painel de acesso de saudação, você deve obter um aplicativo Online automaticamente assinado em tooyour 360.</span><span class="sxs-lookup"><span data-stu-id="80bc3-210">When you click hello 360 Online tile in hello Access Panel, you should get automatically signed-on tooyour 360 Online application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="80bc3-211">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="80bc3-211">Additional resources</span></span>

* [<span data-ttu-id="80bc3-212">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="80bc3-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80bc3-213">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="80bc3-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-360online-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-360online-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-360online-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-360online-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-360online-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-360online-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-360online-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-360online-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-360online-tutorial/tutorial_general_203.png

