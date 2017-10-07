---
title: "Tutorial: integração do Azure Active Directory ao Predictix Price Reporting | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Predictix preço Reporting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 691d0c43-3aa1-4220-9e46-e7a88db234ad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: c2ba85f613f5a71de72278a0d1916c135b835b60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-price-reporting"></a><span data-ttu-id="4ea49-103">Tutorial: integração do Azure Active Directory ao Predictix Price Reporting</span><span class="sxs-lookup"><span data-stu-id="4ea49-103">Tutorial: Azure Active Directory integration with Predictix Price Reporting</span></span>

<span data-ttu-id="4ea49-104">Neste tutorial, você aprenderá como toointegrate Predictix preço Reporting com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="4ea49-104">In this tutorial, you learn how toointegrate Predictix Price Reporting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4ea49-105">Integrar Predictix preço Reporting com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ea49-105">Integrating Predictix Price Reporting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4ea49-106">Você pode controlar no AD do Azure que tenha acesso tooPredictix preço Reporting.</span><span class="sxs-lookup"><span data-stu-id="4ea49-106">You can control in Azure AD who has access tooPredictix Price Reporting.</span></span>
- <span data-ttu-id="4ea49-107">Você pode habilitar seu usuários tooautomatically get conectado tooPredictix preço Reporting (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ea49-107">You can enable your users tooautomatically get signed-on tooPredictix Price Reporting (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4ea49-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ea49-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="4ea49-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4ea49-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ea49-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4ea49-110">Prerequisites</span></span>

<span data-ttu-id="4ea49-111">tooconfigure integração do AD do Azure com Predictix preço Reporting, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ea49-111">tooconfigure Azure AD integration with Predictix Price Reporting, you need hello following items:</span></span>

- <span data-ttu-id="4ea49-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4ea49-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4ea49-113">Uma assinatura do Predictix Price Reporting habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="4ea49-113">A Predictix Price Reporting single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4ea49-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4ea49-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4ea49-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4ea49-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4ea49-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4ea49-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4ea49-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ea49-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4ea49-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4ea49-118">Scenario description</span></span>
<span data-ttu-id="4ea49-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4ea49-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4ea49-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="4ea49-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4ea49-121">Adicionando Predictix preço relatórios da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4ea49-121">Adding Predictix Price Reporting from hello gallery</span></span>
2. <span data-ttu-id="4ea49-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4ea49-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-price-reporting-from-hello-gallery"></a><span data-ttu-id="4ea49-123">Adicionando Predictix preço relatórios da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4ea49-123">Adding Predictix Price Reporting from hello gallery</span></span>
<span data-ttu-id="4ea49-124">integração de saudação tooconfigure do Predictix preço Reporting no Azure AD, é necessário tooadd Predictix Reporting de preço da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4ea49-124">tooconfigure hello integration of Predictix Price Reporting into Azure AD, you need tooadd Predictix Price Reporting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4ea49-125">**tooadd Predictix preço relatórios da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4ea49-125">**tooadd Predictix Price Reporting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ea49-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4ea49-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="4ea49-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4ea49-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4ea49-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4ea49-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="4ea49-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4ea49-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="4ea49-133">Na caixa de pesquisa hello, digite **Predictix preço Reporting**, selecione **Predictix preço Reporting** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4ea49-133">In hello search box, type **Predictix Price Reporting**, select **Predictix Price Reporting** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Preço de Predictix relatórios na lista de resultados de saudação](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4ea49-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ea49-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4ea49-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Predictix Price Reporting, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="4ea49-136">In this section, you configure and test Azure AD single sign-on with Predictix Price Reporting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4ea49-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá nos relatórios de preço Predictix é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ea49-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Predictix Price Reporting is tooa user in Azure AD.</span></span> <span data-ttu-id="4ea49-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação nos relatórios de preço Predictix precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4ea49-138">In other words, a link relationship between an Azure AD user and hello related user in Predictix Price Reporting needs toobe established.</span></span>

<span data-ttu-id="4ea49-139">Nos relatórios de preço Predictix, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ea49-139">In Predictix Price Reporting, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4ea49-140">tooconfigure e teste de logon único do AD do Azure com Predictix preço Reporting, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ea49-140">tooconfigure and test Azure AD single sign-on with Predictix Price Reporting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4ea49-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4ea49-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4ea49-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4ea49-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4ea49-143">**[Criar um usuário de teste Predictix preço Reporting](#create-a-predictix-price-reporting-test-user)**  -toohave um equivalente do Britta Simon em Predictix preço relatórios que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="4ea49-143">**[Create a Predictix Price Reporting test user](#create-a-predictix-price-reporting-test-user)** - toohave a counterpart of Britta Simon in Predictix Price Reporting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4ea49-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="4ea49-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4ea49-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="4ea49-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4ea49-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ea49-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4ea49-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Predictix preço Reporting.</span><span class="sxs-lookup"><span data-stu-id="4ea49-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Predictix Price Reporting application.</span></span>

<span data-ttu-id="4ea49-148">**tooconfigure logon único do AD do Azure com o relatório de preço Predictix, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4ea49-148">**tooconfigure Azure AD single sign-on with Predictix Price Reporting, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ea49-149">Em Olá portal do Azure, Olá **Predictix preço Reporting** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="4ea49-149">In hello Azure portal, on hello **Predictix Price Reporting** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="4ea49-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="4ea49-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_samlbase.png)

3. <span data-ttu-id="4ea49-153">Em Olá **Predictix preço Reporting domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ea49-153">On hello **Predictix Price Reporting Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Predictix Price Reporting](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_url.png)

    <span data-ttu-id="4ea49-155">a.</span><span class="sxs-lookup"><span data-stu-id="4ea49-155">a.</span></span> <span data-ttu-id="4ea49-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname-pricing>.predictix.com/sso/request`</span><span class="sxs-lookup"><span data-stu-id="4ea49-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname-pricing>.predictix.com/sso/request`</span></span>

    <span data-ttu-id="4ea49-157">b.</span><span class="sxs-lookup"><span data-stu-id="4ea49-157">b.</span></span> <span data-ttu-id="4ea49-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ea49-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname-pricing>.predictix.com` |
    | `https://<companyname-pricing>.dev.predictix.com` |

    > [!NOTE] 
    > <span data-ttu-id="4ea49-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4ea49-159">These values are not real.</span></span> <span data-ttu-id="4ea49-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="4ea49-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4ea49-161">Entre em contato com [equipe de suporte do cliente de relatório de preço de Predictix](http://www.infor.com/company/customer-center/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="4ea49-161">Contact [Predictix Price Reporting Client support team](http://www.infor.com/company/customer-center/) tooget these values.</span></span> 
 
4. <span data-ttu-id="4ea49-162">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4ea49-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_certificate.png) 

