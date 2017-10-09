---
title: "Tutorial: Integração do Azure Active Directory ao Symantec WSS (Web Security Service) | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Symantec Web segurança Service (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: f4575e6f5eb63cd0e1d63edd35e30be3cacc3382
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="ec6f7-103">Tutorial: Integração do Azure Active Directory ao Symantec WSS (Web Security Service)</span><span class="sxs-lookup"><span data-stu-id="ec6f7-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="ec6f7-104">Neste tutorial, você aprenderá como toointegrate Symantec Web segurança Service (WSS) com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="ec6f7-104">In this tutorial, you learn how toointegrate Symantec Web Security Service (WSS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ec6f7-105">Integrando o Symantec Web segurança Service (WSS) com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec6f7-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ec6f7-106">Você pode controlar no AD do Azure que tenha acesso tooSymantec segurança de Web Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="ec6f7-106">You can control in Azure AD who has access tooSymantec Web Security Service (WSS)</span></span>
- <span data-ttu-id="ec6f7-107">Você pode habilitar seu usuários tooautomatically get conectado tooSymantec Web segurança Service (WSS) (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ec6f7-107">You can enable your users tooautomatically get signed-on tooSymantec Web Security Service (WSS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ec6f7-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ec6f7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ec6f7-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ec6f7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec6f7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ec6f7-110">Prerequisites</span></span>

<span data-ttu-id="ec6f7-111">tooconfigure integração do AD do Azure com o Symantec Web segurança Service (WSS), você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec6f7-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="ec6f7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ec6f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ec6f7-113">Uma assinatura habilitada para logon único do Symantec WSS (Web Security Service)</span><span class="sxs-lookup"><span data-stu-id="ec6f7-113">A Symantec Web Security Service (WSS) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ec6f7-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ec6f7-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ec6f7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ec6f7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ec6f7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec6f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ec6f7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ec6f7-118">Scenario description</span></span>
<span data-ttu-id="ec6f7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ec6f7-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="ec6f7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ec6f7-121">Adicionando Symantec Web segurança Service (WSS) da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ec6f7-121">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
2. <span data-ttu-id="ec6f7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ec6f7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="ec6f7-123">Adicionando Symantec Web segurança Service (WSS) da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ec6f7-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="ec6f7-124">integração de saudação do tooconfigure da Symantec Web segurança Service (WSS) no AD do Azure, você precisa tooadd Symantec Web segurança Service (WSS) na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ec6f7-125">**tooadd Symantec Web segurança Service (WSS) da Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ec6f7-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec6f7-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ec6f7-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ec6f7-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ec6f7-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ec6f7-133">Na caixa de pesquisa hello, digite **Symantec Web segurança Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-133">In hello search box, type **Symantec Web Security Service (WSS)**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_search.png)

