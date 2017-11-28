---
title: "Tutorial: integração do Azure Active Directory com o Hosted Graphite | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e grafite hospedado."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: d8914f6417ba8fbdef1a48e1b36635200ba130d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a><span data-ttu-id="ede8e-103">Tutorial: integração do Azure Active Directory ao Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="ede8e-103">Tutorial: Azure Active Directory integration with Hosted Graphite</span></span>

<span data-ttu-id="ede8e-104">Neste tutorial, você aprenderá como toointegrate grafite hospedado no Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="ede8e-104">In this tutorial, you learn how toointegrate Hosted Graphite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ede8e-105">Integrando grafite hospedado do Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="ede8e-105">Integrating Hosted Graphite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ede8e-106">Você pode controlar no AD do Azure que tenha acesso tooHosted grafite</span><span class="sxs-lookup"><span data-stu-id="ede8e-106">You can control in Azure AD who has access tooHosted Graphite</span></span>
- <span data-ttu-id="ede8e-107">Você pode habilitar seu usuários tooautomatically get conectado tooHosted grafite (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ede8e-107">You can enable your users tooautomatically get signed-on tooHosted Graphite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ede8e-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ede8e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ede8e-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ede8e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ede8e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ede8e-110">Prerequisites</span></span>

<span data-ttu-id="ede8e-111">tooconfigure integração do AD do Azure com grafite hospedado, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="ede8e-111">tooconfigure Azure AD integration with Hosted Graphite, you need hello following items:</span></span>

- <span data-ttu-id="ede8e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ede8e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ede8e-113">Uma assinatura do Hosted Graphite habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="ede8e-113">A Hosted Graphite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ede8e-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ede8e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ede8e-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ede8e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ede8e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ede8e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ede8e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ede8e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ede8e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ede8e-118">Scenario description</span></span>
<span data-ttu-id="ede8e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ede8e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ede8e-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="ede8e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ede8e-121">Adicionando hospedado grafite da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ede8e-121">Adding Hosted Graphite from hello gallery</span></span>
2. <span data-ttu-id="ede8e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ede8e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hosted-graphite-from-hello-gallery"></a><span data-ttu-id="ede8e-123">Adicionando hospedado grafite da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ede8e-123">Adding Hosted Graphite from hello gallery</span></span>
<span data-ttu-id="ede8e-124">integração de saudação tooconfigure do grafite hospedado no Azure AD, é necessário tooadd grafite hospedado na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ede8e-124">tooconfigure hello integration of Hosted Graphite into Azure AD, you need tooadd Hosted Graphite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ede8e-125">**tooadd grafite hospedado na Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ede8e-125">**tooadd Hosted Graphite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ede8e-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ede8e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ede8e-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ede8e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ede8e-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ede8e-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ede8e-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ede8e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ede8e-133">Na caixa de pesquisa hello, digite **hospedado grafite**.</span><span class="sxs-lookup"><span data-stu-id="ede8e-133">In hello search box, type **Hosted Graphite**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. <span data-ttu-id="ede8e-135">No painel de resultados de saudação, selecione **hospedado grafite**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ede8e-135">In hello results panel, select **Hosted Graphite**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ede8e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ede8e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ede8e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Hosted Graphite com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="ede8e-138">In this section, you configure and test Azure AD single sign-on with Hosted Graphite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ede8e-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte de saudação em grafite hospedado é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ede8e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hosted Graphite is tooa user in Azure AD.</span></span> <span data-ttu-id="ede8e-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em grafite hospedado precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ede8e-140">In other words, a link relationship between an Azure AD user and hello related user in Hosted Graphite needs toobe established.</span></span>

<span data-ttu-id="ede8e-141">Grafite hospedado, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="ede8e-141">In Hosted Graphite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ede8e-142">tooconfigure e teste de logon único do AD do Azure com grafite hospedado, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="ede8e-142">tooconfigure and test Azure AD single sign-on with Hosted Graphite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ede8e-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ede8e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ede8e-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ede8e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ede8e-145">**[Criar um usuário de teste hospedado grafite](#creating-a-hosted-graphite-test-user)**  -toohave um equivalente do Britta Simon em grafite hospedado que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="ede8e-145">**[Creating a Hosted Graphite test user](#creating-a-hosted-graphite-test-user)** - toohave a counterpart of Britta Simon in Hosted Graphite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ede8e-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="ede8e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ede8e-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="ede8e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ede8e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ede8e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ede8e-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo hospedado grafite.</span><span class="sxs-lookup"><span data-stu-id="ede8e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hosted Graphite application.</span></span>

<span data-ttu-id="ede8e-150">**tooconfigure AD do Azure-logon único com grafite hospedado, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ede8e-150">**tooconfigure Azure AD single sign-on with Hosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="ede8e-151">Em Olá portal do Azure, Olá **hospedado grafite** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="ede8e-151">In hello Azure portal, on hello **Hosted Graphite** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ede8e-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="ede8e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. <span data-ttu-id="ede8e-155">Em Olá **hospedado grafite domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ede8e-155">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    <span data-ttu-id="ede8e-157">a.</span><span class="sxs-lookup"><span data-stu-id="ede8e-157">a.</span></span> <span data-ttu-id="ede8e-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.hostedgraphite.com/metadata/<user id>`</span><span class="sxs-lookup"><span data-stu-id="ede8e-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/metadata/<user id>`</span></span>

    <span data-ttu-id="ede8e-159">b.</span><span class="sxs-lookup"><span data-stu-id="ede8e-159">b.</span></span> <span data-ttu-id="ede8e-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.hostedgraphite.com/complete/saml/<user id>`</span><span class="sxs-lookup"><span data-stu-id="ede8e-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/complete/saml/<user id>`</span></span>

4. <span data-ttu-id="ede8e-161">Em Olá **hospedado grafite domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ede8e-161">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    <span data-ttu-id="ede8e-163">a.</span><span class="sxs-lookup"><span data-stu-id="ede8e-163">a.</span></span> <span data-ttu-id="ede8e-164">Clique em Olá **Mostrar configurações de URL avançadas** opção</span><span class="sxs-lookup"><span data-stu-id="ede8e-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="ede8e-165">b.</span><span class="sxs-lookup"><span data-stu-id="ede8e-165">b.</span></span> <span data-ttu-id="ede8e-166">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.hostedgraphite.com/login/saml/<user id>/`</span><span class="sxs-lookup"><span data-stu-id="ede8e-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/login/saml/<user id>/`</span></span>   

    > [!NOTE] 
    > <span data-ttu-id="ede8e-167">Observe que esses não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="ede8e-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="ede8e-168">Você tem tooupdate esses valores com hello identificador real, a URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="ede8e-168">You have tooupdate these values with hello actual Identifier, Reply URL and Sign On URL.</span></span> <span data-ttu-id="ede8e-169">tooget esses valores, você pode ir tooAccess -> Configuração SAML no lado do aplicativo ou entre em contato com [a equipe de suporte hospedado grafite](mailto:help@hostedgraphite.com).</span><span class="sxs-lookup"><span data-stu-id="ede8e-169">tooget these values, you can go tooAccess->SAML setup on your Application side or Contact [Hosted Graphite support team](mailto:help@hostedgraphite.com).</span></span>
    >
 
5. <span data-ttu-id="ede8e-170">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ede8e-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. <span data-ttu-id="ede8e-172">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ede8e-172">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ede8e-174">Em Olá **hospedado grafite configuração** seção, clique em **configurar grafite hospedado** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="ede8e-174">On hello **Hosted Graphite Configuration** section, click **Configure Hosted Graphite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ede8e-175">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="ede8e-175">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. <span data-ttu-id="ede8e-177">Locatário de grafite hospedado tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="ede8e-177">Sign-on tooyour Hosted Graphite tenant as an administrator.</span></span>

9. <span data-ttu-id="ede8e-178">Vá toohello **página de instalação do SAML** na lateral da saudação (**acesso -> instalação do SAML**).</span><span class="sxs-lookup"><span data-stu-id="ede8e-178">Go toohello **SAML Setup page** in hello sidebar (**Access -> SAML Setup**).</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. <span data-ttu-id="ede8e-180">Confirmar essas URls corresponderá à configuração feita na Olá **hospedado grafite domínio e URLs** seção Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ede8e-180">Confirm these URls match your configuration done on hello **Hosted Graphite Domain and URLs** section of hello Azure portal.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. <span data-ttu-id="ede8e-182">Em **entidade ou ID do emissor** e **URL de logon SSO** caixas de texto, cole o valor de saudação do **ID da entidade SAML** e **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ede8e-182">In  **Entity or Issuer ID** and **SSO Login URL** textboxes, paste hello value of **SAML Entity ID** and **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. <span data-ttu-id="ede8e-184">Selecione "**Somente leitura**" como a **Função de usuário padrão**.</span><span class="sxs-lookup"><span data-stu-id="ede8e-184">Select "**Read-only**" as **Default User Role**.</span></span>
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. <span data-ttu-id="ede8e-186">Abra seu certificado codificado em base 64 no bloco de notas que baixou do portal do Azure, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="ede8e-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. <span data-ttu-id="ede8e-188">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ede8e-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="ede8e-189">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="ede8e-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ede8e-190">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ede8e-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ede8e-191">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ede8e-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ede8e-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ede8e-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="ede8e-193">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ede8e-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ede8e-195">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ede8e-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ede8e-196">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ede8e-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ede8e-198">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="ede8e-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ede8e-200">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ede8e-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ede8e-202">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ede8e-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ede8e-204">a.</span><span class="sxs-lookup"><span data-stu-id="ede8e-204">a.</span></span> <span data-ttu-id="ede8e-205">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ede8e-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ede8e-206">b.</span><span class="sxs-lookup"><span data-stu-id="ede8e-206">b.</span></span> <span data-ttu-id="ede8e-207">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ede8e-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ede8e-208">c.</span><span class="sxs-lookup"><span data-stu-id="ede8e-208">c.</span></span> <span data-ttu-id="ede8e-209">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="ede8e-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ede8e-210">d.</span><span class="sxs-lookup"><span data-stu-id="ede8e-210">d.</span></span> <span data-ttu-id="ede8e-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ede8e-211">Click **Create**.</span></span>
 
### <a name="creating-a-hosted-graphite-test-user"></a><span data-ttu-id="ede8e-212">Criação de um usuário de teste no Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="ede8e-212">Creating a Hosted Graphite test user</span></span>

<span data-ttu-id="ede8e-213">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no grafite hospedado.</span><span class="sxs-lookup"><span data-stu-id="ede8e-213">hello objective of this section is toocreate a user called Britta Simon in Hosted Graphite.</span></span> <span data-ttu-id="ede8e-214">O Hosted Graphite dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="ede8e-214">Hosted Graphite supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ede8e-215">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="ede8e-215">There is no action item for you in this section.</span></span> <span data-ttu-id="ede8e-216">Será criado um novo usuário durante uma tentativa tooaccess hospedado grafite se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="ede8e-216">A new user will be created during an attempt tooaccess Hosted Graphite if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="ede8e-217">Se você precisar toocreate um usuário manualmente, você precisa toocontact Olá grafite hospedado a equipe de suporte via < mailto:help@hostedgraphite.com >.</span><span class="sxs-lookup"><span data-stu-id="ede8e-217">If you need toocreate a user manually, you need toocontact hello Hosted Graphite support team via <mailto:help@hostedgraphite.com>.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ede8e-218">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ede8e-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ede8e-219">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHosted grafite.</span><span class="sxs-lookup"><span data-stu-id="ede8e-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHosted Graphite.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ede8e-221">**tooassign Britta Simon tooHosted grafite, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ede8e-221">**tooassign Britta Simon tooHosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="ede8e-222">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ede8e-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ede8e-224">Na lista de aplicativos hello, selecione **hospedado grafite**.</span><span class="sxs-lookup"><span data-stu-id="ede8e-224">In hello applications list, select **Hosted Graphite**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. <span data-ttu-id="ede8e-226">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ede8e-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ede8e-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ede8e-228">Click **Add** button.</span></span> <span data-ttu-id="ede8e-229">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ede8e-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ede8e-231">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="ede8e-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ede8e-232">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ede8e-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ede8e-233">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ede8e-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ede8e-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ede8e-234">Testing single sign-on</span></span>

<span data-ttu-id="ede8e-235">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="ede8e-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ede8e-236">Quando você clica em bloco hospedado grafite Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de grafite hospedado.</span><span class="sxs-lookup"><span data-stu-id="ede8e-236">When you click hello Hosted Graphite tile in hello Access Panel, you should get automatically signed-on tooyour Hosted Graphite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ede8e-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ede8e-237">Additional resources</span></span>

* [<span data-ttu-id="ede8e-238">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ede8e-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ede8e-239">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ede8e-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png

