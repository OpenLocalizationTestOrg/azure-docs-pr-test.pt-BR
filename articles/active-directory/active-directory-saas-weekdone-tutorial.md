---
title: "Tutorial: integração do Azure Active Directory ao Weekdone | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Weekdone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f997f1b49ff1aa0659a2409fdd945c6f96413b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="90f92-103">Tutorial: integração do Azure Active Directory ao Weekdone</span><span class="sxs-lookup"><span data-stu-id="90f92-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="90f92-104">Neste tutorial, você aprenderá como toointegrate Weekdone com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="90f92-104">In this tutorial, you learn how toointegrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="90f92-105">Integrando Weekdone com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="90f92-105">Integrating Weekdone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="90f92-106">Você pode controlar no AD do Azure que tenha acesso tooWeekdone</span><span class="sxs-lookup"><span data-stu-id="90f92-106">You can control in Azure AD who has access tooWeekdone</span></span>
- <span data-ttu-id="90f92-107">Você pode habilitar seu usuários tooautomatically get conectado tooWeekdone (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="90f92-107">You can enable your users tooautomatically get signed-on tooWeekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="90f92-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="90f92-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="90f92-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="90f92-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90f92-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="90f92-110">Prerequisites</span></span>

<span data-ttu-id="90f92-111">tooconfigure integração do AD do Azure com Weekdone, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="90f92-111">tooconfigure Azure AD integration with Weekdone, you need hello following items:</span></span>

- <span data-ttu-id="90f92-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="90f92-112">An Azure AD subscription</span></span>
- <span data-ttu-id="90f92-113">Uma assinatura do Weekdone habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="90f92-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="90f92-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="90f92-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="90f92-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="90f92-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="90f92-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="90f92-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="90f92-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90f92-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="90f92-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="90f92-118">Scenario description</span></span>
<span data-ttu-id="90f92-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="90f92-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="90f92-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="90f92-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="90f92-121">Adicionando Weekdone da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="90f92-121">Adding Weekdone from hello gallery</span></span>
2. <span data-ttu-id="90f92-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="90f92-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-hello-gallery"></a><span data-ttu-id="90f92-123">Adicionando Weekdone da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="90f92-123">Adding Weekdone from hello gallery</span></span>
<span data-ttu-id="90f92-124">integração de saudação tooconfigure de Weekdone no AD do Azure, você precisa tooadd Weekdone da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="90f92-124">tooconfigure hello integration of Weekdone into Azure AD, you need tooadd Weekdone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="90f92-125">**tooadd Weekdone da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="90f92-125">**tooadd Weekdone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="90f92-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="90f92-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="90f92-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="90f92-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="90f92-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="90f92-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="90f92-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="90f92-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="90f92-133">Na caixa de pesquisa hello, digite **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="90f92-133">In hello search box, type **Weekdone**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="90f92-135">No painel de resultados de saudação, selecione **Weekdone**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="90f92-135">In hello results panel, select **Weekdone**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="90f92-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="90f92-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="90f92-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Weekdone com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="90f92-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="90f92-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Weekdone é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="90f92-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Weekdone is tooa user in Azure AD.</span></span> <span data-ttu-id="90f92-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Weekdone precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="90f92-140">In other words, a link relationship between an Azure AD user and hello related user in Weekdone needs toobe established.</span></span>

<span data-ttu-id="90f92-141">Weekdone, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="90f92-141">In Weekdone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="90f92-142">tooconfigure e teste de logon único do AD do Azure com Weekdone, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="90f92-142">tooconfigure and test Azure AD single sign-on with Weekdone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="90f92-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="90f92-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="90f92-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90f92-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="90f92-145">**[Criar um usuário de teste Weekdone](#creating-a-weekdone-test-user)**  -toohave um equivalente do Britta Simon em Weekdone é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="90f92-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - toohave a counterpart of Britta Simon in Weekdone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="90f92-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="90f92-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="90f92-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="90f92-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="90f92-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="90f92-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="90f92-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Weekdone.</span><span class="sxs-lookup"><span data-stu-id="90f92-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="90f92-150">**tooconfigure AD do Azure-logon único com Weekdone, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="90f92-150">**tooconfigure Azure AD single sign-on with Weekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="90f92-151">Em Olá portal do Azure, Olá **Weekdone** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="90f92-151">In hello Azure portal, on hello **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="90f92-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="90f92-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="90f92-155">Em Olá **Weekdone domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="90f92-155">On hello **Weekdone Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="90f92-157">a.</span><span class="sxs-lookup"><span data-stu-id="90f92-157">a.</span></span> <span data-ttu-id="90f92-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="90f92-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="90f92-159">b.</span><span class="sxs-lookup"><span data-stu-id="90f92-159">b.</span></span> <span data-ttu-id="90f92-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="90f92-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="90f92-161">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="90f92-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="90f92-162">Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="90f92-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="90f92-164">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="90f92-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="90f92-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="90f92-165">These values are not real.</span></span> <span data-ttu-id="90f92-166">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="90f92-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="90f92-167">Entre em contato com [equipe de suporte do cliente Weekdone](mailto:hello@weekdone.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="90f92-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) tooget these values.</span></span> 

