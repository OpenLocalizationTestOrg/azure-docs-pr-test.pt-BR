---
title: "Tutorial: integração do Azure Active Directory ao SuccessFactors | Microsoft Docs"
description: "Saiba como toouse SuccessFactors com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="9f1f3-103">Tutorial: Integração do Azure Active Directory com o SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="9f1f3-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="9f1f3-104">Olá objetivo deste tutorial é tooshow você como toointegrate SuccessFactors com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="9f1f3-104">hello objective of this tutorial is tooshow you how toointegrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f1f3-105">Integrando o SuccessFactors com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-105">Integrating SuccessFactors with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="9f1f3-106">Você pode controlar no AD do Azure que tenha acesso tooSuccessFactors</span><span class="sxs-lookup"><span data-stu-id="9f1f3-106">You can control in Azure AD who has access tooSuccessFactors</span></span>
* <span data-ttu-id="9f1f3-107">Você pode habilitar seus usuários tooautomatically get conectado tooSuccessFactors (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f1f3-107">You can enable your users tooautomatically get signed-on tooSuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="9f1f3-108">Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="9f1f3-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="9f1f3-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f1f3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f1f3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9f1f3-110">Prerequisites</span></span>
<span data-ttu-id="9f1f3-111">tooconfigure integração do AD do Azure com o SuccessFactors, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-111">tooconfigure Azure AD integration with SuccessFactors, you need hello following items:</span></span>

* <span data-ttu-id="9f1f3-112">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="9f1f3-112">A valid Azure subscription</span></span>
* <span data-ttu-id="9f1f3-113">Um locatário no SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="9f1f3-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="9f1f3-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="9f1f3-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="9f1f3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="9f1f3-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f1f3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f1f3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9f1f3-118">Scenario description</span></span>
<span data-ttu-id="9f1f3-119">Olá objetivo deste tutorial é tooenable tootest logon único do AD do Azure em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="9f1f3-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f1f3-121">Adicionando SuccessFactors da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9f1f3-121">Adding SuccessFactors from hello gallery</span></span>
2. <span data-ttu-id="9f1f3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f1f3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-hello-gallery"></a><span data-ttu-id="9f1f3-123">Adicionando SuccessFactors da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9f1f3-123">Adding SuccessFactors from hello gallery</span></span>
<span data-ttu-id="9f1f3-124">integração de saudação tooconfigure do SuccessFactors no AD do Azure, você precisa tooadd SuccessFactors da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-124">tooconfigure hello integration of SuccessFactors into Azure AD, you need tooadd SuccessFactors from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9f1f3-125">**tooadd SuccessFactors da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f1f3-125">**tooadd SuccessFactors from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f1f3-126">No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-126">In hello Azure classic portal, on hello left navigation panel, click **Active Directory**.</span></span>
   
    ![Configurando o logon único][1]
2. <span data-ttu-id="9f1f3-128">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="9f1f3-129">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Configurando o logon único][2]
4. <span data-ttu-id="9f1f3-131">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicativos][3]
5. <span data-ttu-id="9f1f3-133">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Configurando o logon único][4]
6. <span data-ttu-id="9f1f3-135">Em Olá **caixa de pesquisa**, tipo **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-135">In hello **search box**, type **SuccessFactors**.</span></span>
   
    ![Configurando o logon único][5]
7. <span data-ttu-id="9f1f3-137">No painel de resultados de saudação, selecione **SuccessFactors**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-137">In hello results panel, select **SuccessFactors**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Configurando o logon único][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f1f3-139">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f1f3-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9f1f3-140">Olá o objetivo desta seção é tooshow como tooconfigure e teste de logon único do AD do Azure com o SuccessFactors com base em um usuário de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9f1f3-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9f1f3-141">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SuccessFactors tooan usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SuccessFactors tooan user in Azure AD is.</span></span> <span data-ttu-id="9f1f3-142">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no SuccessFactors precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-142">In other words, a link relationship between an Azure AD user and hello related user in SuccessFactors needs toobe established.</span></span>

<span data-ttu-id="9f1f3-143">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SuccessFactors.</span></span>

