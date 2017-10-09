---
title: "Tutorial: integração do Azure Active Directory ao Kronos | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Kronos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 16fd5c203162d10b78f51b00d79017adaf8632c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="68a6b-103">Tutorial: integração do Azure Active Directory com o Kronos</span><span class="sxs-lookup"><span data-stu-id="68a6b-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="68a6b-104">Neste tutorial, você aprenderá como toointegrate Kronos com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="68a6b-104">In this tutorial, you learn how toointegrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68a6b-105">Integrando Kronos com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="68a6b-105">Integrating Kronos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="68a6b-106">Você pode controlar no AD do Azure que tenha acesso tooKronos</span><span class="sxs-lookup"><span data-stu-id="68a6b-106">You can control in Azure AD who has access tooKronos</span></span>
- <span data-ttu-id="68a6b-107">Você pode habilitar seus usuários tooautomatically get conectado tooKronos (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="68a6b-107">You can enable your users tooautomatically get signed-on tooKronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="68a6b-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="68a6b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="68a6b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="68a6b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68a6b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="68a6b-110">Prerequisites</span></span>

<span data-ttu-id="68a6b-111">tooconfigure integração do AD do Azure com Kronos, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="68a6b-111">tooconfigure Azure AD integration with Kronos, you need hello following items:</span></span>

- <span data-ttu-id="68a6b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="68a6b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="68a6b-113">Uma assinatura habilitada para SSO do **Kronos Workforce Central**</span><span class="sxs-lookup"><span data-stu-id="68a6b-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68a6b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="68a6b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68a6b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="68a6b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68a6b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="68a6b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68a6b-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68a6b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68a6b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="68a6b-118">Scenario description</span></span>
<span data-ttu-id="68a6b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="68a6b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68a6b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="68a6b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68a6b-121">Adicionando Kronos da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="68a6b-121">Adding Kronos from hello gallery</span></span>
2. <span data-ttu-id="68a6b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="68a6b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-hello-gallery"></a><span data-ttu-id="68a6b-123">Adicionando Kronos da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="68a6b-123">Adding Kronos from hello gallery</span></span>
<span data-ttu-id="68a6b-124">integração de saudação tooconfigure de Kronos no AD do Azure, você precisa tooadd Kronos da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="68a6b-124">tooconfigure hello integration of Kronos into Azure AD, you need tooadd Kronos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="68a6b-125">**tooadd Kronos da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="68a6b-125">**tooadd Kronos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="68a6b-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="68a6b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="68a6b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="68a6b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="68a6b-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="68a6b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="68a6b-133">Na caixa de pesquisa hello, digite **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-133">In hello search box, type **Kronos**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="68a6b-135">No painel de resultados de saudação, selecione **Kronos**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="68a6b-135">In hello results panel, select **Kronos**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="68a6b-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="68a6b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="68a6b-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Kronos, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="68a6b-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="68a6b-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Kronos é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="68a6b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kronos is tooa user in Azure AD.</span></span> <span data-ttu-id="68a6b-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Kronos precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="68a6b-140">In other words, a link relationship between an Azure AD user and hello related user in Kronos needs toobe established.</span></span>

<span data-ttu-id="68a6b-141">Kronos, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="68a6b-141">In Kronos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="68a6b-142">tooconfigure e teste de logon único do AD do Azure com Kronos, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="68a6b-142">tooconfigure and test Azure AD single sign-on with Kronos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="68a6b-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="68a6b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="68a6b-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68a6b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="68a6b-145">**[Criar um usuário de teste Kronos](#creating-a-kronos-test-user)**  -toohave um equivalente do Britta Simon em Kronos é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="68a6b-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - toohave a counterpart of Britta Simon in Kronos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="68a6b-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="68a6b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="68a6b-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="68a6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="68a6b-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="68a6b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="68a6b-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Kronos.</span><span class="sxs-lookup"><span data-stu-id="68a6b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="68a6b-150">**tooconfigure AD do Azure-logon único com Kronos, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="68a6b-150">**tooconfigure Azure AD single sign-on with Kronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="68a6b-151">Em Olá portal do Azure, Olá **Kronos** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-151">In hello Azure portal, on hello **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="68a6b-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="68a6b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="68a6b-155">Em Olá **Kronos domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="68a6b-155">On hello **Kronos Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="68a6b-157">a.</span><span class="sxs-lookup"><span data-stu-id="68a6b-157">a.</span></span> <span data-ttu-id="68a6b-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="68a6b-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="68a6b-159">b.</span><span class="sxs-lookup"><span data-stu-id="68a6b-159">b.</span></span> <span data-ttu-id="68a6b-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="68a6b-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="68a6b-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="68a6b-161">These values are not real.</span></span> <span data-ttu-id="68a6b-162">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="68a6b-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="68a6b-163">Entre em contato com [Kronos equipe de suporte](https://www.kronos.in/contact/en-in/form) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="68a6b-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) tooget these values.</span></span>
 
