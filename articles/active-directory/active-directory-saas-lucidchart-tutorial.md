---
title: "Tutorial: Integração do Azure Active Directory com o Lucidchart | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Lucidchart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 774e5f423097650a3cae8e8ca13b2c65b8470736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="936cc-103">Tutorial: Integração do Active Directory do Azure com o Lucidchart</span><span class="sxs-lookup"><span data-stu-id="936cc-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="936cc-104">Neste tutorial, você aprenderá como toointegrate Lucidchart com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="936cc-104">In this tutorial, you learn how toointegrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="936cc-105">Integrando o Lucidchart com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="936cc-105">Integrating Lucidchart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="936cc-106">Você pode controlar no AD do Azure que tenha acesso tooLucidchart</span><span class="sxs-lookup"><span data-stu-id="936cc-106">You can control in Azure AD who has access tooLucidchart</span></span>
- <span data-ttu-id="936cc-107">Você pode habilitar seu usuários tooautomatically get conectado tooLucidchart (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="936cc-107">You can enable your users tooautomatically get signed-on tooLucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="936cc-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="936cc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="936cc-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="936cc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="936cc-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="936cc-110">Prerequisites</span></span>

<span data-ttu-id="936cc-111">tooconfigure integração do AD do Azure com o Lucidchart, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="936cc-111">tooconfigure Azure AD integration with Lucidchart, you need hello following items:</span></span>

- <span data-ttu-id="936cc-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="936cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="936cc-113">Uma assinatura do Lucidchart com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="936cc-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="936cc-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="936cc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="936cc-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="936cc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="936cc-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="936cc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="936cc-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="936cc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="936cc-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="936cc-118">Scenario description</span></span>
<span data-ttu-id="936cc-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="936cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="936cc-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="936cc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="936cc-121">Adicionando Lucidchart da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="936cc-121">Adding Lucidchart from hello gallery</span></span>
2. <span data-ttu-id="936cc-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="936cc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-hello-gallery"></a><span data-ttu-id="936cc-123">Adicionando Lucidchart da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="936cc-123">Adding Lucidchart from hello gallery</span></span>
<span data-ttu-id="936cc-124">integração de saudação tooconfigure do Lucidchart no AD do Azure, você precisa tooadd Lucidchart da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="936cc-124">tooconfigure hello integration of Lucidchart into Azure AD, you need tooadd Lucidchart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="936cc-125">**tooadd Lucidchart da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="936cc-125">**tooadd Lucidchart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="936cc-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="936cc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="936cc-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="936cc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="936cc-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="936cc-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="936cc-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="936cc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="936cc-133">Na caixa de pesquisa hello, digite **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="936cc-133">In hello search box, type **Lucidchart**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="936cc-135">No painel de resultados de saudação, selecione **Lucidchart**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="936cc-135">In hello results panel, select **Lucidchart**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="936cc-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="936cc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="936cc-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Lucidchart, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="936cc-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="936cc-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Lucidchart é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="936cc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lucidchart is tooa user in Azure AD.</span></span> <span data-ttu-id="936cc-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Lucidchart precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="936cc-140">In other words, a link relationship between an Azure AD user and hello related user in Lucidchart needs toobe established.</span></span>

<span data-ttu-id="936cc-141">No Lucidchart, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="936cc-141">In Lucidchart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="936cc-142">tooconfigure e teste de logon único do AD do Azure com o Lucidchart, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="936cc-142">tooconfigure and test Azure AD single sign-on with Lucidchart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="936cc-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="936cc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="936cc-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="936cc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="936cc-145">**[Criar um usuário de teste do Lucidchart](#creating-a-lucidchart-test-user)**  -toohave um equivalente do Britta Simon no Lucidchart é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="936cc-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - toohave a counterpart of Britta Simon in Lucidchart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="936cc-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="936cc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="936cc-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="936cc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="936cc-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="936cc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="936cc-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="936cc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="936cc-150">**tooconfigure AD do Azure-logon único com o Lucidchart, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="936cc-150">**tooconfigure Azure AD single sign-on with Lucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="936cc-151">Em Olá portal do Azure, Olá **Lucidchart** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="936cc-151">In hello Azure portal, on hello **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="936cc-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="936cc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="936cc-155">Em Olá **Lucidchart domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="936cc-155">On hello **Lucidchart Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="936cc-157">Em Olá **URL de logon** caixa de texto, digite um URL como:`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="936cc-157">In hello **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="936cc-158">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="936cc-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="936cc-160">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="936cc-160">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="936cc-162">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Lucidchart como administrador.</span><span class="sxs-lookup"><span data-stu-id="936cc-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="936cc-163">No menu de saudação na parte superior de saudação, clique em **equipe**.</span><span class="sxs-lookup"><span data-stu-id="936cc-163">In hello menu on hello top, click **Team**.</span></span>
   
    <span data-ttu-id="936cc-164">![Equipe](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Equipe")</span><span class="sxs-lookup"><span data-stu-id="936cc-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="936cc-165">Clique em **Aplicativos \> Gerenciar SAML**.</span><span class="sxs-lookup"><span data-stu-id="936cc-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="936cc-166">![Gerenciar SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Gerenciar SAML")</span><span class="sxs-lookup"><span data-stu-id="936cc-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="936cc-167">Em Olá **configurações de autenticação SAML** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="936cc-167">On hello **SAML Authentication Settings** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="936cc-168">a.</span><span class="sxs-lookup"><span data-stu-id="936cc-168">a.</span></span> <span data-ttu-id="936cc-169">Selecione **Habilitar Autenticação SAML** e clique em **Opcional**.</span><span class="sxs-lookup"><span data-stu-id="936cc-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="936cc-170">![Configurações de Autenticação SAML](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "Configurações de Autenticação SAML")</span><span class="sxs-lookup"><span data-stu-id="936cc-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="936cc-171">b.</span><span class="sxs-lookup"><span data-stu-id="936cc-171">b.</span></span> <span data-ttu-id="936cc-172">Em Olá **domínio** caixa de texto, digite o seu domínio e, em seguida, clique em **alterar certificado**.</span><span class="sxs-lookup"><span data-stu-id="936cc-172">In hello **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="936cc-173">![Alterar Certificado](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Alterar Certificado")</span><span class="sxs-lookup"><span data-stu-id="936cc-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="936cc-174">c.</span><span class="sxs-lookup"><span data-stu-id="936cc-174">c.</span></span> <span data-ttu-id="936cc-175">Abra o arquivo de metadados baixado, a saudação de copiar conteúda e, em seguida, cole-Olá **carregar metadados** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="936cc-175">Open your downloaded metadata file, copy hello content, and then paste it into hello **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="936cc-176">![Carregar Metadados](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Carregar Metadados")</span><span class="sxs-lookup"><span data-stu-id="936cc-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="936cc-177">d.</span><span class="sxs-lookup"><span data-stu-id="936cc-177">d.</span></span> <span data-ttu-id="936cc-178">Selecione **adicionar automaticamente novo agrupamento de usuários toohello**e, em seguida, clique em **salvar alterações**.</span><span class="sxs-lookup"><span data-stu-id="936cc-178">Select **Automatically Add new users toohello team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="936cc-179">![Salvar Alterações](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Salvar Alterações")</span><span class="sxs-lookup"><span data-stu-id="936cc-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="936cc-180">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="936cc-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="936cc-181">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="936cc-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="936cc-182">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="936cc-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="936cc-183">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="936cc-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="936cc-184">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="936cc-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="936cc-186">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="936cc-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="936cc-187">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="936cc-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="936cc-189">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="936cc-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="936cc-191">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="936cc-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="936cc-193">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="936cc-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="936cc-195">a.</span><span class="sxs-lookup"><span data-stu-id="936cc-195">a.</span></span> <span data-ttu-id="936cc-196">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="936cc-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="936cc-197">b.</span><span class="sxs-lookup"><span data-stu-id="936cc-197">b.</span></span> <span data-ttu-id="936cc-198">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="936cc-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="936cc-199">c.</span><span class="sxs-lookup"><span data-stu-id="936cc-199">c.</span></span> <span data-ttu-id="936cc-200">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="936cc-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="936cc-201">d.</span><span class="sxs-lookup"><span data-stu-id="936cc-201">d.</span></span> <span data-ttu-id="936cc-202">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="936cc-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="936cc-203">Criar um usuário de teste do Lucidchart</span><span class="sxs-lookup"><span data-stu-id="936cc-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="936cc-204">Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooLucidchart.</span><span class="sxs-lookup"><span data-stu-id="936cc-204">There is no action item for you tooconfigure user provisioning tooLucidchart.</span></span>  <span data-ttu-id="936cc-205">Quando um usuário atribuído tenta toolog no Lucidchart usando o painel de acesso hello, Lucidchart verifica se o usuário Olá existe.</span><span class="sxs-lookup"><span data-stu-id="936cc-205">When an assigned user tries toolog into Lucidchart using hello access panel, Lucidchart checks whether hello user exists.</span></span>  