<span data-ttu-id="9f1f3-144">tooconfigure e teste de logon único do AD do Azure com o SuccessFactors, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-144">tooconfigure and test Azure AD single sign-on with SuccessFactors, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9f1f3-145">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9f1f3-146">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f1f3-147">**[Criar um usuário de teste do SuccessFactors](#creating-a-successfactors-test-user)**  -toohave um equivalente do Britta Simon no SuccessFactors é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - toohave a counterpart of Britta Simon in SuccessFactors that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9f1f3-148">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f1f3-149">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f1f3-150">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f1f3-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="9f1f3-151">Nesta seção, habilitar o AD do Azure-logon único no portal clássico do hello e configurar o logon único em seu aplicativo SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="9f1f3-152">**tooconfigure AD do Azure-logon único com o SuccessFactors, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f1f3-152">**tooconfigure Azure AD single sign-on with SuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f1f3-153">Em Olá portal clássico do Azure, em Olá **SuccessFactors** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-153">In hello Azure classic portal, on hello **SuccessFactors** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    ![Configurando o logon único][7]
2. <span data-ttu-id="9f1f3-155">Em Olá **como você gostaria usuários toosign em tooSuccessFactors** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-155">On hello **How would you like users toosign on tooSuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configurando o logon único][8]
3. <span data-ttu-id="9f1f3-157">Em Olá **configurar URL do aplicativo** página executar Olá etapas a seguir e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-157">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    ![Configurando o logon único][9]
   
    <span data-ttu-id="9f1f3-159">a.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-159">a.</span></span> <span data-ttu-id="9f1f3-160">Em Olá **URL de logon** caixa de texto, digite um URL usando uma saudação padrões a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-160">In hello **Sign On URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="9f1f3-161">b.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-161">b.</span></span> <span data-ttu-id="9f1f3-162">Em Olá **URL de resposta** caixa de texto, digite um URL usando uma saudação padrões a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-162">In hello **Reply URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="9f1f3-163">c.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-163">c.</span></span> <span data-ttu-id="9f1f3-164">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="9f1f3-165">Observe que esses não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-165">Please note that these are not hello real values.</span></span> <span data-ttu-id="9f1f3-166">Você tem tooupdate esses valores com a URL real Olá URL de logon e de resposta.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-166">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="9f1f3-167">entre em contato com tooget esses valores, [equipe de suporte do SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="9f1f3-167">tooget these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="9f1f3-168">Em Olá **configurar logon único no SuccessFactors** , clique em **Download certificado**e, em seguida, salve o arquivo de certificado de saudação localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-168">On hello **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Configurando o logon único][10]

2. <span data-ttu-id="9f1f3-170">Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do **portal de administração do SuccessFactors** como administrador.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="9f1f3-171">Visite **segurança do aplicativo** e nativo muito**logon único no recurso**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-171">Visit **Application Security** and native too**Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="9f1f3-172">Inserir qualquer valor na Olá **redefinir Token** e clique em **salvar Token** tooenable SSO do SAML.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-172">Place any value in hello **Reset Token** and click **Save Token** tooenable SAML SSO.</span></span>
   
    ![Configurar o logon único no lado do aplicativo][11]

    > [!NOTE] 
    > <span data-ttu-id="9f1f3-174">Esse valor é usado apenas como Olá interruptor.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-174">This value is just used as hello on/off switch.</span></span> <span data-ttu-id="9f1f3-175">Se nenhum valor for salvo, Olá SSO do SAML é ON.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-175">If any value is saved, hello SAML SSO is ON.</span></span> <span data-ttu-id="9f1f3-176">Se um valor em branco é salvo Olá SSO do SAML é OFF.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-176">If a blank value is saved hello SAML SSO is OFF.</span></span>

