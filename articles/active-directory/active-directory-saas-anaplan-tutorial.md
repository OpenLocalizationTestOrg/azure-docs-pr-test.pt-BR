---
title: "Tutorial: integração do Azure Active Directory ao Anaplan | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Anaplan."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a9c2914-6c8c-4a88-93e3-3753afb40e6b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: 38eb210d090e7aa720060680259124e941e30541
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-anaplan"></a><span data-ttu-id="80ee2-103">Tutorial: Integração do Azure Active Directory ao Anaplan</span><span class="sxs-lookup"><span data-stu-id="80ee2-103">Tutorial: Azure Active Directory integration with Anaplan</span></span>

<span data-ttu-id="80ee2-104">Neste tutorial, você aprenderá como toointegrate Anaplan com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="80ee2-104">In this tutorial, you learn how toointegrate Anaplan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="80ee2-105">Integrando Anaplan com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="80ee2-105">Integrating Anaplan with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="80ee2-106">Você pode controlar no AD do Azure que tenha acesso tooAnaplan</span><span class="sxs-lookup"><span data-stu-id="80ee2-106">You can control in Azure AD who has access tooAnaplan</span></span>
- <span data-ttu-id="80ee2-107">Você pode habilitar seu usuários tooautomatically get conectado tooAnaplan (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80ee2-107">You can enable your users tooautomatically get signed-on tooAnaplan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="80ee2-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="80ee2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="80ee2-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80ee2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80ee2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="80ee2-110">Prerequisites</span></span>

<span data-ttu-id="80ee2-111">tooconfigure integração do AD do Azure com Anaplan, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="80ee2-111">tooconfigure Azure AD integration with Anaplan, you need hello following items:</span></span>

- <span data-ttu-id="80ee2-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80ee2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="80ee2-113">Uma assinatura habilitada para logon único do Anaplan</span><span class="sxs-lookup"><span data-stu-id="80ee2-113">An Anaplan single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="80ee2-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="80ee2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="80ee2-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="80ee2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="80ee2-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="80ee2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="80ee2-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="80ee2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="80ee2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="80ee2-118">Scenario description</span></span>
<span data-ttu-id="80ee2-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="80ee2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="80ee2-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="80ee2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="80ee2-121">Adicionando Anaplan da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="80ee2-121">Adding Anaplan from hello gallery</span></span>
2. <span data-ttu-id="80ee2-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80ee2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-anaplan-from-hello-gallery"></a><span data-ttu-id="80ee2-123">Adicionando Anaplan da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="80ee2-123">Adding Anaplan from hello gallery</span></span>
<span data-ttu-id="80ee2-124">integração de saudação tooconfigure de Anaplan no AD do Azure, você precisa tooadd Anaplan da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="80ee2-124">tooconfigure hello integration of Anaplan into Azure AD, you need tooadd Anaplan from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="80ee2-125">**tooadd Anaplan da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="80ee2-125">**tooadd Anaplan from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="80ee2-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="80ee2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="80ee2-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="80ee2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="80ee2-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="80ee2-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="80ee2-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80ee2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="80ee2-133">Na caixa de pesquisa hello, digite **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="80ee2-133">In hello search box, type **Anaplan**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_search.png)

5. <span data-ttu-id="80ee2-135">No painel de resultados de saudação, selecione **Anaplan**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="80ee2-135">In hello results panel, select **Anaplan**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="80ee2-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80ee2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="80ee2-138">Nesta seção, você configura e testa o logon único do Azure AD com o Anaplan, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="80ee2-138">In this section, you configure and test Azure AD single sign-on with Anaplan based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="80ee2-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Anaplan é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="80ee2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Anaplan is tooa user in Azure AD.</span></span> <span data-ttu-id="80ee2-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Anaplan precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="80ee2-140">In other words, a link relationship between an Azure AD user and hello related user in Anaplan needs toobe established.</span></span>

<span data-ttu-id="80ee2-141">Anaplan, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="80ee2-141">In Anaplan, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="80ee2-142">tooconfigure e teste de logon único do AD do Azure com Anaplan, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="80ee2-142">tooconfigure and test Azure AD single sign-on with Anaplan, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="80ee2-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="80ee2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="80ee2-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80ee2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="80ee2-145">**[Criar um usuário de teste Anaplan](#creating-an-anaplan-test-user)**  -toohave um equivalente do Britta Simon em Anaplan é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="80ee2-145">**[Creating an Anaplan test user](#creating-an-anaplan-test-user)** - toohave a counterpart of Britta Simon in Anaplan that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="80ee2-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="80ee2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="80ee2-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="80ee2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="80ee2-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="80ee2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="80ee2-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Anaplan.</span><span class="sxs-lookup"><span data-stu-id="80ee2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Anaplan application.</span></span>

<span data-ttu-id="80ee2-150">**tooconfigure AD do Azure-logon único com Anaplan, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="80ee2-150">**tooconfigure Azure AD single sign-on with Anaplan, perform hello following steps:**</span></span>

1. <span data-ttu-id="80ee2-151">Em Olá portal do Azure, Olá **Anaplan** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="80ee2-151">In hello Azure portal, on hello **Anaplan** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="80ee2-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="80ee2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_samlbase.png)

