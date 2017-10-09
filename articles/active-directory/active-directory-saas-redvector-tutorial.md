---
title: "Tutorial: Integração do Azure Active Directory com o RedVector | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e RedVector."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99042f39-0ab2-475b-8df8-3016d7f875e9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 4b866911769dcd1a5e6fe978f2c42e680215b4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-redvector"></a><span data-ttu-id="79172-103">Tutorial: Integração do Azure Active Directory com o RedVector</span><span class="sxs-lookup"><span data-stu-id="79172-103">Tutorial: Azure Active Directory integration with RedVector</span></span>

<span data-ttu-id="79172-104">Neste tutorial, você aprenderá como toointegrate RedVector com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="79172-104">In this tutorial, you learn how toointegrate RedVector with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79172-105">Integrando RedVector com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="79172-105">Integrating RedVector with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="79172-106">Você pode controlar no AD do Azure que tenha acesso tooRedVector</span><span class="sxs-lookup"><span data-stu-id="79172-106">You can control in Azure AD who has access tooRedVector</span></span>
- <span data-ttu-id="79172-107">Você pode habilitar seu usuários tooautomatically get conectado tooRedVector (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="79172-107">You can enable your users tooautomatically get signed-on tooRedVector (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79172-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="79172-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="79172-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79172-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79172-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="79172-110">Prerequisites</span></span>

<span data-ttu-id="79172-111">tooconfigure integração do AD do Azure com RedVector, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="79172-111">tooconfigure Azure AD integration with RedVector, you need hello following items:</span></span>

- <span data-ttu-id="79172-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="79172-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79172-113">Uma assinatura habilitada para logon único do RedVector</span><span class="sxs-lookup"><span data-stu-id="79172-113">A RedVector single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79172-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="79172-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79172-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="79172-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79172-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="79172-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79172-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79172-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79172-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="79172-118">Scenario description</span></span>
<span data-ttu-id="79172-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="79172-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79172-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="79172-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79172-121">Adicionando RedVector da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="79172-121">Adding RedVector from hello gallery</span></span>
2. <span data-ttu-id="79172-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="79172-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-redvector-from-hello-gallery"></a><span data-ttu-id="79172-123">Adicionando RedVector da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="79172-123">Adding RedVector from hello gallery</span></span>
<span data-ttu-id="79172-124">integração de saudação tooconfigure de RedVector no AD do Azure, você precisa tooadd RedVector da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="79172-124">tooconfigure hello integration of RedVector into Azure AD, you need tooadd RedVector from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="79172-125">**tooadd RedVector da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="79172-125">**tooadd RedVector from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="79172-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="79172-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79172-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="79172-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="79172-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="79172-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="79172-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="79172-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="79172-133">Na caixa de pesquisa hello, digite **RedVector**.</span><span class="sxs-lookup"><span data-stu-id="79172-133">In hello search box, type **RedVector**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_search.png)

5. <span data-ttu-id="79172-135">No painel de resultados de saudação, selecione **RedVector**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="79172-135">In hello results panel, select **RedVector**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79172-137">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="79172-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79172-138">Nesta seção, você configurará e testará o logon único do Azure AD com o RedVector, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="79172-138">In this section, you configure and test Azure AD single sign-on with RedVector based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79172-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em RedVector é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="79172-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RedVector is tooa user in Azure AD.</span></span> <span data-ttu-id="79172-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em RedVector precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="79172-140">In other words, a link relationship between an Azure AD user and hello related user in RedVector needs toobe established.</span></span>

<span data-ttu-id="79172-141">RedVector, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="79172-141">In RedVector, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="79172-142">tooconfigure e teste de logon único do AD do Azure com RedVector, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="79172-142">tooconfigure and test Azure AD single sign-on with RedVector, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="79172-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="79172-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="79172-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79172-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79172-145">**[Criar um usuário de teste RedVector](#creating-a-redvector-test-user)**  -toohave um equivalente do Britta Simon em RedVector é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="79172-145">**[Creating a RedVector test user](#creating-a-redvector-test-user)** - toohave a counterpart of Britta Simon in RedVector that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="79172-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="79172-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79172-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="79172-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79172-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="79172-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79172-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo RedVector.</span><span class="sxs-lookup"><span data-stu-id="79172-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RedVector application.</span></span>

<span data-ttu-id="79172-150">**tooconfigure AD do Azure-logon único com RedVector, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="79172-150">**tooconfigure Azure AD single sign-on with RedVector, perform hello following steps:**</span></span>

1. <span data-ttu-id="79172-151">Em Olá portal do Azure, Olá **RedVector** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="79172-151">In hello Azure portal, on hello **RedVector** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="79172-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="79172-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_samlbase.png)

3. <span data-ttu-id="79172-155">Em Olá **RedVector domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="79172-155">On hello **RedVector Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_url.png)

    <span data-ttu-id="79172-157">a.</span><span class="sxs-lookup"><span data-stu-id="79172-157">a.</span></span> <span data-ttu-id="79172-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://sso2.redvector.com/adfs/<Companyname>`</span><span class="sxs-lookup"><span data-stu-id="79172-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso2.redvector.com/adfs/<Companyname>`</span></span>

    <span data-ttu-id="79172-159">b.</span><span class="sxs-lookup"><span data-stu-id="79172-159">b.</span></span> <span data-ttu-id="79172-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<Companyname>.redvector.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="79172-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<Companyname>.redvector.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79172-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="79172-161">These values are not real.</span></span> <span data-ttu-id="79172-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="79172-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="79172-163">Entre em contato com [equipe de suporte do cliente RedVector](mailto:sso@redvector.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="79172-163">Contact [RedVector Client support team](mailto:sso@redvector.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="79172-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="79172-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_certificate.png) 

5. <span data-ttu-id="79172-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="79172-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-redvector-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="79172-168">Em Olá **RedVector configuração** seção, clique em **configurar RedVector** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="79172-168">On hello **RedVector Configuration** section, click **Configure RedVector** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="79172-169">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="79172-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_configure.png) 

7. <span data-ttu-id="79172-171">tooconfigure logon único no **RedVector** lado, você precisa toosend Olá baixado **certificado (Base64)** e **Single Sign-On URL do serviço SAML** muito[a equipe de suporte RedVector](mailto:sso@redvector.com).</span><span class="sxs-lookup"><span data-stu-id="79172-171">tooconfigure single sign-on on **RedVector** side, you need toosend hello downloaded **Certificate (Base64)** and **SAML Single Sign-On Service URL** too[RedVector support team](mailto:sso@redvector.com).</span></span> <span data-ttu-id="79172-172">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="79172-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="79172-173">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="79172-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="79172-174">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="79172-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="79172-175">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79172-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79172-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="79172-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="79172-177">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="79172-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="79172-179">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="79172-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="79172-180">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="79172-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-redvector-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79172-182">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="79172-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-redvector-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79172-184">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="79172-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-redvector-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79172-186">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="79172-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-redvector-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79172-188">a.</span><span class="sxs-lookup"><span data-stu-id="79172-188">a.</span></span> <span data-ttu-id="79172-189">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79172-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79172-190">b.</span><span class="sxs-lookup"><span data-stu-id="79172-190">b.</span></span> <span data-ttu-id="79172-191">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="79172-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79172-192">c.</span><span class="sxs-lookup"><span data-stu-id="79172-192">c.</span></span> <span data-ttu-id="79172-193">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="79172-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="79172-194">d.</span><span class="sxs-lookup"><span data-stu-id="79172-194">d.</span></span> <span data-ttu-id="79172-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="79172-195">Click **Create**.</span></span>
 
### <a name="creating-a-redvector-test-user"></a><span data-ttu-id="79172-196">Criação de um usuário de teste RedVector</span><span class="sxs-lookup"><span data-stu-id="79172-196">Creating a RedVector test user</span></span>

<span data-ttu-id="79172-197">Nesta seção, você criará um usuário chamado Brenda Fernandes no RedVector.</span><span class="sxs-lookup"><span data-stu-id="79172-197">In this section, you create a user called Britta Simon in RedVector.</span></span> <span data-ttu-id="79172-198">Se você não souber como tooadd Britta Simon em RedVector, trabalhar com [RedVector a equipe de suporte](mailto:sso@redvector.com) tooadd Olá usuário de teste e habilitar o SSO.</span><span class="sxs-lookup"><span data-stu-id="79172-198">If you don't know how tooadd Britta Simon in RedVector, Work with [RedVector support team](mailto:sso@redvector.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="79172-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="79172-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="79172-200">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooRedVector.</span><span class="sxs-lookup"><span data-stu-id="79172-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRedVector.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="79172-202">**tooassign Britta Simon tooRedVector, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="79172-202">**tooassign Britta Simon tooRedVector, perform hello following steps:**</span></span>

1. <span data-ttu-id="79172-203">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="79172-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="79172-205">Na lista de aplicativos hello, selecione **RedVector**.</span><span class="sxs-lookup"><span data-stu-id="79172-205">In hello applications list, select **RedVector**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_app.png) 

3. <span data-ttu-id="79172-207">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="79172-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="79172-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="79172-209">Click **Add** button.</span></span> <span data-ttu-id="79172-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="79172-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="79172-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="79172-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="79172-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="79172-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79172-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="79172-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79172-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="79172-215">Testing single sign-on</span></span>

<span data-ttu-id="79172-216">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="79172-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="79172-217">Quando você clica em bloco RedVector Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour RedVector aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79172-217">When you click hello RedVector tile in hello Access Panel, you should get automatically signed-on tooyour RedVector application..</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79172-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="79172-218">Additional resources</span></span>

* [<span data-ttu-id="79172-219">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="79172-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79172-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="79172-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_203.png

