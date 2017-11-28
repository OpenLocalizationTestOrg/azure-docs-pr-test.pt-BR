---
title: "Tutorial: integração do Azure Active Directory ao PerformanceCentre | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e PerformanceCentre."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 19781c0087093a67c70dc90072cf1a119bb2ade0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="0bb1b-103">Tutorial: Integração do Active Directory do Azure com o PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="0bb1b-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="0bb1b-104">Neste tutorial, você aprenderá como toointegrate PerformanceCentre com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="0bb1b-104">In this tutorial, you learn how toointegrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0bb1b-105">Integrando PerformanceCentre com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="0bb1b-105">Integrating PerformanceCentre with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0bb1b-106">Você pode controlar no AD do Azure que tenha acesso tooPerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="0bb1b-106">You can control in Azure AD who has access tooPerformanceCentre</span></span>
- <span data-ttu-id="0bb1b-107">Você pode habilitar seu usuários tooautomatically get conectado tooPerformanceCentre (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0bb1b-107">You can enable your users tooautomatically get signed-on tooPerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0bb1b-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0bb1b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0bb1b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0bb1b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bb1b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0bb1b-110">Prerequisites</span></span>

<span data-ttu-id="0bb1b-111">tooconfigure integração do AD do Azure com PerformanceCentre, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="0bb1b-111">tooconfigure Azure AD integration with PerformanceCentre, you need hello following items:</span></span>

- <span data-ttu-id="0bb1b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0bb1b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0bb1b-113">Uma assinatura do PerformanceCentre com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="0bb1b-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0bb1b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0bb1b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0bb1b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0bb1b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0bb1b-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0bb1b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0bb1b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0bb1b-118">Scenario description</span></span>
<span data-ttu-id="0bb1b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0bb1b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="0bb1b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0bb1b-121">Adicionando PerformanceCentre da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0bb1b-121">Adding PerformanceCentre from hello gallery</span></span>
2. <span data-ttu-id="0bb1b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0bb1b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-hello-gallery"></a><span data-ttu-id="0bb1b-123">Adicionando PerformanceCentre da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0bb1b-123">Adding PerformanceCentre from hello gallery</span></span>
<span data-ttu-id="0bb1b-124">integração de saudação tooconfigure de PerformanceCentre no AD do Azure, você precisa tooadd PerformanceCentre da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-124">tooconfigure hello integration of PerformanceCentre into Azure AD, you need tooadd PerformanceCentre from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0bb1b-125">**tooadd PerformanceCentre da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0bb1b-125">**tooadd PerformanceCentre from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bb1b-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0bb1b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0bb1b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="0bb1b-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="0bb1b-133">Na caixa de pesquisa hello, digite **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-133">In hello search box, type **PerformanceCentre**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="0bb1b-135">No painel de resultados de saudação, selecione **PerformanceCentre**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-135">In hello results panel, select **PerformanceCentre**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0bb1b-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0bb1b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0bb1b-138">Nesta seção, você configurará e testará o logon único do Azure AD com o PerformanceCentre, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0bb1b-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em PerformanceCentre é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PerformanceCentre is tooa user in Azure AD.</span></span> <span data-ttu-id="0bb1b-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em PerformanceCentre precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-140">In other words, a link relationship between an Azure AD user and hello related user in PerformanceCentre needs toobe established.</span></span>

<span data-ttu-id="0bb1b-141">PerformanceCentre, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-141">In PerformanceCentre, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0bb1b-142">tooconfigure e teste de logon único do AD do Azure com PerformanceCentre, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="0bb1b-142">tooconfigure and test Azure AD single sign-on with PerformanceCentre, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0bb1b-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0bb1b-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0bb1b-145">**[Criar um usuário de teste PerformanceCentre](#creating-a-performancecentre-test-user)**  -toohave um equivalente do Britta Simon em PerformanceCentre é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - toohave a counterpart of Britta Simon in PerformanceCentre that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0bb1b-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0bb1b-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0bb1b-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bb1b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0bb1b-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="0bb1b-150">**tooconfigure AD do Azure-logon único com PerformanceCentre, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0bb1b-150">**tooconfigure Azure AD single sign-on with PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bb1b-151">Em Olá portal do Azure, Olá **PerformanceCentre** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-151">In hello Azure portal, on hello **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="0bb1b-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="0bb1b-155">Em Olá **PerformanceCentre domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0bb1b-155">On hello **PerformanceCentre Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="0bb1b-157">a.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-157">a.</span></span> <span data-ttu-id="0bb1b-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="0bb1b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="0bb1b-159">b.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-159">b.</span></span> <span data-ttu-id="0bb1b-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="0bb1b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0bb1b-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-161">These values are not real.</span></span> <span data-ttu-id="0bb1b-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0bb1b-163">Entre em contato com [equipe de suporte do cliente PerformanceCentre](https://www.performancecentre.com/contact-us/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) tooget these values.</span></span> 

4. <span data-ttu-id="0bb1b-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="0bb1b-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0bb1b-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0bb1b-168">Em Olá **PerformanceCentre configuração** seção, clique em **configurar PerformanceCentre** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-168">On hello **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0bb1b-169">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="0bb1b-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="0bb1b-171">Logon tooyour **PerformanceCentre** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-171">Sign-on tooyour **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="0bb1b-172">Na guia Olá no lado esquerdo do hello, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-172">In hello tab on hello left side, click **Configure**.</span></span>
   
    ![Logon Único do AD do Azure][10]

9. <span data-ttu-id="0bb1b-174">Na guia Olá no lado esquerdo do hello, clique em **diversos**e, em seguida, clique em **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-174">In hello tab on hello left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Logon Único do AD do Azure][11]

10. <span data-ttu-id="0bb1b-176">Para o **Protocolo**, escolha **SAML**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Logon Único do AD do Azure][12]

