---
title: "Tutorial: Integração do Azure Active Directory ao Atomic Learning | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e aprendizado atômica."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 495f54a6-e6c4-41b0-aafa-a6283d33efc8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 12d7c380dbe47899eb35486c5e2a6936e8fb8b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atomic-learning"></a><span data-ttu-id="df5a5-103">Tutorial: integração do Azure Active Directory ao Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="df5a5-103">Tutorial: Azure Active Directory integration with Atomic Learning</span></span>

<span data-ttu-id="df5a5-104">Neste tutorial, você aprenderá como toointegrate atômico aprendizado com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="df5a5-104">In this tutorial, you learn how toointegrate Atomic Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df5a5-105">Integrando atômicas de aprendizado do Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="df5a5-105">Integrating Atomic Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="df5a5-106">Você pode controlar no AD do Azure que tenha acesso tooAtomic de aprendizado</span><span class="sxs-lookup"><span data-stu-id="df5a5-106">You can control in Azure AD who has access tooAtomic Learning</span></span>
- <span data-ttu-id="df5a5-107">Você pode habilitar seu usuários tooautomatically get conectado tooAtomic aprendizado (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df5a5-107">You can enable your users tooautomatically get signed-on tooAtomic Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="df5a5-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="df5a5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="df5a5-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df5a5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df5a5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="df5a5-110">Prerequisites</span></span>

<span data-ttu-id="df5a5-111">tooconfigure integração do AD do Azure com o aprendizado atômico, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="df5a5-111">tooconfigure Azure AD integration with Atomic Learning, you need hello following items:</span></span>

- <span data-ttu-id="df5a5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df5a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df5a5-113">Uma assinatura habilitada para logon único do Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="df5a5-113">An Atomic Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="df5a5-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="df5a5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="df5a5-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="df5a5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df5a5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="df5a5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="df5a5-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df5a5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="df5a5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="df5a5-118">Scenario description</span></span>
<span data-ttu-id="df5a5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="df5a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="df5a5-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="df5a5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df5a5-121">Adicionando atômico aprendizado da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="df5a5-121">Adding Atomic Learning from hello gallery</span></span>
2. <span data-ttu-id="df5a5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df5a5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atomic-learning-from-hello-gallery"></a><span data-ttu-id="df5a5-123">Adicionando atômico aprendizado da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="df5a5-123">Adding Atomic Learning from hello gallery</span></span>
<span data-ttu-id="df5a5-124">integração de saudação tooconfigure do aprendizado atômica no AD do Azure, você precisa tooadd atômico aprendizado da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="df5a5-124">tooconfigure hello integration of Atomic Learning into Azure AD, you need tooadd Atomic Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="df5a5-125">**tooadd atômico aprendizado da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="df5a5-125">**tooadd Atomic Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="df5a5-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="df5a5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="df5a5-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="df5a5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="df5a5-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="df5a5-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="df5a5-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df5a5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="df5a5-133">Na caixa de pesquisa hello, digite **aprendizado atômico**.</span><span class="sxs-lookup"><span data-stu-id="df5a5-133">In hello search box, type **Atomic Learning**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_search.png)

5. <span data-ttu-id="df5a5-135">No painel de resultados de saudação, selecione **aprendizado atômico**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="df5a5-135">In hello results panel, select **Atomic Learning**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="df5a5-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df5a5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="df5a5-138">Nesta seção, você configura e testa o logon único do Azure AD com o Atomic Learning, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="df5a5-138">In this section, you configure and test Azure AD single sign-on with Atomic Learning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="df5a5-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no aprendizado atômico é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="df5a5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atomic Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="df5a5-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no aprendizado atômico precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="df5a5-140">In other words, a link relationship between an Azure AD user and hello related user in Atomic Learning needs toobe established.</span></span>

<span data-ttu-id="df5a5-141">No aprendizado atômica, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="df5a5-141">In Atomic Learning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="df5a5-142">tooconfigure e teste de logon único do AD do Azure com o aprendizado atômico, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="df5a5-142">tooconfigure and test Azure AD single sign-on with Atomic Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="df5a5-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="df5a5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="df5a5-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df5a5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df5a5-145">**[Criar um usuário de teste de aprendizado atômico](#creating-an-atomic-learning-test-user)**  -toohave um equivalente do Britta Simon no aprendizado atômico que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="df5a5-145">**[Creating an Atomic Learning test user](#creating-an-atomic-learning-test-user)** - toohave a counterpart of Britta Simon in Atomic Learning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="df5a5-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="df5a5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df5a5-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="df5a5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="df5a5-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="df5a5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="df5a5-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de aprendizado atômica.</span><span class="sxs-lookup"><span data-stu-id="df5a5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atomic Learning application.</span></span>

<span data-ttu-id="df5a5-150">**tooconfigure AD do Azure-logon único com o aprendizado atômica, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="df5a5-150">**tooconfigure Azure AD single sign-on with Atomic Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="df5a5-151">Em Olá portal do Azure, Olá **aprendizado atômico** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="df5a5-151">In hello Azure portal, on hello **Atomic Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="df5a5-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="df5a5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_samlbase.png)

3. <span data-ttu-id="df5a5-155">Em Olá **domínio atômicas de aprendizado e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="df5a5-155">On hello **Atomic Learning Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_url.png)

     <span data-ttu-id="df5a5-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="df5a5-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="df5a5-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="df5a5-158">This value is not real.</span></span> <span data-ttu-id="df5a5-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="df5a5-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="df5a5-160">Entre em contato com [equipe de suporte do cliente de aprendizado atômico](mailto:cs@atomiclearning.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="df5a5-160">Contact [Atomic Learning Client support team](mailto:cs@atomiclearning.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="df5a5-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="df5a5-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_certificate.png) 