5. <span data-ttu-id="ec6f7-135">No painel de resultados de saudação, selecione **Symantec Web segurança Service (WSS)**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-135">In hello results panel, select **Symantec Web Security Service (WSS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ec6f7-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ec6f7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ec6f7-138">Nesta seção, você configura e testa o logon único do Azure AD com o Symantec WSS (Web Security Service), com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-138">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ec6f7-139">Para toowork de logon único, o AD do Azure precisa tooknow que o usuário de contraparte Olá no Symantec Web segurança Service (WSS) é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="ec6f7-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Symantec Web segurança Service (WSS) precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-140">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="ec6f7-141">No Web segurança Service (WSS) de Symantec, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-141">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ec6f7-142">tooconfigure e teste de logon único do AD do Azure com o Symantec Web segurança Service (WSS), você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec6f7-142">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ec6f7-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ec6f7-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ec6f7-145">**[Criar um usuário de teste do serviço de segurança da Web da Symantec (WSS)](#creating-a-symantec-web-security-service-wss-test-user)**  -toohave um equivalente de Britta Simon na segurança de Web da Symantec Service (WSS) que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-145">**[Creating a Symantec Web Security Service (WSS) test user](#creating-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ec6f7-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ec6f7-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ec6f7-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec6f7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ec6f7-149">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de serviço de segurança da Web da Symantec (WSS).</span><span class="sxs-lookup"><span data-stu-id="ec6f7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="ec6f7-150">**tooconfigure logon único do AD do Azure com o Web segurança Service (WSS) de Symantec, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ec6f7-150">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="ec6f7-151">Em Olá portal do Azure, Olá **Symantec Web segurança Service (WSS)** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-151">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ec6f7-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="ec6f7-155">Em Olá **Symantec Web segurança Service (WSS) domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec6f7-155">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="ec6f7-157">a.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-157">a.</span></span> <span data-ttu-id="ec6f7-158">Em Olá **URL de logon** caixa de texto, mencione Olá url, que você deseja tooblock de acordo com a política de bloqueio de toohello de saudação Symantec Web segurança Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="ec6f7-158">In hello **Sign-on URL** textbox, mention hello url, which you want tooblock according toohello blocking policy of hello Symantec Web Security Service (WSS).</span></span>  
    
    <span data-ttu-id="ec6f7-159">b.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-159">b.</span></span> <span data-ttu-id="ec6f7-160">Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="ec6f7-160">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ec6f7-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-161">These values are not real.</span></span> <span data-ttu-id="ec6f7-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ec6f7-163">Entre em contato com [equipe de suporte do cliente do serviço de segurança da Web da Symantec (WSS)](https://www.symantec.com/contact-us) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-163">Contact [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="ec6f7-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="ec6f7-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ec6f7-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ec6f7-168">tooconfigure logon único no **Symantec Web segurança Service (WSS)** lado, você precisa toosend Olá baixado **Metadata XML** muito[daequipedesuportedoserviçodesegurançadaWebdaSymantec(WSS)](https://www.symantec.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="ec6f7-168">tooconfigure single sign-on on **Symantec Web Security Service (WSS)** side, you need toosend hello downloaded **Metadata XML** too[Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="ec6f7-169">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="ec6f7-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ec6f7-170">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ec6f7-171">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ec6f7-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ec6f7-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ec6f7-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="ec6f7-173">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ec6f7-175">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ec6f7-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ec6f7-176">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ec6f7-178">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ec6f7-180">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ec6f7-182">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec6f7-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ec6f7-184">a.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-184">a.</span></span> <span data-ttu-id="ec6f7-185">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ec6f7-186">b.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-186">b.</span></span> <span data-ttu-id="ec6f7-187">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ec6f7-188">c.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-188">c.</span></span> <span data-ttu-id="ec6f7-189">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ec6f7-190">d.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-190">d.</span></span> <span data-ttu-id="ec6f7-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-191">Click **Create**.</span></span>
 
### <a name="creating-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="ec6f7-192">Criando um usuário de teste do Symantec WSS (Web Security Service)</span><span class="sxs-lookup"><span data-stu-id="ec6f7-192">Creating a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="ec6f7-193">Nesta seção, você cria um usuário chamado Brenda Fernandes no Symantec WSS (Web Security Service).</span><span class="sxs-lookup"><span data-stu-id="ec6f7-193">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="ec6f7-194">Trabalhar com [equipe de suporte do serviço de segurança da Web da Symantec (WSS)](https://www.symantec.com/contact-us) para adicionar usuários de saudação na plataforma do hello Symantec Web segurança Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="ec6f7-194">Work with [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) to add hello users in hello Symantec Web Security Service (WSS) platform.</span></span> <span data-ttu-id="ec6f7-195">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-195">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="ec6f7-196">Também juntamente com hello usuário detalhes você precisa toosend Olá IPaddress público da máquina de saudação do qual você está tentando aplicativo hello de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-196">Also along with hello user details you need toosend hello public IPaddress of hello machine from which you are trying tooaccess hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="ec6f7-197">Por favor, [clique aqui](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget sua máquina do pública IPaddress.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-197">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ec6f7-198">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ec6f7-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ec6f7-199">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSymantec segurança de Web Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="ec6f7-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ec6f7-201">**tooassign Britta Simon tooSymantec Web segurança Service (WSS), execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ec6f7-201">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="ec6f7-202">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ec6f7-204">Na lista de aplicativos hello, selecione **Symantec Web segurança Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-204">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_app.png) 

3. <span data-ttu-id="ec6f7-206">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ec6f7-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-208">Click **Add** button.</span></span> <span data-ttu-id="ec6f7-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ec6f7-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ec6f7-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ec6f7-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ec6f7-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ec6f7-214">Testing single sign-on</span></span>

<span data-ttu-id="ec6f7-215">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ec6f7-216">Quando você clica em Olá Symantec Web segurança Service (WSS) lado a lado no painel de acesso de saudação, você obtém redirecionado toohello bloqueio de página para o qual a política de bloqueio de saudação foi configurada.</span><span class="sxs-lookup"><span data-stu-id="ec6f7-216">When you click hello Symantec Web Security Service (WSS) tile in hello Access Panel, you get redirected toohello blocking page for which hello blocking policy has been configured.</span></span>
<span data-ttu-id="ec6f7-217">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ec6f7-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec6f7-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ec6f7-218">Additional resources</span></span>

* [<span data-ttu-id="ec6f7-219">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ec6f7-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ec6f7-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ec6f7-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_203.png

