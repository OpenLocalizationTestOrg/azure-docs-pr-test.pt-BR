---
title: "Tutorial: integração do Azure Active Directory com Sciforma | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Sciforma."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: abbfb5ac-7687-4153-b263-8090102dae37
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: jeedes
ms.openlocfilehash: fca6237196061355e38d431e958964a45246f965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciforma"></a><span data-ttu-id="a1feb-103">Tutorial: integração do Azure Active Directory com o Sciforma</span><span class="sxs-lookup"><span data-stu-id="a1feb-103">Tutorial: Azure Active Directory integration with Sciforma</span></span>

<span data-ttu-id="a1feb-104">Neste tutorial, você aprenderá como toointegrate Sciforma com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="a1feb-104">In this tutorial, you learn how toointegrate Sciforma with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1feb-105">Integrando o Sciforma com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1feb-105">Integrating Sciforma with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a1feb-106">Você pode controlar no AD do Azure que tenha acesso tooSciforma</span><span class="sxs-lookup"><span data-stu-id="a1feb-106">You can control in Azure AD who has access tooSciforma</span></span>
- <span data-ttu-id="a1feb-107">Você pode habilitar seu usuários tooautomatically get conectado tooSciforma (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a1feb-107">You can enable your users tooautomatically get signed-on tooSciforma (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a1feb-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a1feb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a1feb-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a1feb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1feb-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a1feb-110">Prerequisites</span></span>

<span data-ttu-id="a1feb-111">tooconfigure integração do AD do Azure com Sciforma, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1feb-111">tooconfigure Azure AD integration with Sciforma, you need hello following items:</span></span>

- <span data-ttu-id="a1feb-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a1feb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a1feb-113">Uma assinatura do Sciforma habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="a1feb-113">A Sciforma single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a1feb-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a1feb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a1feb-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a1feb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a1feb-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a1feb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a1feb-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a1feb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a1feb-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a1feb-118">Scenario description</span></span>
<span data-ttu-id="a1feb-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a1feb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a1feb-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="a1feb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1feb-121">Adicionando Sciforma da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a1feb-121">Adding Sciforma from hello gallery</span></span>
2. <span data-ttu-id="a1feb-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a1feb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciforma-from-hello-gallery"></a><span data-ttu-id="a1feb-123">Adicionando Sciforma da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a1feb-123">Adding Sciforma from hello gallery</span></span>
<span data-ttu-id="a1feb-124">integração de saudação tooconfigure do Sciforma no AD do Azure, você precisa tooadd Sciforma da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a1feb-124">tooconfigure hello integration of Sciforma into Azure AD, you need tooadd Sciforma from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a1feb-125">**tooadd Sciforma da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a1feb-125">**tooadd Sciforma from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1feb-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a1feb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a1feb-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a1feb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a1feb-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a1feb-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a1feb-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a1feb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a1feb-133">Na caixa de pesquisa hello, digite **Sciforma**.</span><span class="sxs-lookup"><span data-stu-id="a1feb-133">In hello search box, type **Sciforma**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_search.png)

5. <span data-ttu-id="a1feb-135">No painel de resultados de saudação, selecione **Sciforma**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a1feb-135">In hello results panel, select **Sciforma**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a1feb-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a1feb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a1feb-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Sciforma, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a1feb-138">In this section, you configure and test Azure AD single sign-on with Sciforma based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a1feb-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Sciforma é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1feb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sciforma is tooa user in Azure AD.</span></span> <span data-ttu-id="a1feb-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Sciforma precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a1feb-140">In other words, a link relationship between an Azure AD user and hello related user in Sciforma needs toobe established.</span></span>