11. <span data-ttu-id="0bb1b-178">Abra o arquivo de metadados baixado no bloco de notas, copie Olá conteúdo, cole-o em Olá **metadados do provedor de identidade** caixa de texto e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-178">Open your downloaded metadata file in notepad, copy hello content, paste it into hello **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Logon Único do AD do Azure][13]

12. <span data-ttu-id="0bb1b-180">Verifique se que valores Olá Olá **URL de base de dados de entidade** e **URL de ID de entidade** estão corretas.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-180">Verify that hello values for hello **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Logon Único do AD do Azure][14]

> [!TIP]
> <span data-ttu-id="0bb1b-182">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="0bb1b-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0bb1b-183">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0bb1b-184">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0bb1b-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0bb1b-185">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0bb1b-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="0bb1b-186">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="0bb1b-188">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0bb1b-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bb1b-189">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0bb1b-191">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0bb1b-193">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0bb1b-195">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0bb1b-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0bb1b-197">a.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-197">a.</span></span> <span data-ttu-id="0bb1b-198">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0bb1b-199">b.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-199">b.</span></span> <span data-ttu-id="0bb1b-200">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0bb1b-201">c.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-201">c.</span></span> <span data-ttu-id="0bb1b-202">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0bb1b-203">d.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-203">d.</span></span> <span data-ttu-id="0bb1b-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="0bb1b-205">Criar um usuário de teste do PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="0bb1b-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="0bb1b-206">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-206">hello objective of this section is toocreate a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="0bb1b-207">**toocreate um usuário chamado Britta Simon no PerformanceCentre, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0bb1b-207">**toocreate a user called Britta Simon in PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bb1b-208">Faça logon no tooyour PerformanceCentre site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-208">Sign on tooyour PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="0bb1b-209">No menu Olá Olá esquerda, clique em **Interrelate**e, em seguida, clique em **criar participante**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-209">In hello menu on hello left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Criar Usuário][400]

3. <span data-ttu-id="0bb1b-211">Em Olá **se inter-relacionam - criar o participante** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0bb1b-211">On hello **Interrelate - Create Participant** dialog, perform hello following steps:</span></span>
   
    ![Criar Usuário][401]
    
    <span data-ttu-id="0bb1b-213">a.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-213">a.</span></span> <span data-ttu-id="0bb1b-214">Saudação de tipo atributos necessários para Britta Simon nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-214">Type hello required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="0bb1b-215">Nome de usuário de Britta atributo PerformanceCentre deve ser Olá mesmo Olá nome de usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-215">Britta's User Name attribute in PerformanceCentre must be hello same as hello User Name in Azure AD.</span></span>
    
    <span data-ttu-id="0bb1b-216">b.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-216">b.</span></span> <span data-ttu-id="0bb1b-217">Selecione **Administrador Cliente** como **Escolher Função**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="0bb1b-218">c.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-218">c.</span></span> <span data-ttu-id="0bb1b-219">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-219">Click **Save**.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0bb1b-220">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0bb1b-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0bb1b-221">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerformanceCentre.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="0bb1b-223">**tooassign Britta Simon tooPerformanceCentre, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0bb1b-223">**tooassign Britta Simon tooPerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bb1b-224">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0bb1b-226">Na lista de aplicativos hello, selecione **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-226">In hello applications list, select **PerformanceCentre**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="0bb1b-228">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="0bb1b-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-230">Click **Add** button.</span></span> <span data-ttu-id="0bb1b-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="0bb1b-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0bb1b-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0bb1b-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0bb1b-236">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="0bb1b-236">Testing single sign-on</span></span>

<span data-ttu-id="0bb1b-237">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="0bb1b-238">Quando você clica em bloco PerformanceCentre Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour PerformanceCentre aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0bb1b-238">When you click hello PerformanceCentre tile in hello Access Panel, you should get automatically signed-on tooyour PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0bb1b-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0bb1b-239">Additional resources</span></span>

* [<span data-ttu-id="0bb1b-240">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0bb1b-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0bb1b-241">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0bb1b-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

