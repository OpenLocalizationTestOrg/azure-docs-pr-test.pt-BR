---
title: "Tutorial: integração do Azure Active Directory ao Tidemark | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Tidemark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5cf80d4e-6e8b-48ec-81c8-27872af5e5d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 4fffee30370d928ae8070a5904c58ba8a7a06343
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tidemark"></a><span data-ttu-id="0a4a0-103">Tutorial: integração do Active Directory do Azure com o Tidemark</span><span class="sxs-lookup"><span data-stu-id="0a4a0-103">Tutorial: Azure Active Directory integration with Tidemark</span></span>

<span data-ttu-id="0a4a0-104">Neste tutorial, você aprenderá como toointegrate Tidemark com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="0a4a0-104">In this tutorial, you learn how toointegrate Tidemark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a4a0-105">Integrando Tidemark com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a4a0-105">Integrating Tidemark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0a4a0-106">Você pode controlar no AD do Azure que tenha acesso tooTidemark</span><span class="sxs-lookup"><span data-stu-id="0a4a0-106">You can control in Azure AD who has access tooTidemark</span></span>
- <span data-ttu-id="0a4a0-107">Você pode habilitar seu usuários tooautomatically get conectado tooTidemark (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0a4a0-107">You can enable your users tooautomatically get signed-on tooTidemark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a4a0-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0a4a0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0a4a0-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a4a0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a4a0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0a4a0-110">Prerequisites</span></span>

<span data-ttu-id="0a4a0-111">tooconfigure integração do AD do Azure com Tidemark, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a4a0-111">tooconfigure Azure AD integration with Tidemark, you need hello following items:</span></span>

- <span data-ttu-id="0a4a0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0a4a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a4a0-113">Uma assinatura do Tidemark habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="0a4a0-113">A Tidemark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a4a0-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a4a0-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0a4a0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a4a0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a4a0-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a4a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a4a0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0a4a0-118">Scenario description</span></span>
<span data-ttu-id="0a4a0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a4a0-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="0a4a0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a4a0-121">Adicionando Tidemark da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0a4a0-121">Adding Tidemark from hello gallery</span></span>
2. <span data-ttu-id="0a4a0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0a4a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tidemark-from-hello-gallery"></a><span data-ttu-id="0a4a0-123">Adicionando Tidemark da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0a4a0-123">Adding Tidemark from hello gallery</span></span>
<span data-ttu-id="0a4a0-124">integração de saudação tooconfigure de Tidemark no AD do Azure, você precisa tooadd Tidemark da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-124">tooconfigure hello integration of Tidemark into Azure AD, you need tooadd Tidemark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0a4a0-125">**tooadd Tidemark da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0a4a0-125">**tooadd Tidemark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a4a0-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0a4a0-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0a4a0-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="0a4a0-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="0a4a0-133">Na caixa de pesquisa hello, digite **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-133">In hello search box, type **Tidemark**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_search.png)

5. <span data-ttu-id="0a4a0-135">No painel de resultados de saudação, selecione **Tidemark**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-135">In hello results panel, select **Tidemark**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a4a0-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0a4a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a4a0-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Tidemark, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="0a4a0-138">In this section, you configure and test Azure AD single sign-on with Tidemark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0a4a0-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Tidemark é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tidemark is tooa user in Azure AD.</span></span> <span data-ttu-id="0a4a0-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Tidemark precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-140">In other words, a link relationship between an Azure AD user and hello related user in Tidemark needs toobe established.</span></span>

<span data-ttu-id="0a4a0-141">Tidemark, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-141">In Tidemark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0a4a0-142">tooconfigure e teste de logon único do AD do Azure com Tidemark, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a4a0-142">tooconfigure and test Azure AD single sign-on with Tidemark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0a4a0-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0a4a0-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a4a0-145">**[Criar um usuário de teste Tidemark](#creating-a-tidemark-test-user)**  -toohave um equivalente do Britta Simon em Tidemark é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-145">**[Creating a Tidemark test user](#creating-a-tidemark-test-user)** - toohave a counterpart of Britta Simon in Tidemark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a4a0-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a4a0-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a4a0-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a4a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a4a0-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Tidemark.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tidemark application.</span></span>

<span data-ttu-id="0a4a0-150">**tooconfigure AD do Azure-logon único com Tidemark, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0a4a0-150">**tooconfigure Azure AD single sign-on with Tidemark, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a4a0-151">Em Olá portal do Azure, Olá **Tidemark** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-151">In hello Azure portal, on hello **Tidemark** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="0a4a0-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_samlbase.png)

3. <span data-ttu-id="0a4a0-155">Em Olá **Tidemark domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a4a0-155">On hello **Tidemark Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_url.png)

    <span data-ttu-id="0a4a0-157">a.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-157">a.</span></span> <span data-ttu-id="0a4a0-158">Em Olá **URL de logon** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="0a4a0-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/login` |
    | `https://<subdomain>.tidemark.net/login` |

    <span data-ttu-id="0a4a0-159">b.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-159">b.</span></span> <span data-ttu-id="0a4a0-160">Em Olá **identificador** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="0a4a0-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/saml` |
    | `https://<subdomain>.tidemark.net/saml` |

    > [!NOTE] 
    > <span data-ttu-id="0a4a0-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-161">These values are not real.</span></span> <span data-ttu-id="0a4a0-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0a4a0-163">Entre em contato com [equipe de suporte do cliente Tidemark](http://www.tidemark.com/contact-us) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-163">Contact [Tidemark Client support team](http://www.tidemark.com/contact-us) tooget these values.</span></span> 
 
4. <span data-ttu-id="0a4a0-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_certificate.png) 

5. <span data-ttu-id="0a4a0-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0a4a0-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tidemark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0a4a0-168">Em Olá **Tidemark configuração** seção, clique em **configurar Tidemark** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-168">On hello **Tidemark Configuration** section, click **Configure Tidemark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0a4a0-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="0a4a0-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_configure.png) 

7. <span data-ttu-id="0a4a0-171">tooconfigure logon único no **Tidemark** lado, você precisa toosend Olá baixado **Certificate(Base64), ID de entidade de SAML, URL de logout e Single Sign-On URL do serviço SAML** muito[Tidemark equipe de suporte](http://www.tidemark.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="0a4a0-171">tooconfigure single sign-on on **Tidemark** side, you need toosend hello downloaded **Certificate(Base64), SAML Entity ID, Sign-Out URL and SAML Single Sign-On Service URL** too[Tidemark support team](http://www.tidemark.com/contact-us).</span></span> <span data-ttu-id="0a4a0-172">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0a4a0-173">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="0a4a0-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0a4a0-174">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0a4a0-175">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a4a0-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a4a0-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0a4a0-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a4a0-177">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="0a4a0-179">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0a4a0-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a4a0-180">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tidemark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a4a0-182">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tidemark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a4a0-184">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tidemark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a4a0-186">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a4a0-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tidemark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a4a0-188">a.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-188">a.</span></span> <span data-ttu-id="0a4a0-189">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a4a0-190">b.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-190">b.</span></span> <span data-ttu-id="0a4a0-191">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a4a0-192">c.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-192">c.</span></span> <span data-ttu-id="0a4a0-193">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0a4a0-194">d.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-194">d.</span></span> <span data-ttu-id="0a4a0-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-195">Click **Create**.</span></span>
 
### <a name="creating-a-tidemark-test-user"></a><span data-ttu-id="0a4a0-196">Criar um usuário de teste do Tidemark</span><span class="sxs-lookup"><span data-stu-id="0a4a0-196">Creating a Tidemark test user</span></span>

<span data-ttu-id="0a4a0-197">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Tidemark.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-197">hello objective of this section is toocreate a user called Britta Simon in Tidemark.</span></span> <span data-ttu-id="0a4a0-198">Trabalhe com [a equipe de suporte Tidemark](http://www.tidemark.com/contact-us) tooadd usuários Olá Olá conta Tidemark.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-198">Please work with [Tidemark support team](http://www.tidemark.com/contact-us) tooadd hello users in hello Tidemark account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0a4a0-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0a4a0-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0a4a0-200">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTidemark.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTidemark.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="0a4a0-202">**tooassign Britta Simon tooTidemark, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0a4a0-202">**tooassign Britta Simon tooTidemark, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a4a0-203">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0a4a0-205">Na lista de aplicativos hello, selecione **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-205">In hello applications list, select **Tidemark**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_app.png) 

3. <span data-ttu-id="0a4a0-207">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="0a4a0-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-209">Click **Add** button.</span></span> <span data-ttu-id="0a4a0-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="0a4a0-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0a4a0-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a4a0-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a4a0-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="0a4a0-215">Testing single sign-on</span></span>

<span data-ttu-id="0a4a0-216">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0a4a0-217">Quando você clica em bloco Tidemark Olá Olá painel de acesso, você deve obter o aplicativo de Tidemark tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="0a4a0-217">When you click hello Tidemark tile in hello Access Panel, you should get automatically signed-on tooyour Tidemark application.</span></span>
<span data-ttu-id="0a4a0-218">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0a4a0-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a4a0-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0a4a0-219">Additional resources</span></span>

* [<span data-ttu-id="0a4a0-220">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0a4a0-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a4a0-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a4a0-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_203.png

