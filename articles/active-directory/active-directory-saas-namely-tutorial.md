---
title: "Tutorial: integração do Azure Active Directory ao Namely | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e como."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0477ca6fa52a21abea7de458f8a99a01e8c25c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="2f425-103">Tutorial: Integração do Active Directory do Azure com o Namely</span><span class="sxs-lookup"><span data-stu-id="2f425-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="2f425-104">Neste tutorial, você aprenderá como toointegrate, ou seja, com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="2f425-104">In this tutorial, you learn how toointegrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f425-105">Ou seja, integração com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f425-105">Integrating Namely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2f425-106">Você pode controlar no AD do Azure que tenha acesso tooNamely</span><span class="sxs-lookup"><span data-stu-id="2f425-106">You can control in Azure AD who has access tooNamely</span></span>
- <span data-ttu-id="2f425-107">Você pode habilitar seu usuários tooautomatically get conectado tooNamely (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f425-107">You can enable your users tooautomatically get signed-on tooNamely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f425-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2f425-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2f425-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f425-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f425-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2f425-110">Prerequisites</span></span>

<span data-ttu-id="2f425-111">integração tooconfigure AD do Azure com, ou seja, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f425-111">tooconfigure Azure AD integration with Namely, you need hello following items:</span></span>

- <span data-ttu-id="2f425-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f425-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f425-113">Uma assinatura habilitada para logon único do Namely</span><span class="sxs-lookup"><span data-stu-id="2f425-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f425-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2f425-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f425-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2f425-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f425-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2f425-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f425-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f425-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f425-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2f425-118">Scenario description</span></span>
<span data-ttu-id="2f425-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2f425-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f425-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="2f425-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f425-121">Ou seja, adicionar da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="2f425-121">Adding Namely from hello gallery</span></span>
2. <span data-ttu-id="2f425-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f425-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-hello-gallery"></a><span data-ttu-id="2f425-123">Ou seja, adicionar da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="2f425-123">Adding Namely from hello gallery</span></span>
<span data-ttu-id="2f425-124">integração de saudação tooconfigure do especificamente no AD do Azure, você precisa tooadd nomeada da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="2f425-124">tooconfigure hello integration of Namely into Azure AD, you need tooadd Namely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2f425-125">**tooadd nomeada da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f425-125">**tooadd Namely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f425-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="2f425-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f425-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2f425-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2f425-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2f425-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="2f425-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f425-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="2f425-133">Na caixa de pesquisa hello, digite **como**.</span><span class="sxs-lookup"><span data-stu-id="2f425-133">In hello search box, type **Namely**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="2f425-135">No painel de resultados de saudação, selecione **especificamente**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2f425-135">In hello results panel, select **Namely**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f425-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f425-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f425-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Namely, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="2f425-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f425-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ou seja, é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f425-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Namely is tooa user in Azure AD.</span></span> <span data-ttu-id="2f425-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em especificamente precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="2f425-140">In other words, a link relationship between an Azure AD user and hello related user in Namely needs toobe established.</span></span>

<span data-ttu-id="2f425-141">Isto é, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f425-141">In Namely, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2f425-142">tooconfigure e teste de logon único do AD do Azure com, ou seja, você precisam Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f425-142">tooconfigure and test Azure AD single sign-on with Namely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2f425-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2f425-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2f425-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f425-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f425-145">**[Criar um usuário de teste, ou seja](#creating-a-namely-test-user)**  -toohave um equivalente de Britta Simon em saber que é vinculado toohello representação do AD do Azure do usuário.</span><span class="sxs-lookup"><span data-stu-id="2f425-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - toohave a counterpart of Britta Simon in Namely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f425-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="2f425-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f425-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="2f425-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f425-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f425-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f425-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu aplicativo, ou seja.</span><span class="sxs-lookup"><span data-stu-id="2f425-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="2f425-150">**tooconfigure AD do Azure-logon único com, ou seja, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f425-150">**tooconfigure Azure AD single sign-on with Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f425-151">Em Olá portal do Azure, Olá **especificamente** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="2f425-151">In hello Azure portal, on hello **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="2f425-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="2f425-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="2f425-155">Em Olá **, ou seja, domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f425-155">On hello **Namely Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="2f425-157">a.</span><span class="sxs-lookup"><span data-stu-id="2f425-157">a.</span></span> <span data-ttu-id="2f425-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="2f425-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="2f425-159">b.</span><span class="sxs-lookup"><span data-stu-id="2f425-159">b.</span></span> <span data-ttu-id="2f425-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="2f425-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2f425-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="2f425-161">These values are not real.</span></span> <span data-ttu-id="2f425-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="2f425-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2f425-163">Entre em contato com [a equipe de suporte como cliente](https://www.namely.com/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="2f425-163">Contact [Namely Client support team](https://www.namely.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="2f425-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="2f425-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="2f425-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="2f425-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2f425-168">Em Olá **ou seja, a configuração** seção, clique em **configurar isto é** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="2f425-168">On hello **Namely Configuration** section, click **Configure Namely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2f425-169">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="2f425-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="2f425-171">Em outra janela do navegador, conecte-se tooyour ou seja, o site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="2f425-171">In another browser window, sign on tooyour Namely company site as an administrator.</span></span>

8. <span data-ttu-id="2f425-172">Na barra de ferramentas de saudação na parte superior do hello, clique em **empresa**.</span><span class="sxs-lookup"><span data-stu-id="2f425-172">In hello toolbar on hello top, click **Company**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="2f425-174">Clique em Olá **configurações** guia.</span><span class="sxs-lookup"><span data-stu-id="2f425-174">Click hello **Settings** tab.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="2f425-176">Clique em **SAML**.</span><span class="sxs-lookup"><span data-stu-id="2f425-176">Click **SAML**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="2f425-178">Em Olá **configurações SAML** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f425-178">On hello **SAML Settings** page, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="2f425-180">a.</span><span class="sxs-lookup"><span data-stu-id="2f425-180">a.</span></span> <span data-ttu-id="2f425-181">Clique em **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="2f425-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="2f425-182">b.</span><span class="sxs-lookup"><span data-stu-id="2f425-182">b.</span></span> <span data-ttu-id="2f425-183">Em Olá **url SSO do provedor de identidade** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f425-183">In hello **Identity provider SSO url** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="2f425-184">c.</span><span class="sxs-lookup"><span data-stu-id="2f425-184">c.</span></span> <span data-ttu-id="2f425-185">Abra seu certificado baixado no bloco de notas, Olá de cópia de conteúdo e, em seguida, cole-o em Olá **certificado do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2f425-185">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="2f425-186">d.</span><span class="sxs-lookup"><span data-stu-id="2f425-186">d.</span></span> <span data-ttu-id="2f425-187">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2f425-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2f425-188">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="2f425-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2f425-189">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="2f425-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2f425-190">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f425-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f425-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f425-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f425-192">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f425-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="2f425-194">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f425-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f425-195">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="2f425-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f425-197">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="2f425-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f425-199">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f425-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f425-201">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f425-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f425-203">a.</span><span class="sxs-lookup"><span data-stu-id="2f425-203">a.</span></span> <span data-ttu-id="2f425-204">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f425-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f425-205">b.</span><span class="sxs-lookup"><span data-stu-id="2f425-205">b.</span></span> <span data-ttu-id="2f425-206">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2f425-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f425-207">c.</span><span class="sxs-lookup"><span data-stu-id="2f425-207">c.</span></span> <span data-ttu-id="2f425-208">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="2f425-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2f425-209">d.</span><span class="sxs-lookup"><span data-stu-id="2f425-209">d.</span></span> <span data-ttu-id="2f425-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2f425-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="2f425-211">Criando um usuário de teste do Namely</span><span class="sxs-lookup"><span data-stu-id="2f425-211">Creating a Namely test user</span></span>

<span data-ttu-id="2f425-212">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon em saber.</span><span class="sxs-lookup"><span data-stu-id="2f425-212">hello objective of this section is toocreate a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="2f425-213">**toocreate um usuário chamado Britta Simon no, ou seja, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f425-213">**toocreate a user called Britta Simon in Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f425-214">Ou seja, o tooyour logon da empresa site como um administrador.</span><span class="sxs-lookup"><span data-stu-id="2f425-214">Sign-on tooyour Namely company site as an administrator.</span></span>

2. <span data-ttu-id="2f425-215">Na barra de ferramentas de saudação na parte superior do hello, clique em **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="2f425-215">In hello toolbar on hello top, click **People**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="2f425-217">Clique em Olá **diretório** guia.</span><span class="sxs-lookup"><span data-stu-id="2f425-217">Click hello **Directory** tab.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="2f425-219">Clique em **Adicionar Nova Pessoa**.</span><span class="sxs-lookup"><span data-stu-id="2f425-219">Click **Add New Person**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="2f425-221">Em Olá **adicionar nova pessoa** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f425-221">On hello **Add New Person** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="2f425-222">a.</span><span class="sxs-lookup"><span data-stu-id="2f425-222">a.</span></span> <span data-ttu-id="2f425-223">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2f425-223">In hello **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="2f425-224">b.</span><span class="sxs-lookup"><span data-stu-id="2f425-224">b.</span></span> <span data-ttu-id="2f425-225">Em Olá **Sobrenome** caixa de texto, tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2f425-225">In hello **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="2f425-226">c.</span><span class="sxs-lookup"><span data-stu-id="2f425-226">c.</span></span> <span data-ttu-id="2f425-227">Em Olá **Email** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2f425-227">In hello **Email** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f425-228">d.</span><span class="sxs-lookup"><span data-stu-id="2f425-228">d.</span></span> <span data-ttu-id="2f425-229">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2f425-229">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2f425-230">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2f425-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2f425-231">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooNamely.</span><span class="sxs-lookup"><span data-stu-id="2f425-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNamely.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="2f425-233">**tooassign Britta Simon tooNamely, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2f425-233">**tooassign Britta Simon tooNamely, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f425-234">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2f425-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2f425-236">Na lista de aplicativos hello, selecione **como**.</span><span class="sxs-lookup"><span data-stu-id="2f425-236">In hello applications list, select **Namely**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="2f425-238">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2f425-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="2f425-240">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2f425-240">Click **Add** button.</span></span> <span data-ttu-id="2f425-241">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f425-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="2f425-243">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f425-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2f425-244">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f425-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f425-245">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2f425-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f425-246">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="2f425-246">Testing single sign-on</span></span>

<span data-ttu-id="2f425-247">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="2f425-247">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="2f425-248">Quando você clica em Olá bloco ou seja, no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo, ou seja</span><span class="sxs-lookup"><span data-stu-id="2f425-248">When you click hello Namely tile in hello Access Panel, you should get automatically signed-on tooyour Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f425-249">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2f425-249">Additional resources</span></span>

* [<span data-ttu-id="2f425-250">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2f425-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f425-251">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2f425-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

