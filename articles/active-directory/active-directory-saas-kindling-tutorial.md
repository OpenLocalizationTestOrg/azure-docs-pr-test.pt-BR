---
title: "Tutorial: integração do Azure Active Directory com o Kindling | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Kindling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 32ad6116c2690aea2060a2dd56e052f233ad7ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="7cca2-103">Tutorial: integração do Active Directory do Azure com o Kindling</span><span class="sxs-lookup"><span data-stu-id="7cca2-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="7cca2-104">Neste tutorial, você aprenderá como toointegrate Kindling com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="7cca2-104">In this tutorial, you learn how toointegrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7cca2-105">Integrando Kindling com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="7cca2-105">Integrating Kindling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7cca2-106">Você pode controlar no AD do Azure que tenha acesso tooKindling</span><span class="sxs-lookup"><span data-stu-id="7cca2-106">You can control in Azure AD who has access tooKindling</span></span>
- <span data-ttu-id="7cca2-107">Você pode habilitar seu usuários tooautomatically get conectado tooKindling (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7cca2-107">You can enable your users tooautomatically get signed-on tooKindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7cca2-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7cca2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7cca2-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte.</span><span class="sxs-lookup"><span data-stu-id="7cca2-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="7cca2-110">[o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7cca2-110">[what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cca2-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7cca2-111">Prerequisites</span></span>

<span data-ttu-id="7cca2-112">integração de tooconfigure AD do Azure com Kindling, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="7cca2-112">tooconfigure Azure AD integration with Kindling, you need hello following items:</span></span>

- <span data-ttu-id="7cca2-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7cca2-113">An Azure AD subscription</span></span>
- <span data-ttu-id="7cca2-114">Uma assinatura habilitada para logon único do Kindling</span><span class="sxs-lookup"><span data-stu-id="7cca2-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7cca2-115">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7cca2-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7cca2-116">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7cca2-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7cca2-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7cca2-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7cca2-118">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7cca2-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7cca2-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7cca2-119">Scenario description</span></span>
<span data-ttu-id="7cca2-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7cca2-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7cca2-121">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="7cca2-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7cca2-122">Adicionando Kindling da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7cca2-122">Adding Kindling from hello gallery</span></span>
2. <span data-ttu-id="7cca2-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7cca2-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-hello-gallery"></a><span data-ttu-id="7cca2-124">Adicionando Kindling da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7cca2-124">Adding Kindling from hello gallery</span></span>
<span data-ttu-id="7cca2-125">integração de saudação do tooconfigure do Kindling no AD do Azure, você precisa tooadd Kindling da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7cca2-125">tooconfigure hello integration of Kindling into Azure AD, you need tooadd Kindling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7cca2-126">**tooadd Kindling da Galeria hello, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7cca2-126">**tooadd Kindling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7cca2-127">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7cca2-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7cca2-129">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7cca2-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7cca2-130">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7cca2-130">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7cca2-132">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7cca2-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7cca2-134">Na caixa de pesquisa hello, digite **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="7cca2-134">In hello search box, type **Kindling**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_search.png)

5. <span data-ttu-id="7cca2-136">No painel de resultados de saudação, selecione **Kindling**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7cca2-136">In hello results panel, select **Kindling**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7cca2-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7cca2-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7cca2-139">Nesta seção, você configurará e testará o logon único do Azure AD com o Kindling, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="7cca2-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7cca2-140">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Kindling é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7cca2-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kindling is tooa user in Azure AD.</span></span> <span data-ttu-id="7cca2-141">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Kindling necessidades toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7cca2-141">In other words, a link relationship between an Azure AD user and hello related user in Kindling needs toobe established.</span></span>

<span data-ttu-id="7cca2-142">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Kindling.</span><span class="sxs-lookup"><span data-stu-id="7cca2-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Kindling.</span></span>

<span data-ttu-id="7cca2-143">tooconfigure e teste de logon único do AD do Azure com Kindling, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="7cca2-143">tooconfigure and test Azure AD single sign-on with Kindling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7cca2-144">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7cca2-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7cca2-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7cca2-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7cca2-146">**[Criar um usuário de teste Kindling](#creating-a-kindling-test-user)**  -toohave um equivalente do Britta Simon em Kindling que é vinculado a representação toohello AD do Azure do usuário.</span><span class="sxs-lookup"><span data-stu-id="7cca2-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - toohave a counterpart of Britta Simon in Kindling that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7cca2-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="7cca2-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7cca2-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="7cca2-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7cca2-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7cca2-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7cca2-150">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Kindling.</span><span class="sxs-lookup"><span data-stu-id="7cca2-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="7cca2-151">**tooconfigure logon único do AD do Azure com Kindling, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7cca2-151">**tooconfigure Azure AD single sign-on with Kindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="7cca2-152">Em Olá portal do Azure, Olá **Kindling** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="7cca2-152">In hello Azure portal, on hello **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7cca2-154">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="7cca2-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_samlbase.png)

3. <span data-ttu-id="7cca2-156">Em Olá **Kindling domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7cca2-156">On hello **Kindling Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="7cca2-158">a.</span><span class="sxs-lookup"><span data-stu-id="7cca2-158">a.</span></span> <span data-ttu-id="7cca2-159">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="7cca2-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="7cca2-160">b.</span><span class="sxs-lookup"><span data-stu-id="7cca2-160">b.</span></span>  <span data-ttu-id="7cca2-161">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="7cca2-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7cca2-162">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="7cca2-162">These values are not hello real.</span></span> <span data-ttu-id="7cca2-163">Atualize esses valores com URL de logon real hello e o identificador.</span><span class="sxs-lookup"><span data-stu-id="7cca2-163">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="7cca2-164">Entre em contato com [Kindling a equipe de suporte](mailto:support@kindlingapp.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="7cca2-164">Contact [Kindling support team](mailto:support@kindlingapp.com) tooget these values.</span></span>
 
4. <span data-ttu-id="7cca2-165">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7cca2-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_certificate.png) 

5. <span data-ttu-id="7cca2-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7cca2-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kindling-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7cca2-169">Em Olá **Kindling configuração** seção, clique em **configurar Kindling** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="7cca2-169">On hello **Kindling Configuration** section, click **Configure Kindling** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7cca2-170">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="7cca2-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_configure.png) 

7. <span data-ttu-id="7cca2-172">tooconfigure logon único no **Kindling** lado, você precisa toosend Olá baixado **certificado (Base64)**, **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML**muito[a equipe de suporte Kindling](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="7cca2-172">tooconfigure single sign-on on **Kindling** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="7cca2-173">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="7cca2-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7cca2-174">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="7cca2-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7cca2-175">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7cca2-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7cca2-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7cca2-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="7cca2-177">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7cca2-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7cca2-179">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7cca2-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7cca2-180">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7cca2-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kindling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7cca2-182">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="7cca2-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kindling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7cca2-184">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7cca2-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7cca2-186">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7cca2-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7cca2-188">a.</span><span class="sxs-lookup"><span data-stu-id="7cca2-188">a.</span></span> <span data-ttu-id="7cca2-189">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7cca2-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7cca2-190">b.</span><span class="sxs-lookup"><span data-stu-id="7cca2-190">b.</span></span> <span data-ttu-id="7cca2-191">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7cca2-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7cca2-192">c.</span><span class="sxs-lookup"><span data-stu-id="7cca2-192">c.</span></span> <span data-ttu-id="7cca2-193">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="7cca2-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7cca2-194">d.</span><span class="sxs-lookup"><span data-stu-id="7cca2-194">d.</span></span> <span data-ttu-id="7cca2-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7cca2-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="7cca2-196">Criar um usuário de teste Kindling</span><span class="sxs-lookup"><span data-stu-id="7cca2-196">Creating a Kindling test user</span></span>

<span data-ttu-id="7cca2-197">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Kindling.</span><span class="sxs-lookup"><span data-stu-id="7cca2-197">hello objective of this section is toocreate a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="7cca2-198">O Kindling dá suporte ao provisionamento just-in-time.</span><span class="sxs-lookup"><span data-stu-id="7cca2-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="7cca2-199">Você já habilitou isso em [Configurar o logon único do AD do Azure](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="7cca2-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="7cca2-200">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="7cca2-200">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7cca2-201">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7cca2-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7cca2-202">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooKindling.</span><span class="sxs-lookup"><span data-stu-id="7cca2-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKindling.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7cca2-204">**tooassign Britta Simon tooKindling, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7cca2-204">**tooassign Britta Simon tooKindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="7cca2-205">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7cca2-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7cca2-207">Na lista de aplicativos hello, selecione **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="7cca2-207">In hello applications list, select **Kindling**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_app.png) 

3. <span data-ttu-id="7cca2-209">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7cca2-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7cca2-211">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7cca2-211">Click **Add** button.</span></span> <span data-ttu-id="7cca2-212">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7cca2-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7cca2-214">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="7cca2-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7cca2-215">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7cca2-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7cca2-216">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7cca2-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7cca2-217">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7cca2-217">Testing single sign-on</span></span>

<span data-ttu-id="7cca2-218">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="7cca2-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7cca2-219">Quando você clica em bloco Kindling Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Kindling aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7cca2-219">When you click hello Kindling tile in hello Access Panel, you should get automatically signed-on tooyour Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7cca2-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7cca2-220">Additional resources</span></span>

* [<span data-ttu-id="7cca2-221">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7cca2-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7cca2-222">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7cca2-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_203.png

