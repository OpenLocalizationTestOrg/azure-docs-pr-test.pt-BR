---
title: "Tutorial: Integração do Azure Active Directory com o Learning at Work | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e aprendizado no trabalho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: fa09d585d57932a95cadba9a66029765d7df3694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a><span data-ttu-id="90193-103">Tutorial: Integração do Azure Active Directory com o Learning at Work</span><span class="sxs-lookup"><span data-stu-id="90193-103">Tutorial: Azure Active Directory integration with Learning at Work</span></span>

<span data-ttu-id="90193-104">Neste tutorial, você aprenderá como toointegrate aprendizado no trabalho com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="90193-104">In this tutorial, you learn how toointegrate Learning at Work with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="90193-105">Integração de aprendizado no trabalho com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="90193-105">Integrating Learning at Work with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="90193-106">Você pode controlar no AD do Azure que tenha acesso tooLearning no trabalho</span><span class="sxs-lookup"><span data-stu-id="90193-106">You can control in Azure AD who has access tooLearning at Work</span></span>
- <span data-ttu-id="90193-107">Você pode habilitar seu usuários tooautomatically get conectado tooLearning no trabalho (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="90193-107">You can enable your users tooautomatically get signed-on tooLearning at Work (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="90193-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="90193-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="90193-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="90193-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90193-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="90193-110">Prerequisites</span></span>

<span data-ttu-id="90193-111">tooconfigure integração do AD do Azure com o aprendizado no trabalho, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="90193-111">tooconfigure Azure AD integration with Learning at Work, you need hello following items:</span></span>

- <span data-ttu-id="90193-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="90193-112">An Azure AD subscription</span></span>
- <span data-ttu-id="90193-113">Uma assinatura com logon único habilitado do Learning at Work</span><span class="sxs-lookup"><span data-stu-id="90193-113">A Learning at Work single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="90193-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="90193-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="90193-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="90193-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="90193-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="90193-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="90193-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90193-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="90193-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="90193-118">Scenario description</span></span>
<span data-ttu-id="90193-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="90193-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="90193-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="90193-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="90193-121">Adição de aprendizado no trabalho da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="90193-121">Adding Learning at Work from hello gallery</span></span>
2. <span data-ttu-id="90193-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="90193-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-at-work-from-hello-gallery"></a><span data-ttu-id="90193-123">Adição de aprendizado no trabalho da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="90193-123">Adding Learning at Work from hello gallery</span></span>
<span data-ttu-id="90193-124">integração de saudação tooconfigure de aprendizagem no trabalho no Azure AD, você precisa tooadd aprendizado no trabalho da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="90193-124">tooconfigure hello integration of Learning at Work into Azure AD, you need tooadd Learning at Work from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="90193-125">**tooadd de aprendizagem no trabalho da Galeria hello, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="90193-125">**tooadd Learning at Work from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="90193-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="90193-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="90193-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="90193-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="90193-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="90193-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="90193-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="90193-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="90193-133">Na caixa de pesquisa hello, digite **aprendizado no trabalho**.</span><span class="sxs-lookup"><span data-stu-id="90193-133">In hello search box, type **Learning at Work**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_search.png)

5. <span data-ttu-id="90193-135">No painel de resultados de saudação, selecione **aprendizado no trabalho**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="90193-135">In hello results panel, select **Learning at Work**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="90193-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="90193-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="90193-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Learning at Work, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="90193-138">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="90193-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no aprendizado de trabalho é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="90193-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning at Work is tooa user in Azure AD.</span></span> <span data-ttu-id="90193-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no aprendizado de trabalho precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="90193-140">In other words, a link relationship between an Azure AD user and hello related user in Learning at Work needs toobe established.</span></span>

<span data-ttu-id="90193-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no aprendizado no trabalho.</span><span class="sxs-lookup"><span data-stu-id="90193-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning at Work.</span></span>

<span data-ttu-id="90193-142">tooconfigure e teste de logon único do AD do Azure com o aprendizado no trabalho, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="90193-142">tooconfigure and test Azure AD single sign-on with Learning at Work, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="90193-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="90193-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="90193-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90193-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="90193-145">**[Criando um aprendizado no usuário de teste de trabalho](#creating-a-learning-at-work-test-user)**  -toohave um equivalente do Britta Simon no aprendizado no trabalho que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="90193-145">**[Creating a Learning at Work test user](#creating-a-learning-at-work-test-user)** - toohave a counterpart of Britta Simon in Learning at Work that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="90193-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="90193-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="90193-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="90193-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="90193-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="90193-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="90193-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único do aprendizado no aplicativo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="90193-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning at Work application.</span></span>

<span data-ttu-id="90193-150">**tooconfigure AD do Azure-logon único com o aprendizado no trabalho, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="90193-150">**tooconfigure Azure AD single sign-on with Learning at Work, perform hello following steps:**</span></span>

1. <span data-ttu-id="90193-151">Em Olá portal do Azure, Olá **aprendizado no trabalho** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="90193-151">In hello Azure portal, on hello **Learning at Work** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="90193-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="90193-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_samlbase.png)