<span data-ttu-id="936cc-206">Se não houver conta de usuário ainda, ela é criada automaticamente pelo Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="936cc-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="936cc-207">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="936cc-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="936cc-208">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLucidchart.</span><span class="sxs-lookup"><span data-stu-id="936cc-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLucidchart.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="936cc-210">**tooassign Britta Simon tooLucidchart, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="936cc-210">**tooassign Britta Simon tooLucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="936cc-211">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="936cc-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="936cc-213">Na lista de aplicativos hello, selecione **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="936cc-213">In hello applications list, select **Lucidchart**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="936cc-215">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="936cc-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="936cc-217">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="936cc-217">Click **Add** button.</span></span> <span data-ttu-id="936cc-218">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="936cc-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="936cc-220">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="936cc-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="936cc-221">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="936cc-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="936cc-222">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="936cc-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="936cc-223">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="936cc-223">Testing single sign-on</span></span>

<span data-ttu-id="936cc-224">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="936cc-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="936cc-225">Quando você clica em bloco Lucidchart Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Lucidchart aplicativo.</span><span class="sxs-lookup"><span data-stu-id="936cc-225">When you click hello Lucidchart tile in hello Access Panel, you should get automatically signed-on tooyour Lucidchart application.</span></span>
<span data-ttu-id="936cc-226">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="936cc-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="936cc-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="936cc-227">Additional resources</span></span>

* [<span data-ttu-id="936cc-228">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="936cc-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="936cc-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="936cc-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