5. <span data-ttu-id="90f92-168">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="90f92-168">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="90f92-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="90f92-170">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="90f92-172">Em Olá **Weekdone configuração** seção, clique em **configurar Weekdone** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="90f92-172">On hello **Weekdone Configuration** section, click **Configure Weekdone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="90f92-173">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="90f92-173">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="90f92-175">tooconfigure logon único no **Weekdone** lado, você precisa toosend Olá baixado **Metadata XML, URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** muito[Weekdone suporte equipe](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="90f92-175">tooconfigure single sign-on on **Weekdone** side, you need toosend hello downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="90f92-176">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="90f92-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="90f92-177">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="90f92-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="90f92-178">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="90f92-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="90f92-179">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="90f92-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="90f92-180">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="90f92-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="90f92-182">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="90f92-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="90f92-183">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="90f92-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="90f92-185">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="90f92-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="90f92-187">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="90f92-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="90f92-189">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="90f92-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="90f92-191">a.</span><span class="sxs-lookup"><span data-stu-id="90f92-191">a.</span></span> <span data-ttu-id="90f92-192">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="90f92-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="90f92-193">b.</span><span class="sxs-lookup"><span data-stu-id="90f92-193">b.</span></span> <span data-ttu-id="90f92-194">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="90f92-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="90f92-195">c.</span><span class="sxs-lookup"><span data-stu-id="90f92-195">c.</span></span> <span data-ttu-id="90f92-196">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="90f92-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="90f92-197">d.</span><span class="sxs-lookup"><span data-stu-id="90f92-197">d.</span></span> <span data-ttu-id="90f92-198">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="90f92-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="90f92-199">Criando um usuário de teste Weekdone</span><span class="sxs-lookup"><span data-stu-id="90f92-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="90f92-200">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Weekdone.</span><span class="sxs-lookup"><span data-stu-id="90f92-200">hello objective of this section is toocreate a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="90f92-201">O Weekdone dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="90f92-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="90f92-202">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="90f92-202">There is no action item for you in this section.</span></span> <span data-ttu-id="90f92-203">Um novo usuário é criado durante uma tentativa tooaccess Weekdone se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="90f92-203">A new user is created during an attempt tooaccess Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="90f92-204">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [equipe de suporte do cliente Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="90f92-204">If you need toocreate a user manually, you need toocontact hello [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="90f92-205">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="90f92-205">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="90f92-206">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWeekdone.</span><span class="sxs-lookup"><span data-stu-id="90f92-206">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWeekdone.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="90f92-208">**tooassign Britta Simon tooWeekdone, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="90f92-208">**tooassign Britta Simon tooWeekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="90f92-209">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="90f92-209">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="90f92-211">Na lista de aplicativos hello, selecione **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="90f92-211">In hello applications list, select **Weekdone**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="90f92-213">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="90f92-213">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="90f92-215">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="90f92-215">Click **Add** button.</span></span> <span data-ttu-id="90f92-216">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="90f92-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="90f92-218">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="90f92-218">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="90f92-219">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="90f92-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="90f92-220">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="90f92-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="90f92-221">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="90f92-221">Testing single sign-on</span></span>

<span data-ttu-id="90f92-222">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="90f92-222">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="90f92-223">Quando você clica em bloco Weekdone Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Weekdone aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90f92-223">When you click hello Weekdone tile in hello Access Panel, you should get automatically signed-on tooyour Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="90f92-224">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="90f92-224">Additional resources</span></span>

* [<span data-ttu-id="90f92-225">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="90f92-225">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="90f92-226">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="90f92-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