3. <span data-ttu-id="90193-155">Em Olá **no domínio de trabalho e as URLs de aprendizado** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="90193-155">On hello **Learning at Work Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_url.png)

    <span data-ttu-id="90193-157">a.</span><span class="sxs-lookup"><span data-stu-id="90193-157">a.</span></span> <span data-ttu-id="90193-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span><span class="sxs-lookup"><span data-stu-id="90193-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span></span>

    <span data-ttu-id="90193-159">b.</span><span class="sxs-lookup"><span data-stu-id="90193-159">b.</span></span> <span data-ttu-id="90193-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span><span class="sxs-lookup"><span data-stu-id="90193-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="90193-161">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="90193-161">These values are not hello real.</span></span> <span data-ttu-id="90193-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="90193-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="90193-163">Entre em contato com [aprendizado na equipe de suporte de trabalho cliente](https://www.learninga-z.com/site/contact/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="90193-163">Contact [Learning at Work Client support team](https://www.learninga-z.com/site/contact/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="90193-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="90193-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_certificate.png) 

5. <span data-ttu-id="90193-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="90193-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="90193-168">Em Olá **na configuração de trabalho de aprendizado** seção, clique em **configurar aprendizado no trabalho** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="90193-168">On hello **Learning at Work Configuration** section, click **Configure Learning at Work** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="90193-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="90193-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_configure.png) 

7. <span data-ttu-id="90193-171">tooconfigure logon único no **aprendizado no trabalho** lado, você precisa toosend Olá baixado **Metadata XML**, **ID da entidade SAML**, **SAML Single Sign-On URL do serviço**, e **URL de logout** muito[aprendizado no suporte de trabalho](https://www.learninga-z.com/site/contact/support).</span><span class="sxs-lookup"><span data-stu-id="90193-171">tooconfigure single sign-on on **Learning at Work** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL** too[Learning at Work support](https://www.learninga-z.com/site/contact/support).</span></span>

> [!TIP]
> <span data-ttu-id="90193-172">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="90193-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="90193-173">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="90193-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="90193-174">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="90193-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="90193-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="90193-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="90193-176">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="90193-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="90193-178">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="90193-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="90193-179">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="90193-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="90193-181">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="90193-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="90193-183">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="90193-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="90193-185">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="90193-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="90193-187">a.</span><span class="sxs-lookup"><span data-stu-id="90193-187">a.</span></span> <span data-ttu-id="90193-188">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="90193-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="90193-189">b.</span><span class="sxs-lookup"><span data-stu-id="90193-189">b.</span></span> <span data-ttu-id="90193-190">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="90193-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="90193-191">c.</span><span class="sxs-lookup"><span data-stu-id="90193-191">c.</span></span> <span data-ttu-id="90193-192">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="90193-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="90193-193">d.</span><span class="sxs-lookup"><span data-stu-id="90193-193">d.</span></span> <span data-ttu-id="90193-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="90193-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-at-work-test-user"></a><span data-ttu-id="90193-195">Criar um usuário de teste do Learning at Work</span><span class="sxs-lookup"><span data-stu-id="90193-195">Creating a Learning at Work test user</span></span>

<span data-ttu-id="90193-196">Nesta seção, você deve criar uma usuária chamada Brenda Fernandes no Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="90193-196">In this section, you create a user called Britta Simon in Learning at Work.</span></span> <span data-ttu-id="90193-197">Trabalhar com [aprendizado no suporte de trabalho](https://www.learninga-z.com/site/contact/support) usuários Olá tooadd Olá aprendizado na plataforma de trabalho.</span><span class="sxs-lookup"><span data-stu-id="90193-197">Work with [Learning at Work support](https://www.learninga-z.com/site/contact/support) tooadd hello users in hello Learning at Work platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="90193-198">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="90193-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="90193-199">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLearning no trabalho.</span><span class="sxs-lookup"><span data-stu-id="90193-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning at Work.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="90193-201">**tooassign Britta Simon tooLearning no trabalho, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="90193-201">**tooassign Britta Simon tooLearning at Work, perform hello following steps:**</span></span>

1. <span data-ttu-id="90193-202">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="90193-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="90193-204">Na lista de aplicativos hello, selecione **aprendizado no trabalho**.</span><span class="sxs-lookup"><span data-stu-id="90193-204">In hello applications list, select **Learning at Work**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_app.png) 

3. <span data-ttu-id="90193-206">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="90193-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="90193-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="90193-208">Click **Add** button.</span></span> <span data-ttu-id="90193-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="90193-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="90193-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="90193-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="90193-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="90193-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="90193-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="90193-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="90193-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="90193-214">Testing single sign-on</span></span>

<span data-ttu-id="90193-215">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="90193-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="90193-216">Quando você clica em hello aprendizado no bloco de trabalho no hello painel de acesso, você deve obter automaticamente assinado em tooyour aprendizado no aplicativo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="90193-216">When you click hello Learning at Work tile in hello Access Panel, you should get automatically signed-on tooyour Learning at Work application.</span></span>
<span data-ttu-id="90193-217">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="90193-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="90193-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="90193-218">Additional resources</span></span>

* [<span data-ttu-id="90193-219">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="90193-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="90193-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="90193-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_203.png