5. <span data-ttu-id="df5a5-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="df5a5-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="df5a5-165">tooconfigure logon único no **aprendizado atômico** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte de aprendizado atômico](mailto:cs@atomiclearning.com).</span><span class="sxs-lookup"><span data-stu-id="df5a5-165">tooconfigure single sign-on on **Atomic Learning** side, you need toosend hello downloaded **Metadata XML** too[Atomic Learning support team](mailto:cs@atomiclearning.com).</span></span> <span data-ttu-id="df5a5-166">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="df5a5-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="df5a5-167">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="df5a5-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="df5a5-168">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="df5a5-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="df5a5-169">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="df5a5-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="df5a5-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df5a5-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="df5a5-171">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="df5a5-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="df5a5-173">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="df5a5-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="df5a5-174">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="df5a5-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="df5a5-176">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="df5a5-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="df5a5-178">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="df5a5-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="df5a5-180">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="df5a5-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="df5a5-182">a.</span><span class="sxs-lookup"><span data-stu-id="df5a5-182">a.</span></span> <span data-ttu-id="df5a5-183">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df5a5-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="df5a5-184">b.</span><span class="sxs-lookup"><span data-stu-id="df5a5-184">b.</span></span> <span data-ttu-id="df5a5-185">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="df5a5-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="df5a5-186">c.</span><span class="sxs-lookup"><span data-stu-id="df5a5-186">c.</span></span> <span data-ttu-id="df5a5-187">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="df5a5-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="df5a5-188">d.</span><span class="sxs-lookup"><span data-stu-id="df5a5-188">d.</span></span> <span data-ttu-id="df5a5-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="df5a5-189">Click **Create**.</span></span>
 
### <a name="creating-an-atomic-learning-test-user"></a><span data-ttu-id="df5a5-190">Criando um usuário de teste do Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="df5a5-190">Creating an Atomic Learning test user</span></span>

<span data-ttu-id="df5a5-191">Nesta seção, você deve criar uma usuária chamada Brenda Fernandes no Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="df5a5-191">In this section, you create a user called Britta Simon in Atomic Learning.</span></span> <span data-ttu-id="df5a5-192">O Atomic Learning dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="df5a5-192">Atomic Learning supports just-in-time provisioning, which is by default enabled.</span></span> 

<span data-ttu-id="df5a5-193">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="df5a5-193">There is no action item for you in this section.</span></span> <span data-ttu-id="df5a5-194">Um novo usuário é criado durante tooaccess uma tentativa de aprendizado atômica se ele não existir ainda usando o endereço de email de saudação do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="df5a5-194">A new user is created during an attempt tooaccess Atomic Learning if it doesn't exist yet using hello email address for hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="df5a5-195">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df5a5-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="df5a5-196">Nesta seção, você deve habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAtomic de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="df5a5-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtomic Learning.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="df5a5-198">**tooassign Britta Simon tooAtomic aprendizado, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="df5a5-198">**tooassign Britta Simon tooAtomic Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="df5a5-199">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="df5a5-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="df5a5-201">Na lista de aplicativos hello, selecione **aprendizado atômico**.</span><span class="sxs-lookup"><span data-stu-id="df5a5-201">In hello applications list, select **Atomic Learning**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_app.png) 

3. <span data-ttu-id="df5a5-203">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="df5a5-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="df5a5-205">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="df5a5-205">Click **Add** button.</span></span> <span data-ttu-id="df5a5-206">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df5a5-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="df5a5-208">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="df5a5-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="df5a5-209">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df5a5-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="df5a5-210">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df5a5-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="df5a5-211">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="df5a5-211">Testing single sign-on</span></span>

<span data-ttu-id="df5a5-212">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="df5a5-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="df5a5-213">Quando você clica em um bloco atômico aprendizado Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de aprendizado atômica.</span><span class="sxs-lookup"><span data-stu-id="df5a5-213">When you click hello Atomic Learning tile in hello Access Panel, you should get automatically signed-on tooyour Atomic Learning application.</span></span>
<span data-ttu-id="df5a5-214">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="df5a5-214">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="df5a5-215">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="df5a5-215">Additional resources</span></span>

* [<span data-ttu-id="df5a5-216">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="df5a5-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df5a5-217">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="df5a5-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_203.png

