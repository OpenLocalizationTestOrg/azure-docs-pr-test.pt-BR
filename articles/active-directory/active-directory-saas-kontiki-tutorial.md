---
title: "Tutorial: Integração do Azure Active Directory com o Kontiki | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Kontiki."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8d5e5413-da4c-40d8-b1d0-f03ecfef030b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: bfbc3c4f23494f7e3cf9498817fb8948bb300470
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kontiki"></a><span data-ttu-id="d3162-103">Tutorial: Integração do Active Directory do Azure com o Kontiki</span><span class="sxs-lookup"><span data-stu-id="d3162-103">Tutorial: Azure Active Directory integration with Kontiki</span></span>

<span data-ttu-id="d3162-104">Neste tutorial, você aprenderá como toointegrate Kontiki com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="d3162-104">In this tutorial, you learn how toointegrate Kontiki with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3162-105">Integrando Kontiki com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3162-105">Integrating Kontiki with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d3162-106">Você pode controlar no AD do Azure que tenha acesso tooKontiki</span><span class="sxs-lookup"><span data-stu-id="d3162-106">You can control in Azure AD who has access tooKontiki</span></span>
- <span data-ttu-id="d3162-107">Você pode habilitar seu usuários tooautomatically get conectado tooKontiki (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d3162-107">You can enable your users tooautomatically get signed-on tooKontiki (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d3162-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d3162-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d3162-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d3162-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3162-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d3162-110">Prerequisites</span></span>

<span data-ttu-id="d3162-111">tooconfigure integração do AD do Azure com Kontiki, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3162-111">tooconfigure Azure AD integration with Kontiki, you need hello following items:</span></span>

- <span data-ttu-id="d3162-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d3162-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3162-113">Uma assinatura do Kontiki com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="d3162-113">A Kontiki single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3162-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d3162-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3162-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d3162-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3162-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d3162-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3162-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3162-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3162-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d3162-118">Scenario description</span></span>
<span data-ttu-id="d3162-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d3162-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3162-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="d3162-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3162-121">Adicionando Kontiki da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d3162-121">Adding Kontiki from hello gallery</span></span>
2. <span data-ttu-id="d3162-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d3162-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kontiki-from-hello-gallery"></a><span data-ttu-id="d3162-123">Adicionando Kontiki da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d3162-123">Adding Kontiki from hello gallery</span></span>
<span data-ttu-id="d3162-124">integração de saudação tooconfigure do Kontiki no AD do Azure, você precisa tooadd Kontiki da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d3162-124">tooconfigure hello integration of Kontiki into Azure AD, you need tooadd Kontiki from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d3162-125">**tooadd Kontiki da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d3162-125">**tooadd Kontiki from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3162-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d3162-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d3162-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d3162-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d3162-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d3162-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="d3162-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d3162-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="d3162-133">Na caixa de pesquisa hello, digite **Kontiki**.</span><span class="sxs-lookup"><span data-stu-id="d3162-133">In hello search box, type **Kontiki**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_search.png)

5. <span data-ttu-id="d3162-135">No painel de resultados de saudação, selecione **Kontiki**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d3162-135">In hello results panel, select **Kontiki**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d3162-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d3162-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d3162-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Kontiki, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="d3162-138">In this section, you configure and test Azure AD single sign-on with Kontiki based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d3162-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Kontiki é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d3162-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kontiki is tooa user in Azure AD.</span></span> <span data-ttu-id="d3162-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Kontiki precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="d3162-140">In other words, a link relationship between an Azure AD user and hello related user in Kontiki needs toobe established.</span></span>