5. <span data-ttu-id="4ea49-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4ea49-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4ea49-166">Em Olá **Predictix preço de configuração do Reporting** seção, clique em **Configurar relatório de preço Predictix** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="4ea49-166">On hello **Predictix Price Reporting Configuration** section, click **Configure Predictix Price Reporting** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4ea49-167">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="4ea49-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Predictix Price Reporting](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_configure.png) 

7. <span data-ttu-id="4ea49-169">tooconfigure logon único no **Predictix preço Reporting** lado, você precisa toosend Olá baixado **certificado (Base64)**, **URL de logout, ID de entidade de SAML e logon único SAML URL do serviço** muito[Predictix preço Reporting a equipe de suporte](http://www.infor.com/company/customer-center/).</span><span class="sxs-lookup"><span data-stu-id="4ea49-169">tooconfigure single sign-on on **Predictix Price Reporting** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Predictix Price Reporting support team](http://www.infor.com/company/customer-center/).</span></span> <span data-ttu-id="4ea49-170">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="4ea49-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4ea49-171">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="4ea49-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4ea49-172">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="4ea49-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4ea49-173">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4ea49-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4ea49-174">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ea49-174">Create an Azure AD test user</span></span>

<span data-ttu-id="4ea49-175">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ea49-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="4ea49-177">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4ea49-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ea49-178">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="4ea49-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4ea49-180">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="4ea49-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4ea49-182">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4ea49-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4ea49-184">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ea49-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4ea49-186">a.</span><span class="sxs-lookup"><span data-stu-id="4ea49-186">a.</span></span> <span data-ttu-id="4ea49-187">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4ea49-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4ea49-188">b.</span><span class="sxs-lookup"><span data-stu-id="4ea49-188">b.</span></span> <span data-ttu-id="4ea49-189">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4ea49-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="4ea49-190">c.</span><span class="sxs-lookup"><span data-stu-id="4ea49-190">c.</span></span> <span data-ttu-id="4ea49-191">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="4ea49-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="4ea49-192">d.</span><span class="sxs-lookup"><span data-stu-id="4ea49-192">d.</span></span> <span data-ttu-id="4ea49-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4ea49-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-price-reporting-test-user"></a><span data-ttu-id="4ea49-194">Criar um usuário de teste do Predictix Price Reporting</span><span class="sxs-lookup"><span data-stu-id="4ea49-194">Create a Predictix Price Reporting test user</span></span>

<span data-ttu-id="4ea49-195">Nesta seção, você criará um usuário chamado Britta Simon no Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="4ea49-195">In this section, you create a user called Britta Simon in Predictix Price Reporting.</span></span> <span data-ttu-id="4ea49-196">Trabalhar com [Predictix preço Reporting a equipe de suporte](http://www.infor.com/company/customer-center/) tooadd usuários de saudação na plataforma de relatórios de preço Predictix hello.</span><span class="sxs-lookup"><span data-stu-id="4ea49-196">Work with [Predictix Price Reporting support team](http://www.infor.com/company/customer-center/) tooadd hello users in hello Predictix Price Reporting platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4ea49-197">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4ea49-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4ea49-198">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPredictix preço Reporting.</span><span class="sxs-lookup"><span data-stu-id="4ea49-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPredictix Price Reporting.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="4ea49-200">**tooassign tooPredictix Britta Simon preço Reporting, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4ea49-200">**tooassign Britta Simon tooPredictix Price Reporting, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ea49-201">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4ea49-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4ea49-203">Na lista de aplicativos hello, selecione **Predictix preço Reporting**.</span><span class="sxs-lookup"><span data-stu-id="4ea49-203">In hello applications list, select **Predictix Price Reporting**.</span></span>

    ![link de Predictix preço Reporting Olá na lista de aplicativos Olá](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_app.png)  

3. <span data-ttu-id="4ea49-205">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4ea49-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="4ea49-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4ea49-207">Click **Add** button.</span></span> <span data-ttu-id="4ea49-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4ea49-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="4ea49-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ea49-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4ea49-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4ea49-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4ea49-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4ea49-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4ea49-213">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="4ea49-213">Test single sign-on</span></span>

<span data-ttu-id="4ea49-214">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ea49-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4ea49-215">Quando você clica em Olá Predictix preço Reporting lado a lado no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Predictix preço Reporting aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4ea49-215">When you click hello Predictix Price Reporting tile in hello Access Panel, you should get automatically signed-on tooyour Predictix Price Reporting application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4ea49-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4ea49-216">Additional resources</span></span>

* [<span data-ttu-id="4ea49-217">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4ea49-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4ea49-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4ea49-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_203.png

