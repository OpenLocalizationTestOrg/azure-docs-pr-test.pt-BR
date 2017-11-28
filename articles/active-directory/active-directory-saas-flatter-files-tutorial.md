---
title: "Tutorial: integração do Azure Active Directory com o Flatter Files | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e arquivos simples."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 73ca2613b7bbaf9992ecf624ff5defabaa44f7a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="5c26c-103">Tutorial: Integração do Active Directory do Azure ao Flatter Files</span><span class="sxs-lookup"><span data-stu-id="5c26c-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="5c26c-104">Neste tutorial, você aprenderá como toointegrate arquivos simples com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="5c26c-104">In this tutorial, you learn how toointegrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c26c-105">Integrando arquivos simples com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c26c-105">Integrating Flatter Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5c26c-106">Você pode controlar no AD do Azure que tenha acesso tooFlatter arquivos</span><span class="sxs-lookup"><span data-stu-id="5c26c-106">You can control in Azure AD who has access tooFlatter Files</span></span>
- <span data-ttu-id="5c26c-107">Você pode habilitar seu usuários tooautomatically obter arquivos tooFlatter conectado (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c26c-107">You can enable your users tooautomatically get signed-on tooFlatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c26c-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5c26c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5c26c-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c26c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c26c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5c26c-110">Prerequisites</span></span>

<span data-ttu-id="5c26c-111">tooconfigure integração do AD do Azure com arquivos simples, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c26c-111">tooconfigure Azure AD integration with Flatter Files, you need hello following items:</span></span>

- <span data-ttu-id="5c26c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c26c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c26c-113">Uma assinatura do Flatter Files com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="5c26c-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c26c-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5c26c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c26c-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5c26c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c26c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5c26c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c26c-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c26c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c26c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5c26c-118">Scenario description</span></span>
<span data-ttu-id="5c26c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5c26c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c26c-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="5c26c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c26c-121">Adicionando arquivos simples da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5c26c-121">Adding Flatter Files from hello gallery</span></span>
2. <span data-ttu-id="5c26c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c26c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-hello-gallery"></a><span data-ttu-id="5c26c-123">Adicionando arquivos simples da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5c26c-123">Adding Flatter Files from hello gallery</span></span>
<span data-ttu-id="5c26c-124">integração de saudação tooconfigure de arquivos simples no AD do Azure, você precisa tooadd arquivos simples na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5c26c-124">tooconfigure hello integration of Flatter Files into Azure AD, you need tooadd Flatter Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5c26c-125">**tooadd arquivos simples da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5c26c-125">**tooadd Flatter Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c26c-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5c26c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c26c-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5c26c-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="5c26c-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5c26c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="5c26c-133">Na caixa de pesquisa hello, digite **arquivos simples**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-133">In hello search box, type **Flatter Files**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="5c26c-135">No painel de resultados de saudação, selecione **arquivos simples**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5c26c-135">In hello results panel, select **Flatter Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c26c-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c26c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c26c-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Flatter Files com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="5c26c-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5c26c-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em arquivos simples é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c26c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Flatter Files is tooa user in Azure AD.</span></span> <span data-ttu-id="5c26c-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em arquivos simples deve toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="5c26c-140">In other words, a link relationship between an Azure AD user and hello related user in Flatter Files needs toobe established.</span></span>

<span data-ttu-id="5c26c-141">Em arquivos simples, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c26c-141">In Flatter Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5c26c-142">tooconfigure e teste de logon único do AD do Azure com arquivos simples, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c26c-142">tooconfigure and test Azure AD single sign-on with Flatter Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5c26c-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5c26c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5c26c-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c26c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c26c-145">**[Criar um usuário de teste de arquivos simples](#creating-a-flatter-files-test-user)**  -toohave um equivalente do Britta Simon em arquivos simples que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="5c26c-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - toohave a counterpart of Britta Simon in Flatter Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c26c-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="5c26c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c26c-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="5c26c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c26c-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c26c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c26c-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de arquivos simples.</span><span class="sxs-lookup"><span data-stu-id="5c26c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="5c26c-150">**tooconfigure AD do Azure-logon único com arquivos simples, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5c26c-150">**tooconfigure Azure AD single sign-on with Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c26c-151">Em Olá portal do Azure, Olá **arquivos simples** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-151">In hello Azure portal, on hello **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="5c26c-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="5c26c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="5c26c-155">Em Olá **domínio mais simples de arquivos e URLs** seção, hello usuário não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure.</span><span class="sxs-lookup"><span data-stu-id="5c26c-155">On hello **Flatter Files Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="5c26c-157">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5c26c-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="5c26c-159">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5c26c-159">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5c26c-161">Em Olá **configuração mais simples de arquivos** seção, clique em **configurar arquivos simples** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="5c26c-161">On hello **Flatter Files Configuration** section, click **Configure Flatter Files** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5c26c-162">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="5c26c-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="5c26c-164">Logon tooyour aplicativo de arquivos simples como um administrador.</span><span class="sxs-lookup"><span data-stu-id="5c26c-164">Sign-on tooyour Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="5c26c-165">Clique em **PAINEL**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-165">Click **DASHBOARD**.</span></span> 
   
    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="5c26c-167">Clique em **configurações**e, em seguida, executar Olá seguindo as etapas na Olá **empresa** guia:</span><span class="sxs-lookup"><span data-stu-id="5c26c-167">Click **Settings**, and then perform hello following steps on hello **Company** tab:</span></span> 
   
    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="5c26c-169">a.</span><span class="sxs-lookup"><span data-stu-id="5c26c-169">a.</span></span> <span data-ttu-id="5c26c-170">Selecione **Usar SAML 2.0 para Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="5c26c-171">b.</span><span class="sxs-lookup"><span data-stu-id="5c26c-171">b.</span></span> <span data-ttu-id="5c26c-172">Clique em **Configurar SAML**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="5c26c-173">Em Olá **configuração SAML** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c26c-173">On hello **SAML Configuration** dialog, perform hello following steps:</span></span> 
   
    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="5c26c-175">a.</span><span class="sxs-lookup"><span data-stu-id="5c26c-175">a.</span></span> <span data-ttu-id="5c26c-176">Em Olá **domínio** caixa de texto, digite o domínio registrado.</span><span class="sxs-lookup"><span data-stu-id="5c26c-176">In hello **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="5c26c-177">Se não tiver um domínio registrado, entre em contato com a equipe de suporte do Flatter Files pelo email [support@flatterfiles.com](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="5c26c-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="5c26c-178">b.</span><span class="sxs-lookup"><span data-stu-id="5c26c-178">b.</span></span> <span data-ttu-id="5c26c-179">Em **URL do provedor de identidade** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou formam o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c26c-179">In **Identity Provider URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="5c26c-180">c.</span><span class="sxs-lookup"><span data-stu-id="5c26c-180">c.</span></span>  <span data-ttu-id="5c26c-181">Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="5c26c-181">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="5c26c-182">d.</span><span class="sxs-lookup"><span data-stu-id="5c26c-182">d.</span></span> <span data-ttu-id="5c26c-183">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="5c26c-184">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="5c26c-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5c26c-185">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="5c26c-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5c26c-186">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c26c-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c26c-187">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c26c-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c26c-188">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c26c-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="5c26c-190">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5c26c-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c26c-191">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5c26c-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c26c-193">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c26c-195">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c26c-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c26c-197">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c26c-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c26c-199">a.</span><span class="sxs-lookup"><span data-stu-id="5c26c-199">a.</span></span> <span data-ttu-id="5c26c-200">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c26c-201">b.</span><span class="sxs-lookup"><span data-stu-id="5c26c-201">b.</span></span> <span data-ttu-id="5c26c-202">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5c26c-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c26c-203">c.</span><span class="sxs-lookup"><span data-stu-id="5c26c-203">c.</span></span> <span data-ttu-id="5c26c-204">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5c26c-205">d.</span><span class="sxs-lookup"><span data-stu-id="5c26c-205">d.</span></span> <span data-ttu-id="5c26c-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="5c26c-207">Criação de um usuário de teste do Flatter Files</span><span class="sxs-lookup"><span data-stu-id="5c26c-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="5c26c-208">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon em arquivos simples.</span><span class="sxs-lookup"><span data-stu-id="5c26c-208">hello objective of this section is toocreate a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="5c26c-209">**toocreate um usuário chamado Britta Simon em arquivos simples, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5c26c-209">**toocreate a user called Britta Simon in Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c26c-210">Logon tooyour **arquivos simples** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="5c26c-210">Sign on tooyour **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="5c26c-211">No painel de navegação Olá Olá esquerda, clique em **configurações**e, em seguida, clique em Olá **usuários** guia.</span><span class="sxs-lookup"><span data-stu-id="5c26c-211">In hello navigation pane on hello left, click **Settings**, and then click hello **Users** tab.</span></span>
   
    ![Criar um usuário do Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="5c26c-213">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="5c26c-214">Em Olá **adicionar usuário** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5c26c-214">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    ![Criar um usuário do Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="5c26c-216">a.</span><span class="sxs-lookup"><span data-stu-id="5c26c-216">a.</span></span> <span data-ttu-id="5c26c-217">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-217">In hello **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="5c26c-218">b.</span><span class="sxs-lookup"><span data-stu-id="5c26c-218">b.</span></span> <span data-ttu-id="5c26c-219">Em Olá **Sobrenome** caixa de texto, tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-219">In hello **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="5c26c-220">c.</span><span class="sxs-lookup"><span data-stu-id="5c26c-220">c.</span></span> <span data-ttu-id="5c26c-221">Em Olá **endereço de Email** caixa de texto, digite o endereço de email de Britta Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c26c-221">In hello **Email Address** textbox, type Britta's email address in hello Azure portal.</span></span>
   
    <span data-ttu-id="5c26c-222">d.</span><span class="sxs-lookup"><span data-stu-id="5c26c-222">d.</span></span> <span data-ttu-id="5c26c-223">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-223">Click **Submit**.</span></span>   


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5c26c-224">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c26c-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5c26c-225">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooFlatter arquivos.</span><span class="sxs-lookup"><span data-stu-id="5c26c-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFlatter Files.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="5c26c-227">**tooassign Britta Simon tooFlatter arquivos, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5c26c-227">**tooassign Britta Simon tooFlatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c26c-228">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5c26c-230">Na lista de aplicativos hello, selecione **arquivos simples**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-230">In hello applications list, select **Flatter Files**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="5c26c-232">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="5c26c-234">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5c26c-234">Click **Add** button.</span></span> <span data-ttu-id="5c26c-235">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5c26c-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="5c26c-237">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c26c-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5c26c-238">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5c26c-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c26c-239">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5c26c-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c26c-240">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="5c26c-240">Testing single sign-on</span></span>

<span data-ttu-id="5c26c-241">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c26c-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5c26c-242">Quando você clica em Olá bloco de arquivos simples no hello painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de arquivos simples.</span><span class="sxs-lookup"><span data-stu-id="5c26c-242">When you click hello Flatter Files tile in hello Access Panel, you should get automatically signed-on tooyour Flatter Files application.</span></span>
<span data-ttu-id="5c26c-243">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5c26c-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c26c-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5c26c-244">Additional resources</span></span>

* [<span data-ttu-id="5c26c-245">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5c26c-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c26c-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5c26c-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