1. <span data-ttu-id="9f1f3-177">Captura de tela de toobelow nativos e executar Olá ações a seguir.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-177">Native toobelow screenshot and perform hello following actions.</span></span>
   
    ![Configurar o logon único no lado do aplicativo][12]
   
    <span data-ttu-id="9f1f3-179">a.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-179">a.</span></span> <span data-ttu-id="9f1f3-180">Selecione Olá **SSO do SAML v2** botão de opção</span><span class="sxs-lookup"><span data-stu-id="9f1f3-180">Select hello **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="9f1f3-181">b.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-181">b.</span></span> <span data-ttu-id="9f1f3-182">Defina Olá SAML declarar parte Name(e.g. SAml issuer + company name).</span><span class="sxs-lookup"><span data-stu-id="9f1f3-182">Set hello SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="9f1f3-183">c.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-183">c.</span></span> <span data-ttu-id="9f1f3-184">Em Olá **emissor SAML** caixa de texto colocar o valor de saudação de **URL do emissor** do Assistente de configuração de aplicativo do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-184">In hello **SAML Issuer** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="9f1f3-185">d.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-185">d.</span></span> <span data-ttu-id="9f1f3-186">Selecione **Resposta(Gerada pelo Cliente/IdP/AP)** como **Exigir Assinatura Obrigatória**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="9f1f3-187">e.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-187">e.</span></span> <span data-ttu-id="9f1f3-188">Selecione **Habilitado** como **Habilitar Sinalizador SAML**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="9f1f3-189">f.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-189">f.</span></span> <span data-ttu-id="9f1f3-190">Selecione **Não** como **Assinatura da Solicitação de Logon (Gerado por SF/SP/RP)**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="9f1f3-191">g.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-191">g.</span></span> <span data-ttu-id="9f1f3-192">Selecione **Perfil de Navegador/Postagem** como **Perfil SAML**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="9f1f3-193">h.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-193">h.</span></span> <span data-ttu-id="9f1f3-194">Selecione **Não** como **Impor Período de Certificado Válido**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="9f1f3-195">i.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-195">i.</span></span> <span data-ttu-id="9f1f3-196">Copiar conteúdo Olá Olá baixado do arquivo de certificado e, em seguida, cole-Olá **SAML verificando certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-196">Copy hello content of hello downloaded certificate file, and then paste it into hello **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9f1f3-197">conteúdo do certificado Olá deve ter começar marcas de certificado do certificado e de fim.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-197">hello certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="9f1f3-198">Navegar tooSAML V2 e, em seguida, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-198">Navigate tooSAML V2, and then perform hello following steps:</span></span>
   
    ![Configurar o logon único no lado do aplicativo][13]
   
    <span data-ttu-id="9f1f3-200">a.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-200">a.</span></span> <span data-ttu-id="9f1f3-201">Selecione **Sim** como **Logoff Global iniciado por SP de suporte**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="9f1f3-202">b.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-202">b.</span></span> <span data-ttu-id="9f1f3-203">Em Olá **URL do serviço Global Logout (destino LogoutRequest)** caixa de texto colocar o valor de saudação de **URL de Logout remoto** do Assistente de configuração de aplicativo do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-203">In hello **Global Logout Service URL (LogoutRequest destination)** textbox put hello value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="9f1f3-204">c.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-204">c.</span></span> <span data-ttu-id="9f1f3-205">Selecione **Não** como **Exigir que sp criptografe todos os elementos NameID**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="9f1f3-206">d.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-206">d.</span></span> <span data-ttu-id="9f1f3-207">Selecione **não especificado** como **Formato de NameID**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="9f1f3-208">e.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-208">e.</span></span> <span data-ttu-id="9f1f3-209">Selecione **Sim** como **Habilitar logon iniciado por sp (AuthnRequest)**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="9f1f3-210">f.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-210">f.</span></span> <span data-ttu-id="9f1f3-211">Em Olá **solicitação de envio como o emissor de toda a empresa** caixa de texto colocar o valor de saudação de **URL de logon remoto** do Assistente de configuração de aplicativo do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-211">In hello **Send request as Company-Wide issuer** textbox put hello value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="9f1f3-212">Execute estas etapas se desejar que os nomes de usuário de logon de saudação toomake não diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-212">Perform these steps if you want toomake hello login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="9f1f3-213">a.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-213">a.</span></span> <span data-ttu-id="9f1f3-214">Visite **configurações da empresa**(parte inferior Olá).</span><span class="sxs-lookup"><span data-stu-id="9f1f3-214">Visit **Company Settings**(near hello bottom).</span></span>
   
    <span data-ttu-id="9f1f3-215">b.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-215">b.</span></span> <span data-ttu-id="9f1f3-216">marque a caixa de seleção ao lado de **Habilitar Nome de Usuário que Não Diferencia Maiúsculas de Minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="9f1f3-217">c.Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-217">c.Click **Save**.</span></span>
   
    ![Configurar Logon Único][29]

    > [!NOTE] 
    > <span data-ttu-id="9f1f3-219">Se você tentar tooenable isso, o sistema de saudação verifica se ele criará um nome de logon do SAML duplicado.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-219">If you try tooenable this, hello system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="9f1f3-220">Por exemplo, se o cliente Olá tem nomes de usuário Usuário1 e user1.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-220">For example if hello customer has usernames User1 and user1.</span></span> <span data-ttu-id="9f1f3-221">Parar de diferenciar maiúsculas e minúsculas cria essas duplicatas.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="9f1f3-222">sistema de saudação dará a você uma mensagem de erro e não habilitará o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-222">hello system will give you an error message and will not enable hello feature.</span></span> <span data-ttu-id="9f1f3-223">Olá cliente precisará toochange um dos nomes de usuário Olá para ele, na verdade, está escrito diferentes.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-223">hello customer will need toochange one of hello usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="9f1f3-224">Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-224">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    ![Aplicativos][14]
