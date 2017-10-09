---
title: "Tutorial: Integração do Azure Active Directory com o Jive | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: f22bf78a55e8a4a9ea2f0020ef2f535be88b6302
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="e1cdb-103">Tutorial: Integração do Active Directory do Azure com o Jive</span><span class="sxs-lookup"><span data-stu-id="e1cdb-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="e1cdb-104">Neste tutorial, você aprenderá como toointegrate Jive com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="e1cdb-104">In this tutorial, you learn how toointegrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1cdb-105">Integrando Jive com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cdb-105">Integrating Jive with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e1cdb-106">Você pode controlar no AD do Azure que tenha acesso tooJive</span><span class="sxs-lookup"><span data-stu-id="e1cdb-106">You can control in Azure AD who has access tooJive</span></span>
- <span data-ttu-id="e1cdb-107">Você pode habilitar seu usuários tooautomatically get conectado tooJive (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e1cdb-107">You can enable your users tooautomatically get signed-on tooJive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1cdb-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e1cdb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e1cdb-109">Se você quiser tooknow para obter mais informações sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1cdb-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1cdb-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e1cdb-110">Prerequisites</span></span>

<span data-ttu-id="e1cdb-111">tooconfigure integração do AD do Azure com Jive, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cdb-111">tooconfigure Azure AD integration with Jive, you need hello following items:</span></span>

- <span data-ttu-id="e1cdb-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e1cdb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1cdb-113">Uma assinatura habilitada para logon único do Jive</span><span class="sxs-lookup"><span data-stu-id="e1cdb-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1cdb-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1cdb-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e1cdb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1cdb-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1cdb-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1cdb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1cdb-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e1cdb-118">Scenario description</span></span>
<span data-ttu-id="e1cdb-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1cdb-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="e1cdb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1cdb-121">Adicionando Jive da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e1cdb-121">Adding Jive from hello gallery</span></span>
2. <span data-ttu-id="e1cdb-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e1cdb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-hello-gallery"></a><span data-ttu-id="e1cdb-123">Adicionando Jive da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e1cdb-123">Adding Jive from hello gallery</span></span>
<span data-ttu-id="e1cdb-124">integração de saudação do tooconfigure do Jive no AD do Azure, você precisa tooadd Jive da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-124">tooconfigure hello integration of Jive into Azure AD, you need tooadd Jive from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e1cdb-125">**tooadd Jive da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e1cdb-125">**tooadd Jive from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1cdb-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1cdb-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e1cdb-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e1cdb-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e1cdb-133">Na caixa de pesquisa hello, digite **Jive**.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-133">In hello search box, type **Jive**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="e1cdb-135">No painel de resultados de saudação, selecione **Jive**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-135">In hello results panel, select **Jive**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1cdb-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e1cdb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e1cdb-138">Nesta seção, você configura e testa o logon único do Azure AD com o Jive, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e1cdb-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Jive é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jive is tooa user in Azure AD.</span></span> <span data-ttu-id="e1cdb-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Jive precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-140">In other words, a link relationship between an Azure AD user and hello related user in Jive needs toobe established.</span></span>

<span data-ttu-id="e1cdb-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Jive.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Jive.</span></span>

<span data-ttu-id="e1cdb-142">tooconfigure e teste de logon único do AD do Azure com Jive, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cdb-142">tooconfigure and test Azure AD single sign-on with Jive, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e1cdb-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e1cdb-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1cdb-145">**[Criar um usuário de teste do Jive](#creating-a-jive-test-user)**  -toohave um equivalente do Britta Simon em Jive é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - toohave a counterpart of Britta Simon in Jive that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1cdb-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1cdb-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1cdb-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1cdb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e1cdb-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Jive.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="e1cdb-150">**tooconfigure logon único do AD do Azure com Jive, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e1cdb-150">**tooconfigure Azure AD single sign-on with Jive, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1cdb-151">Em Olá portal do Azure, Olá **Jive** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-151">In hello Azure portal, on hello **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e1cdb-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="e1cdb-155">Em Olá **Jive domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cdb-155">On hello **Jive Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="e1cdb-157">a.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-157">a.</span></span> <span data-ttu-id="e1cdb-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="e1cdb-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="e1cdb-159">b.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-159">b.</span></span> <span data-ttu-id="e1cdb-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="e1cdb-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e1cdb-161">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-161">These values are not hello real.</span></span> <span data-ttu-id="e1cdb-162">Atualize esses valores com URL de logon real hello e o identificador.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="e1cdb-163">Entre em contato com [equipe de suporte do cliente Jive](https://www.jivesoftware.com/services-support/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="e1cdb-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="e1cdb-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e1cdb-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e1cdb-168">tooconfigure logon único no **Jive** locatário do Jive tooyour lado, logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-168">tooconfigure single sign-on on **Jive** side, sign-on tooyour Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="e1cdb-169">No menu de saudação na parte superior de saudação, clique em "**Saml**."</span><span class="sxs-lookup"><span data-stu-id="e1cdb-169">In hello menu on hello top, Click "**Saml**."</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="e1cdb-171">a.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-171">a.</span></span> <span data-ttu-id="e1cdb-172">Selecione **habilitado** em Olá **geral** guia.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-172">Select **Enabled** under hello **General** tab.</span></span>   
    <span data-ttu-id="e1cdb-173">b.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-173">b.</span></span> <span data-ttu-id="e1cdb-174">Clique em hello "**salvar todas as configurações de saml**" botão.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-174">Click hello "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="e1cdb-175">Navegue toohello "**metadados Idp**" guia.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-175">Navigate toohello "**Idp Metadata**" tab.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="e1cdb-177">a.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-177">a.</span></span> <span data-ttu-id="e1cdb-178">Copiar conteúdo Olá Olá baixado XML do arquivo de metadados e, em seguida, cole-Olá **metadados do provedor de identidade (IDP)** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-178">Copy hello content of hello downloaded metadata XML file, and then paste it into hello **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="e1cdb-179">b.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-179">b.</span></span> <span data-ttu-id="e1cdb-180">Clique em hello "**salvar todas as configurações de saml**" botão.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-180">Click hello "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="e1cdb-181">Vá toohello "**mapeamento de atributo de usuário**" guia.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-181">Go toohello "**User Attribute Mapping**" tab.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="e1cdb-183">a.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-183">a.</span></span> <span data-ttu-id="e1cdb-184">Em Olá **Email** caixa de texto, copiar e Colar nome do atributo de saudação do **mail** valor.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-184">In hello **Email** textbox, copy and paste hello attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="e1cdb-185">b.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-185">b.</span></span> <span data-ttu-id="e1cdb-186">Em Olá **nome** caixa de texto, copiar e Colar nome do atributo de saudação do **givenname** valor.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-186">In hello **First Name** textbox, copy and paste hello attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="e1cdb-187">c.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-187">c.</span></span> <span data-ttu-id="e1cdb-188">Em Olá **Sobrenome** caixa de texto, copiar e Colar nome do atributo de saudação do **Sobrenome** valor.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-188">In hello **Last Name** textbox, copy and paste hello attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="e1cdb-189">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="e1cdb-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e1cdb-190">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e1cdb-191">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1cdb-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1cdb-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e1cdb-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="e1cdb-193">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e1cdb-195">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e1cdb-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1cdb-196">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1cdb-198">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1cdb-200">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1cdb-202">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1cdb-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1cdb-204">a.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-204">a.</span></span> <span data-ttu-id="e1cdb-205">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1cdb-206">b.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-206">b.</span></span> <span data-ttu-id="e1cdb-207">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1cdb-208">c.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-208">c.</span></span> <span data-ttu-id="e1cdb-209">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e1cdb-210">d.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-210">d.</span></span> <span data-ttu-id="e1cdb-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="e1cdb-212">Criar um usuário de teste Jive</span><span class="sxs-lookup"><span data-stu-id="e1cdb-212">Creating a Jive test user</span></span>

<span data-ttu-id="e1cdb-213">Trabalhar com [equipe de suporte do cliente Jive](https://www.jivesoftware.com/services-support/) tooadd usuários de saudação na plataforma do hello Jive.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) tooadd hello users in hello Jive platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e1cdb-214">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e1cdb-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e1cdb-215">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooJive.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJive.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e1cdb-217">**tooassign Britta Simon tooJive, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e1cdb-217">**tooassign Britta Simon tooJive, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1cdb-218">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e1cdb-220">Na lista de aplicativos hello, selecione **Jive**.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-220">In hello applications list, select **Jive**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="e1cdb-222">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e1cdb-224">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-224">Click **Add** button.</span></span> <span data-ttu-id="e1cdb-225">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e1cdb-227">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e1cdb-228">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1cdb-229">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e1cdb-230">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e1cdb-230">Testing single sign-on</span></span>

<span data-ttu-id="e1cdb-231">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e1cdb-232">Quando você clica em bloco Jive Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Jive.</span><span class="sxs-lookup"><span data-stu-id="e1cdb-232">When you click hello Jive tile in hello Access Panel, you should get automatically signed-on tooyour Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1cdb-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e1cdb-233">Additional resources</span></span>

* [<span data-ttu-id="e1cdb-234">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e1cdb-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1cdb-235">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e1cdb-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e1cdb-236">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="e1cdb-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

