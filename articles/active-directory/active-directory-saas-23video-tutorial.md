---
title: "Tutorial: integração do Azure Active Directory com o 23 Video | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e 23 de vídeo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 3430e4db3cd1114db62233e6699618071a3646ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="a59f2-103">Tutorial: integração do Active Directory do Azure com o 23 Video</span><span class="sxs-lookup"><span data-stu-id="a59f2-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="a59f2-104">Neste tutorial, você aprenderá como toointegrate 23 vídeo com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="a59f2-104">In this tutorial, you learn how toointegrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a59f2-105">Integrando 23 vídeo com o Azure AD fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="a59f2-105">Integrating 23 Video with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a59f2-106">Você pode controlar no AD do Azure que tenha acesso too23 vídeo</span><span class="sxs-lookup"><span data-stu-id="a59f2-106">You can control in Azure AD who has access too23 Video</span></span>
- <span data-ttu-id="a59f2-107">Você pode permitir que os usuários tooautomatically obter assinado no vídeo too23 (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a59f2-107">You can enable your users tooautomatically get signed-on too23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a59f2-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a59f2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a59f2-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a59f2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a59f2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a59f2-110">Prerequisites</span></span>

<span data-ttu-id="a59f2-111">tooconfigure integração do AD do Azure com vídeo 23, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="a59f2-111">tooconfigure Azure AD integration with 23 Video, you need hello following items:</span></span>

- <span data-ttu-id="a59f2-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a59f2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a59f2-113">Uma assinatura habilitada para logon único do 23 Video</span><span class="sxs-lookup"><span data-stu-id="a59f2-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a59f2-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a59f2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a59f2-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a59f2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a59f2-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a59f2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a59f2-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a59f2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a59f2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a59f2-118">Scenario description</span></span>
<span data-ttu-id="a59f2-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a59f2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a59f2-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="a59f2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a59f2-121">Adicionando 23 vídeo da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a59f2-121">Adding 23 Video from hello gallery</span></span>
2. <span data-ttu-id="a59f2-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a59f2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-hello-gallery"></a><span data-ttu-id="a59f2-123">Adicionando 23 vídeo da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a59f2-123">Adding 23 Video from hello gallery</span></span>
<span data-ttu-id="a59f2-124">integração de saudação tooconfigure de vídeo 23 no AD do Azure, você precisa tooadd 23 vídeo da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a59f2-124">tooconfigure hello integration of 23 Video into Azure AD, you need tooadd 23 Video from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a59f2-125">**Executar de vídeo da Galeria de saudação tooadd 23 Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a59f2-125">**tooadd 23 Video from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a59f2-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a59f2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a59f2-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a59f2-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a59f2-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a59f2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a59f2-133">Na caixa de pesquisa hello, digite **vídeo 23**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-133">In hello search box, type **23 Video**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="a59f2-135">No painel de resultados de saudação, selecione **vídeo 23**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a59f2-135">In hello results panel, select **23 Video**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a59f2-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a59f2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a59f2-138">Nesta seção, você configurará e testará o logon único do Azure AD com o 23 Video, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a59f2-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a59f2-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá 23 vídeo é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a59f2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 23 Video is tooa user in Azure AD.</span></span> <span data-ttu-id="a59f2-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em 23 vídeo precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a59f2-140">In other words, a link relationship between an Azure AD user and hello related user in 23 Video needs toobe established.</span></span>

<span data-ttu-id="a59f2-141">Vídeo 23, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="a59f2-141">In 23 Video, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a59f2-142">tooconfigure e teste de logon único do AD do Azure com vídeo 23, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="a59f2-142">tooconfigure and test Azure AD single sign-on with 23 Video, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a59f2-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a59f2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a59f2-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a59f2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a59f2-145">**[Criar um usuário de teste de vídeo 23](#creating-a-23-video-test-user)**  -toohave um equivalente do Britta Simon 23 vídeo que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="a59f2-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - toohave a counterpart of Britta Simon in 23 Video that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a59f2-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="a59f2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a59f2-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="a59f2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a59f2-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a59f2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a59f2-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de vídeo 23.</span><span class="sxs-lookup"><span data-stu-id="a59f2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="a59f2-150">**tooconfigure AD do Azure-logon único com vídeo 23, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a59f2-150">**tooconfigure Azure AD single sign-on with 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="a59f2-151">Em Olá portal do Azure, Olá **vídeo 23** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-151">In hello Azure portal, on hello **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a59f2-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="a59f2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="a59f2-155">Em Olá **23 URLs e domínio de vídeo** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a59f2-155">On hello **23 Video Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="a59f2-157">a.</span><span class="sxs-lookup"><span data-stu-id="a59f2-157">a.</span></span> <span data-ttu-id="a59f2-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="a59f2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="a59f2-159">b.</span><span class="sxs-lookup"><span data-stu-id="a59f2-159">b.</span></span> <span data-ttu-id="a59f2-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="a59f2-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a59f2-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="a59f2-161">These values are not real.</span></span> <span data-ttu-id="a59f2-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="a59f2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a59f2-163">Entre em contato com [23 equipe de suporte de cliente de vídeo](mailto:support@23company.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="a59f2-163">Contact [23 Video Client support team](mailto:support@23company.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="a59f2-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a59f2-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="a59f2-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a59f2-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a59f2-168">Em Olá **configuração de vídeo 23** seção, clique em **configurar 23 vídeo** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="a59f2-168">On hello **23 Video Configuration** section, click **Configure 23 Video** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a59f2-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="a59f2-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="a59f2-171">tooconfigure logon único no **vídeo 23** lado, você precisa toosend Olá baixado **certificado (Base64)**, **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML**muito[23 equipe de suporte de vídeo](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="a59f2-171">tooconfigure single sign-on on **23 Video** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="a59f2-172">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="a59f2-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a59f2-173">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="a59f2-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a59f2-174">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a59f2-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a59f2-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a59f2-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="a59f2-176">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a59f2-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a59f2-178">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a59f2-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a59f2-179">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a59f2-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a59f2-181">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a59f2-183">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a59f2-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a59f2-185">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a59f2-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a59f2-187">a.</span><span class="sxs-lookup"><span data-stu-id="a59f2-187">a.</span></span> <span data-ttu-id="a59f2-188">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a59f2-189">b.</span><span class="sxs-lookup"><span data-stu-id="a59f2-189">b.</span></span> <span data-ttu-id="a59f2-190">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a59f2-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a59f2-191">c.</span><span class="sxs-lookup"><span data-stu-id="a59f2-191">c.</span></span> <span data-ttu-id="a59f2-192">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a59f2-193">d.</span><span class="sxs-lookup"><span data-stu-id="a59f2-193">d.</span></span> <span data-ttu-id="a59f2-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="a59f2-195">Criando um usuário de teste do 23 Video</span><span class="sxs-lookup"><span data-stu-id="a59f2-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="a59f2-196">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon vídeo 23.</span><span class="sxs-lookup"><span data-stu-id="a59f2-196">hello objective of this section is toocreate a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="a59f2-197">**toocreate um usuário chamado Britta Simon vídeo 23, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a59f2-197">**toocreate a user called Britta Simon in 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="a59f2-198">Faça logon no tooyour 23 site da empresa de vídeo como administrador.</span><span class="sxs-lookup"><span data-stu-id="a59f2-198">Sign on tooyour 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="a59f2-199">Vá muito**configurações**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-199">Go too**Settings**.</span></span>
 
3. <span data-ttu-id="a59f2-200">Na seção **Usuários**, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-200">In **Users** section, click **Configure**.</span></span>
   
    ![Atribuir usuário][400]

4. <span data-ttu-id="a59f2-202">Clique em **Adicionar um novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-202">Click **Add a new user**.</span></span> 
   
    ![Atribuir usuário][401]

5. <span data-ttu-id="a59f2-204">Em Olá **convidar alguém toojoin este site** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a59f2-204">In hello **Invite someone toojoin this site** section, perform hello following steps:</span></span>
   
    ![Atribuir usuário][402]

    <span data-ttu-id="a59f2-206">a.</span><span class="sxs-lookup"><span data-stu-id="a59f2-206">a.</span></span> <span data-ttu-id="a59f2-207">Em Olá **endereços de email** caixa de texto, digite o endereço de email Britta Simon no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a59f2-207">In hello **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="a59f2-208">b.</span><span class="sxs-lookup"><span data-stu-id="a59f2-208">b.</span></span> <span data-ttu-id="a59f2-209">Clique em **adicionar usuário de saudação**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-209">Click **Add hello user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a59f2-210">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a59f2-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a59f2-211">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso too23 vídeo.</span><span class="sxs-lookup"><span data-stu-id="a59f2-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too23 Video.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a59f2-213">**tooassign Britta Simon too23 vídeo, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a59f2-213">**tooassign Britta Simon too23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="a59f2-214">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a59f2-216">Na lista de aplicativos hello, selecione **vídeo 23**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-216">In hello applications list, select **23 Video**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="a59f2-218">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a59f2-220">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a59f2-220">Click **Add** button.</span></span> <span data-ttu-id="a59f2-221">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a59f2-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a59f2-223">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="a59f2-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a59f2-224">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a59f2-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a59f2-225">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a59f2-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a59f2-226">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a59f2-226">Testing single sign-on</span></span>

<span data-ttu-id="a59f2-227">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a59f2-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a59f2-228">Quando você clica em um bloco de vídeo Olá 23 Olá painel de acesso, você deve obter aplicativos de vídeo tooyour automaticamente conectado em 23.</span><span class="sxs-lookup"><span data-stu-id="a59f2-228">When you click hello 23 Video tile in hello Access Panel, you should get automatically signed-on tooyour 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a59f2-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a59f2-229">Additional resources</span></span>

* [<span data-ttu-id="a59f2-230">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a59f2-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a59f2-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a59f2-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