<span data-ttu-id="d3162-141">No Kontiki, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3162-141">In Kontiki, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d3162-142">tooconfigure e teste de logon único do AD do Azure com Kontiki, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3162-142">tooconfigure and test Azure AD single sign-on with Kontiki, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d3162-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d3162-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d3162-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3162-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3162-145">**[Criar um usuário de teste do Kontiki](#creating-a-kontiki-test-user)**  -toohave um equivalente do Britta Simon no Kontiki é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="d3162-145">**[Creating a Kontiki test user](#creating-a-kontiki-test-user)** - toohave a counterpart of Britta Simon in Kontiki that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d3162-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="d3162-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3162-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="d3162-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d3162-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3162-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d3162-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Kontiki.</span><span class="sxs-lookup"><span data-stu-id="d3162-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kontiki application.</span></span>

<span data-ttu-id="d3162-150">**tooconfigure AD do Azure-logon único com Kontiki, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d3162-150">**tooconfigure Azure AD single sign-on with Kontiki, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3162-151">Em Olá portal do Azure, Olá **Kontiki** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="d3162-151">In hello Azure portal, on hello **Kontiki** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d3162-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="d3162-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_samlbase.png)

3. <span data-ttu-id="d3162-155">Em Olá **Kontiki domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3162-155">On hello **Kontiki Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_url.png)

     <span data-ttu-id="d3162-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.mc.eval.kontiki.com`</span><span class="sxs-lookup"><span data-stu-id="d3162-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mc.eval.kontiki.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d3162-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="d3162-158">This value is not real.</span></span> <span data-ttu-id="d3162-159">Valor de saudação de atualização com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="d3162-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="d3162-160">Entre em contato com [a equipe de suporte Kontiki cliente](http://customersupport.kontiki.com/enterprise/contactsupport.html) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3162-160">Contact [Kontiki Client support team](http://customersupport.kontiki.com/enterprise/contactsupport.html) tooget hello value.</span></span> 
 
4. <span data-ttu-id="d3162-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d3162-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_certificate.png) 

5. <span data-ttu-id="d3162-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d3162-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kontiki-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="d3162-165">tooconfigure logon único no **Kontiki** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte Kontiki](http://customersupport.kontiki.com/enterprise/contactsupport.html).</span><span class="sxs-lookup"><span data-stu-id="d3162-165">tooconfigure single sign-on on **Kontiki** side, you need toosend hello downloaded **Metadata XML** too[Kontiki support team](http://customersupport.kontiki.com/enterprise/contactsupport.html).</span></span> <span data-ttu-id="d3162-166">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="d3162-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d3162-167">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="d3162-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d3162-168">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="d3162-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d3162-169">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d3162-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d3162-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d3162-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="d3162-171">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d3162-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d3162-173">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d3162-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3162-174">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d3162-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kontiki-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d3162-176">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="d3162-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kontiki-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d3162-178">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3162-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kontiki-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d3162-180">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d3162-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kontiki-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d3162-182">a.</span><span class="sxs-lookup"><span data-stu-id="d3162-182">a.</span></span> <span data-ttu-id="d3162-183">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3162-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3162-184">b.</span><span class="sxs-lookup"><span data-stu-id="d3162-184">b.</span></span> <span data-ttu-id="d3162-185">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d3162-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d3162-186">c.</span><span class="sxs-lookup"><span data-stu-id="d3162-186">c.</span></span> <span data-ttu-id="d3162-187">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="d3162-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d3162-188">d.</span><span class="sxs-lookup"><span data-stu-id="d3162-188">d.</span></span> <span data-ttu-id="d3162-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d3162-189">Click **Create**.</span></span>
 
### <a name="creating-a-kontiki-test-user"></a><span data-ttu-id="d3162-190">Criar um usuário de teste do Kontiki</span><span class="sxs-lookup"><span data-stu-id="d3162-190">Creating a Kontiki test user</span></span>

<span data-ttu-id="d3162-191">Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooKontiki.</span><span class="sxs-lookup"><span data-stu-id="d3162-191">There is no action item for you tooconfigure user provisioning tooKontiki.</span></span> <span data-ttu-id="d3162-192">Quando um usuário atribuído tenta toolog em tooKontiki usando o painel de acesso hello, Kontiki verifica se o usuário Olá existe.</span><span class="sxs-lookup"><span data-stu-id="d3162-192">When an assigned user tries toolog in tooKontiki using hello access panel, Kontiki checks whether hello user exists.</span></span>  

>[!NOTE]
><span data-ttu-id="d3162-193">Se não houver conta de usuário ainda, ela é criada automaticamente pelo Kontiki.</span><span class="sxs-lookup"><span data-stu-id="d3162-193">If there is no user account available yet, it is automatically created by Kontiki.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d3162-194">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d3162-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d3162-195">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooKontiki.</span><span class="sxs-lookup"><span data-stu-id="d3162-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKontiki.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="d3162-197">**tooassign Britta Simon tooKontiki, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d3162-197">**tooassign Britta Simon tooKontiki, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3162-198">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d3162-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d3162-200">Na lista de aplicativos hello, selecione **Kontiki**.</span><span class="sxs-lookup"><span data-stu-id="d3162-200">In hello applications list, select **Kontiki**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_app.png) 

3. <span data-ttu-id="d3162-202">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d3162-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="d3162-204">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d3162-204">Click **Add** button.</span></span> <span data-ttu-id="d3162-205">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d3162-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="d3162-207">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3162-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d3162-208">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d3162-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d3162-209">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d3162-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d3162-210">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d3162-210">Testing single sign-on</span></span>

<span data-ttu-id="d3162-211">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="d3162-211">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d3162-212">Quando você clica em bloco Kontiki Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Kontiki aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d3162-212">When you click hello Kontiki tile in hello Access Panel, you should get automatically signed-on tooyour Kontiki application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d3162-213">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d3162-213">Additional resources</span></span>

* [<span data-ttu-id="d3162-214">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d3162-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3162-215">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d3162-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_203.png