<span data-ttu-id="a1feb-141">No Sciforma, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1feb-141">In Sciforma, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a1feb-142">tooconfigure e teste de logon único do AD do Azure com Sciforma, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1feb-142">tooconfigure and test Azure AD single sign-on with Sciforma, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a1feb-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a1feb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a1feb-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1feb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a1feb-145">**[Criar um usuário de teste do Sciforma](#creating-a-sciforma-test-user)**  -toohave um equivalente do Britta Simon no Sciforma é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="a1feb-145">**[Creating a Sciforma test user](#creating-a-sciforma-test-user)** - toohave a counterpart of Britta Simon in Sciforma that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a1feb-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="a1feb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a1feb-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="a1feb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a1feb-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1feb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a1feb-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Sciforma.</span><span class="sxs-lookup"><span data-stu-id="a1feb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sciforma application.</span></span>

<span data-ttu-id="a1feb-150">**tooconfigure AD do Azure-logon único com Sciforma, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a1feb-150">**tooconfigure Azure AD single sign-on with Sciforma, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1feb-151">Em Olá portal do Azure, Olá **Sciforma** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="a1feb-151">In hello Azure portal, on hello **Sciforma** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a1feb-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="a1feb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_samlbase.png)

3. <span data-ttu-id="a1feb-155">Em Olá **Sciforma domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1feb-155">On hello **Sciforma Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_url.png)

    <span data-ttu-id="a1feb-157">a.</span><span class="sxs-lookup"><span data-stu-id="a1feb-157">a.</span></span> <span data-ttu-id="a1feb-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.sciforma.net/sciforma/main.html`</span><span class="sxs-lookup"><span data-stu-id="a1feb-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sciforma.net/sciforma/main.html`</span></span>

    <span data-ttu-id="a1feb-159">b.</span><span class="sxs-lookup"><span data-stu-id="a1feb-159">b.</span></span> <span data-ttu-id="a1feb-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.sciforma.net/sciforma/saml`</span><span class="sxs-lookup"><span data-stu-id="a1feb-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sciforma.net/sciforma/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a1feb-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="a1feb-161">These values are not real.</span></span> <span data-ttu-id="a1feb-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="a1feb-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a1feb-163">Entre em contato com [equipe de suporte do Sciforma cliente](http://www.sciforma.com/company/contact_us) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="a1feb-163">Contact [Sciforma Client support team](http://www.sciforma.com/company/contact_us) tooget these values.</span></span> 
 


4. <span data-ttu-id="a1feb-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a1feb-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_certificate.png) 

5. <span data-ttu-id="a1feb-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a1feb-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sciforma-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a1feb-168">tooconfigure logon único no **Sciforma** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do Sciforma](http://www.sciforma.com/company/contact_us).</span><span class="sxs-lookup"><span data-stu-id="a1feb-168">tooconfigure single sign-on on **Sciforma** side, you need toosend hello downloaded **Metadata XML** too[Sciforma support team](http://www.sciforma.com/company/contact_us).</span></span>

> [!TIP]
> <span data-ttu-id="a1feb-169">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="a1feb-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a1feb-170">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="a1feb-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a1feb-171">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a1feb-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a1feb-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a1feb-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="a1feb-173">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1feb-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a1feb-175">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a1feb-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1feb-176">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a1feb-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sciforma-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a1feb-178">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="a1feb-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sciforma-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a1feb-180">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1feb-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sciforma-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a1feb-182">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1feb-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sciforma-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a1feb-184">a.</span><span class="sxs-lookup"><span data-stu-id="a1feb-184">a.</span></span> <span data-ttu-id="a1feb-185">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a1feb-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a1feb-186">b.</span><span class="sxs-lookup"><span data-stu-id="a1feb-186">b.</span></span> <span data-ttu-id="a1feb-187">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a1feb-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a1feb-188">c.</span><span class="sxs-lookup"><span data-stu-id="a1feb-188">c.</span></span> <span data-ttu-id="a1feb-189">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="a1feb-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a1feb-190">d.</span><span class="sxs-lookup"><span data-stu-id="a1feb-190">d.</span></span> <span data-ttu-id="a1feb-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a1feb-191">Click **Create**.</span></span>
 
### <a name="creating-a-sciforma-test-user"></a><span data-ttu-id="a1feb-192">Criar um usuário de teste do Sciforma</span><span class="sxs-lookup"><span data-stu-id="a1feb-192">Creating a Sciforma test user</span></span>

<span data-ttu-id="a1feb-193">Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooSciforma.</span><span class="sxs-lookup"><span data-stu-id="a1feb-193">There is no action item for you tooconfigure user provisioning tooSciforma.</span></span> <span data-ttu-id="a1feb-194">Quando um usuário atribuído tenta toolog em tooSciforma usando o painel de acesso hello, o Sciforma verifica se o usuário Olá existe.</span><span class="sxs-lookup"><span data-stu-id="a1feb-194">When an assigned user tries toolog in tooSciforma using hello access panel, Sciforma checks whether hello user exists.</span></span>  

* <span data-ttu-id="a1feb-195">Se ainda não houver uma conta de usuário disponível, ela será automaticamente criada pelo Sciforma.</span><span class="sxs-lookup"><span data-stu-id="a1feb-195">If there is no user account available yet, it is automatically created by Sciforma.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a1feb-196">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a1feb-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a1feb-197">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSciforma.</span><span class="sxs-lookup"><span data-stu-id="a1feb-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSciforma.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a1feb-199">**tooassign Britta Simon tooSciforma, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a1feb-199">**tooassign Britta Simon tooSciforma, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1feb-200">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a1feb-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a1feb-202">Na lista de aplicativos hello, selecione **Sciforma**.</span><span class="sxs-lookup"><span data-stu-id="a1feb-202">In hello applications list, select **Sciforma**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_app.png) 

3. <span data-ttu-id="a1feb-204">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a1feb-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a1feb-206">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a1feb-206">Click **Add** button.</span></span> <span data-ttu-id="a1feb-207">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a1feb-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a1feb-209">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1feb-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a1feb-210">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a1feb-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a1feb-211">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a1feb-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a1feb-212">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a1feb-212">Testing single sign-on</span></span>

<span data-ttu-id="a1feb-213">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a1feb-213">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="a1feb-214">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a1feb-214">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a1feb-215">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a1feb-215">Additional resources</span></span>

* [<span data-ttu-id="a1feb-216">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a1feb-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1feb-217">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a1feb-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_203.png