4. <span data-ttu-id="68a6b-164">Seu aplicativo de Kronos espera as asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="68a6b-164">Your Kronos application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="68a6b-165">Trabalhar com [Kronos equipe de suporte](https://www.kronos.in/contact/en-in/form) primeiro tooidentify Olá correto identificador do usuário, que é mapeado para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="68a6b-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first tooidentify hello correct user identifier, which is mapped into hello application.</span></span> <span data-ttu-id="68a6b-166">Reserve também orientações Olá sobre atributo Olá que quiserem toouse para que esse mapeamento.</span><span class="sxs-lookup"><span data-stu-id="68a6b-166">Also please take hello guidance about hello attribute, which they want toouse for this mapping.</span></span>
 
     <span data-ttu-id="68a6b-167">A Microsoft recomenda usar Olá **"NameIdentifier"** atributo como identificador de usuário.</span><span class="sxs-lookup"><span data-stu-id="68a6b-167">Microsoft recommends using hello **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="68a6b-168">Você pode gerenciar os valores hello desses atributos de saudação **"Atributos do usuário"** seção na página de integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="68a6b-168">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="68a6b-169">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="68a6b-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="68a6b-170">Aqui nós mapeou hello **identificador de usuário (nameid)** com **ExtractMailPrefix()** função de **User**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-170">Here we have mapped hello **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="68a6b-171">Isso retorna o valor de prefixo de saudação de email do usuário de saudação que é Olá ID exclusivo do usuário.</span><span class="sxs-lookup"><span data-stu-id="68a6b-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="68a6b-172">Isto é enviado toohello Kronos aplicativo em cada resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="68a6b-172">This is sent toohello Kronos application in every successful response.</span></span> 
     
    ![Configurar Logon Único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="68a6b-174">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="68a6b-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="68a6b-175">a.</span><span class="sxs-lookup"><span data-stu-id="68a6b-175">a.</span></span> <span data-ttu-id="68a6b-176">Na lista de lista suspensa de identificador de usuário hello, selecione **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-176">In hello User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="68a6b-177">b.</span><span class="sxs-lookup"><span data-stu-id="68a6b-177">b.</span></span> <span data-ttu-id="68a6b-178">Em Olá **Mail** lista suspensa, selecione **User**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-178">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="68a6b-179">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="68a6b-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="68a6b-181">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="68a6b-181">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="68a6b-183">tooconfigure logon único no **Kronos** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do Kronos](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="68a6b-183">tooconfigure single sign-on on **Kronos** side, you need toosend hello downloaded **Metadata XML** too[Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="68a6b-184">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="68a6b-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="68a6b-185">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="68a6b-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="68a6b-186">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="68a6b-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="68a6b-187">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="68a6b-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="68a6b-188">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="68a6b-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="68a6b-190">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="68a6b-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="68a6b-191">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="68a6b-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="68a6b-193">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="68a6b-195">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="68a6b-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="68a6b-197">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="68a6b-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="68a6b-199">a.</span><span class="sxs-lookup"><span data-stu-id="68a6b-199">a.</span></span> <span data-ttu-id="68a6b-200">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68a6b-201">b.</span><span class="sxs-lookup"><span data-stu-id="68a6b-201">b.</span></span> <span data-ttu-id="68a6b-202">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="68a6b-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="68a6b-203">c.</span><span class="sxs-lookup"><span data-stu-id="68a6b-203">c.</span></span> <span data-ttu-id="68a6b-204">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="68a6b-205">d.</span><span class="sxs-lookup"><span data-stu-id="68a6b-205">d.</span></span> <span data-ttu-id="68a6b-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="68a6b-207">Criar um usuário de teste do Kronos</span><span class="sxs-lookup"><span data-stu-id="68a6b-207">Creating a Kronos test user</span></span>

<span data-ttu-id="68a6b-208">Nesta seção, você criará um usuário chamado Brenda Fernandes no Kronos.</span><span class="sxs-lookup"><span data-stu-id="68a6b-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="68a6b-209">Kronos aplicativo precisa de todos os toobe de usuários Olá provisionado no aplicativo hello antes de executar o SSO.</span><span class="sxs-lookup"><span data-stu-id="68a6b-209">Kronos application needs all hello users toobe provisioned in hello application before doing SSO.</span></span> 

<span data-ttu-id="68a6b-210">Trabalhar com hello [Kronos equipe de suporte](https://www.kronos.in/contact/en-in/form) tooprovision todos esses usuários para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="68a6b-210">Work with hello [Kronos support team](https://www.kronos.in/contact/en-in/form) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="68a6b-211">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="68a6b-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="68a6b-212">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooKronos.</span><span class="sxs-lookup"><span data-stu-id="68a6b-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKronos.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="68a6b-214">**tooassign Britta Simon tooKronos, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="68a6b-214">**tooassign Britta Simon tooKronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="68a6b-215">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="68a6b-217">Na lista de aplicativos hello, selecione **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-217">In hello applications list, select **Kronos**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="68a6b-219">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="68a6b-221">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="68a6b-221">Click **Add** button.</span></span> <span data-ttu-id="68a6b-222">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="68a6b-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="68a6b-224">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="68a6b-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="68a6b-225">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="68a6b-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="68a6b-226">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="68a6b-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="68a6b-227">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="68a6b-227">Testing single sign-on</span></span>

<span data-ttu-id="68a6b-228">Nesta seção, você deve testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="68a6b-228">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="68a6b-229">Quando você clica em Olá Kronos bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Kronos aplicativo.</span><span class="sxs-lookup"><span data-stu-id="68a6b-229">When you click hello Kronos tile in hello Access Panel, you should get automatically signed-on tooyour Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="68a6b-230">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="68a6b-230">Additional resources</span></span>

* [<span data-ttu-id="68a6b-231">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="68a6b-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="68a6b-232">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="68a6b-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