3. <span data-ttu-id="80ee2-155">Em Olá **Anaplan domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="80ee2-155">On hello **Anaplan Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_url.png)

    <span data-ttu-id="80ee2-157">a.</span><span class="sxs-lookup"><span data-stu-id="80ee2-157">a.</span></span> <span data-ttu-id="80ee2-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="80ee2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span></span>

    <span data-ttu-id="80ee2-159">b.</span><span class="sxs-lookup"><span data-stu-id="80ee2-159">b.</span></span> <span data-ttu-id="80ee2-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.anaplan.com`</span><span class="sxs-lookup"><span data-stu-id="80ee2-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.anaplan.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="80ee2-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="80ee2-161">These values are not real.</span></span> <span data-ttu-id="80ee2-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="80ee2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="80ee2-163">Entre em contato com [equipe de suporte do cliente Anaplan](mailto:support@anaplan.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="80ee2-163">Contact [Anaplan Client support team](mailto:support@anaplan.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="80ee2-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="80ee2-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_certificate.png) 

5. <span data-ttu-id="80ee2-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="80ee2-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-anaplan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="80ee2-168">Em Olá **Anaplan configuração** seção, clique em **configurar Anaplan** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="80ee2-168">On hello **Anaplan Configuration** section, click **Configure Anaplan** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="80ee2-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="80ee2-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_configure.png) 

7. <span data-ttu-id="80ee2-171">tooconfigure logon único no **Anaplan** lado, você precisa toosend Olá baixado **Metadata XML**, **ID da entidade SAML**, **Single Sign-On URL do serviço SAML**  e **URL de logout** muito[a equipe de suporte Anaplan](mailto:support@anaplan.com).</span><span class="sxs-lookup"><span data-stu-id="80ee2-171">tooconfigure single sign-on on **Anaplan** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL**   too[Anaplan support team](mailto:support@anaplan.com).</span></span> <span data-ttu-id="80ee2-172">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="80ee2-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="80ee2-173">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="80ee2-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="80ee2-174">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="80ee2-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="80ee2-175">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="80ee2-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="80ee2-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80ee2-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="80ee2-177">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="80ee2-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="80ee2-179">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="80ee2-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="80ee2-180">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="80ee2-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-anaplan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="80ee2-182">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="80ee2-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-anaplan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="80ee2-184">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="80ee2-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-anaplan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="80ee2-186">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="80ee2-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-anaplan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="80ee2-188">a.</span><span class="sxs-lookup"><span data-stu-id="80ee2-188">a.</span></span> <span data-ttu-id="80ee2-189">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="80ee2-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="80ee2-190">b.</span><span class="sxs-lookup"><span data-stu-id="80ee2-190">b.</span></span> <span data-ttu-id="80ee2-191">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="80ee2-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="80ee2-192">c.</span><span class="sxs-lookup"><span data-stu-id="80ee2-192">c.</span></span> <span data-ttu-id="80ee2-193">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="80ee2-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="80ee2-194">d.</span><span class="sxs-lookup"><span data-stu-id="80ee2-194">d.</span></span> <span data-ttu-id="80ee2-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="80ee2-195">Click **Create**.</span></span>
 
### <a name="creating-an-anaplan-test-user"></a><span data-ttu-id="80ee2-196">Criando um usuário de teste do Anaplan</span><span class="sxs-lookup"><span data-stu-id="80ee2-196">Creating an Anaplan test user</span></span>

<span data-ttu-id="80ee2-197">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Anaplan.</span><span class="sxs-lookup"><span data-stu-id="80ee2-197">In this section, you create a user called Britta Simon in Anaplan.</span></span> <span data-ttu-id="80ee2-198">Trabalhe com [Anaplan a equipe de suporte](mailto:support@anaplan.com) tooadd usuários de saudação na plataforma de Anaplan hello.</span><span class="sxs-lookup"><span data-stu-id="80ee2-198">Please work with [Anaplan support team](mailto:support@anaplan.com) tooadd hello users in hello Anaplan platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="80ee2-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80ee2-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="80ee2-200">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAnaplan.</span><span class="sxs-lookup"><span data-stu-id="80ee2-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAnaplan.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="80ee2-202">**tooassign Britta Simon tooAnaplan, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="80ee2-202">**tooassign Britta Simon tooAnaplan, perform hello following steps:**</span></span>

1. <span data-ttu-id="80ee2-203">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="80ee2-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="80ee2-205">Na lista de aplicativos hello, selecione **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="80ee2-205">In hello applications list, select **Anaplan**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_app.png) 

3. <span data-ttu-id="80ee2-207">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="80ee2-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="80ee2-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="80ee2-209">Click **Add** button.</span></span> <span data-ttu-id="80ee2-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80ee2-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="80ee2-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="80ee2-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="80ee2-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80ee2-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="80ee2-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80ee2-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="80ee2-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="80ee2-215">Testing single sign-on</span></span>

<span data-ttu-id="80ee2-216">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="80ee2-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="80ee2-217">Quando você clica em bloco Anaplan Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Anaplan aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80ee2-217">When you click hello Anaplan tile in hello Access Panel, you should get automatically signed-on tooyour Anaplan application.</span></span>

<span data-ttu-id="80ee2-218">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="80ee2-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="80ee2-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="80ee2-219">Additional resources</span></span>

* [<span data-ttu-id="80ee2-220">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="80ee2-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80ee2-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="80ee2-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_203.png