2. <span data-ttu-id="9f1f3-226">Em Olá **único logon confirmação** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-226">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Aplicativos][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f1f3-228">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f1f3-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f1f3-229">Olá objetivo desta seção é toocreate um usuário de teste no portal clássico do hello chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-229">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][16]

<span data-ttu-id="9f1f3-231">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f1f3-231">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f1f3-232">Em Olá **Portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-232">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][17]
2. <span data-ttu-id="9f1f3-234">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-234">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="9f1f3-235">lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-235">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][18]
4. <span data-ttu-id="9f1f3-237">Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-237">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][19]
5. <span data-ttu-id="9f1f3-239">Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-239">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][20]
   
    <span data-ttu-id="9f1f3-241">a.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-241">a.</span></span> <span data-ttu-id="9f1f3-242">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="9f1f3-243">b.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-243">b.</span></span> <span data-ttu-id="9f1f3-244">Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-244">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="9f1f3-245">c.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-245">c.</span></span> <span data-ttu-id="9f1f3-246">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-246">Click **Next**.</span></span>
6. <span data-ttu-id="9f1f3-247">Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-247">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][21]
   
    <span data-ttu-id="9f1f3-249">a.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-249">a.</span></span> <span data-ttu-id="9f1f3-250">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-250">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="9f1f3-251">b.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-251">b.</span></span> <span data-ttu-id="9f1f3-252">Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-252">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="9f1f3-253">c.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-253">c.</span></span> <span data-ttu-id="9f1f3-254">Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-254">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="9f1f3-255">d.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-255">d.</span></span> <span data-ttu-id="9f1f3-256">Em Olá **função** lista, selecione **usuário**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-256">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="9f1f3-257">e.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-257">e.</span></span> <span data-ttu-id="9f1f3-258">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-258">Click **Next**.</span></span>
7. <span data-ttu-id="9f1f3-259">Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-259">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][22]
8. <span data-ttu-id="9f1f3-261">Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f1f3-261">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][23]
   
    <span data-ttu-id="9f1f3-263">a.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-263">a.</span></span> <span data-ttu-id="9f1f3-264">Anote o valor Olá Olá **nova senha**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-264">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="9f1f3-265">b.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-265">b.</span></span> <span data-ttu-id="9f1f3-266">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="9f1f3-267">Criação de um usuário de teste do SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="9f1f3-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="9f1f3-268">Ordem tooenable AD do Azure usuários toolog no SuccessFactors, eles devem ser provisionados no SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-268">In order tooenable Azure AD users toolog into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="9f1f3-269">No caso de saudação do SuccessFactors, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-269">In hello case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="9f1f3-270">usuários tooget criados no SuccessFactors, você precisa Olá toocontact [equipe de suporte do SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="9f1f3-270">tooget users created in SuccessFactors, you need toocontact hello [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9f1f3-271">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f1f3-271">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="9f1f3-272">Olá objetivo desta seção é tooenabling Britta Simon toouse logon único do Azure concedendo tooSuccessFactors seu acesso.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-272">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSuccessFactors.</span></span>

![Atribuir usuário][24]

<span data-ttu-id="9f1f3-274">**tooassign Britta Simon tooSuccessFactors, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9f1f3-274">**tooassign Britta Simon tooSuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f1f3-275">No portal clássico do hello, exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, clique em **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-275">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Atribuir usuário][25]
2. <span data-ttu-id="9f1f3-277">Na lista de aplicativos hello, selecione **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-277">In hello applications list, select **SuccessFactors**.</span></span>
   
    ![Configurar Logon Único][26]
3. <span data-ttu-id="9f1f3-279">No menu de saudação na parte superior de saudação, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-279">In hello menu on hello top, click **Users**.</span></span>
   
    ![Atribuir usuário][27]
4. <span data-ttu-id="9f1f3-281">Na lista de usuários hello, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-281">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="9f1f3-282">Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-282">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Atribuir usuário][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="9f1f3-284">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9f1f3-284">Testing single sign-on</span></span>
<span data-ttu-id="9f1f3-285">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-285">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9f1f3-286">Quando você clica em Olá SuccessFactors bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="9f1f3-286">When you click hello SuccessFactors tile in hello Access Panel, you should get automatically signed-on tooyour SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9f1f3-287">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9f1f3-287">Additional resources</span></span>
* [<span data-ttu-id="9f1f3-288">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9f1f3-288">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f1f3-289">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9f1f3-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
