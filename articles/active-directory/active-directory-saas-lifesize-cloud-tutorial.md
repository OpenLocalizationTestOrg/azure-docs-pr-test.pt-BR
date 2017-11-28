---
title: "Tutorial: integração do Azure Active Directory ao Lifesize Cloud | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e a nuvem Lifesize."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="0dff8-103">Tutorial: Integração do Azure Active Directory com o Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="0dff8-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="0dff8-104">Neste tutorial, você aprenderá como toointegrate Lifesize nuvem com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="0dff8-104">In this tutorial, you learn how toointegrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0dff8-105">Integrando Lifesize nuvem com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dff8-105">Integrating Lifesize Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0dff8-106">Você pode controlar no AD do Azure que tenha acesso tooLifesize nuvem</span><span class="sxs-lookup"><span data-stu-id="0dff8-106">You can control in Azure AD who has access tooLifesize Cloud</span></span>
- <span data-ttu-id="0dff8-107">Você pode habilitar seu usuários tooautomatically get conectado tooLifesize nuvem (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0dff8-107">You can enable your users tooautomatically get signed-on tooLifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0dff8-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0dff8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0dff8-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0dff8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dff8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0dff8-110">Prerequisites</span></span>

<span data-ttu-id="0dff8-111">tooconfigure integração do AD do Azure com Lifesize nuvem, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dff8-111">tooconfigure Azure AD integration with Lifesize Cloud, you need hello following items:</span></span>

- <span data-ttu-id="0dff8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0dff8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0dff8-113">Uma assinatura habilitada para logon único do Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="0dff8-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0dff8-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0dff8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0dff8-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0dff8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0dff8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0dff8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0dff8-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0dff8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0dff8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0dff8-118">Scenario description</span></span>
<span data-ttu-id="0dff8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0dff8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0dff8-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="0dff8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0dff8-121">Adicionando Lifesize nuvem da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0dff8-121">Adding Lifesize Cloud from hello gallery</span></span>
2. <span data-ttu-id="0dff8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0dff8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-hello-gallery"></a><span data-ttu-id="0dff8-123">Adicionando Lifesize nuvem da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0dff8-123">Adding Lifesize Cloud from hello gallery</span></span>
<span data-ttu-id="0dff8-124">integração de saudação tooconfigure da nuvem Lifesize no AD do Azure, você precisa tooadd Lifesize nuvem na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0dff8-124">tooconfigure hello integration of Lifesize Cloud into Azure AD, you need tooadd Lifesize Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0dff8-125">**tooadd Lifesize nuvem da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0dff8-125">**tooadd Lifesize Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dff8-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0dff8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0dff8-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0dff8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0dff8-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0dff8-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="0dff8-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0dff8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="0dff8-133">Na caixa de pesquisa hello, digite **Lifesize nuvem**.</span><span class="sxs-lookup"><span data-stu-id="0dff8-133">In hello search box, type **Lifesize Cloud**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="0dff8-135">No painel de resultados de saudação, selecione **Lifesize nuvem**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0dff8-135">In hello results panel, select **Lifesize Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0dff8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0dff8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0dff8-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Lifesize Cloud, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="0dff8-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0dff8-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na nuvem Lifesize é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0dff8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lifesize Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="0dff8-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na nuvem Lifesize precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="0dff8-140">In other words, a link relationship between an Azure AD user and hello related user in Lifesize Cloud needs toobe established.</span></span>

<span data-ttu-id="0dff8-141">Na nuvem Lifesize, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dff8-141">In Lifesize Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0dff8-142">tooconfigure e teste de logon único do AD do Azure com Lifesize nuvem, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dff8-142">tooconfigure and test Azure AD single sign-on with Lifesize Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0dff8-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0dff8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0dff8-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0dff8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0dff8-145">**[Criar um usuário de teste de nuvem Lifesize](#creating-a-lifesize-cloud-test-user)**  -toohave um equivalente do Britta Simon na nuvem Lifesize que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="0dff8-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - toohave a counterpart of Britta Simon in Lifesize Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0dff8-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="0dff8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0dff8-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="0dff8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0dff8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dff8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0dff8-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de nuvem Lifesize.</span><span class="sxs-lookup"><span data-stu-id="0dff8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="0dff8-150">**tooconfigure AD do Azure-logon único com Lifesize nuvem, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0dff8-150">**tooconfigure Azure AD single sign-on with Lifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dff8-151">Em Olá portal do Azure, Olá **Lifesize nuvem** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="0dff8-151">In hello Azure portal, on hello **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="0dff8-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="0dff8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="0dff8-155">Em Olá **Lifesize nuvem domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dff8-155">On hello **Lifesize Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="0dff8-157">a.</span><span class="sxs-lookup"><span data-stu-id="0dff8-157">a.</span></span> <span data-ttu-id="0dff8-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="0dff8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="0dff8-159">b.</span><span class="sxs-lookup"><span data-stu-id="0dff8-159">b.</span></span> <span data-ttu-id="0dff8-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="0dff8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="0dff8-161">Verificar **Mostrar configurações de URL avançadas**, executar Olá etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dff8-161">Check **Show advanced URL settings**, perform hello following step:</span></span>  
   
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="0dff8-163">Em Olá **estado de retransmissão** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="0dff8-163">In hello **Relay state** textbox, type a URL using hello following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="0dff8-164">Observe que esses não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dff8-164">Please note that these are not hello real values.</span></span> <span data-ttu-id="0dff8-165">Você tem tooupdate esses valores com hello real URL de logon, o estado de retransmissão e identificador.</span><span class="sxs-lookup"><span data-stu-id="0dff8-165">you have tooupdate these values with hello actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="0dff8-166">Entre em contato com [equipe de suporte do cliente de nuvem Lifesize](https://www.lifesize.com/support) tooget URL de logon e valores de identificador e você pode obter o valor de estado de retransmissão de configuração de SSO é explicado posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dff8-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) tooget Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in hello tutorial.</span></span>

4. <span data-ttu-id="0dff8-167">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0dff8-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="0dff8-169">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0dff8-169">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0dff8-171">Em Olá **configuração de nuvem Lifesize** seção, clique em **configurar Lifesize nuvem** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="0dff8-171">On hello **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0dff8-172">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="0dff8-172">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="0dff8-174">tooget SSO configurado para seu aplicativo, o logon em Olá aplicativos de nuvem Lifesize com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="0dff8-174">tooget SSO configured for your application, login into hello Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="0dff8-175">No hello canto superior direito clique em seu nome e, em seguida, clique em Olá **configurações avançadas**.</span><span class="sxs-lookup"><span data-stu-id="0dff8-175">In hello top right corner click on your name and then click on hello **Advance Settings**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="0dff8-177">Em Olá configurações avançadas agora, clique em Olá **configuração SSO** link.</span><span class="sxs-lookup"><span data-stu-id="0dff8-177">In hello Advance Settings now click on hello **SSO Configuration** link.</span></span> <span data-ttu-id="0dff8-178">Ele abrirá a página de configuração de SSO de saudação para sua instância.</span><span class="sxs-lookup"><span data-stu-id="0dff8-178">It will open hello SSO Configuration page for your instance.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="0dff8-180">Configure agora Olá valores na interface de configuração de SSO Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="0dff8-180">Now configure hello following values in hello SSO configuration UI.</span></span>    
   
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="0dff8-182">a.</span><span class="sxs-lookup"><span data-stu-id="0dff8-182">a.</span></span> <span data-ttu-id="0dff8-183">Em **emissor do provedor de identidade** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0dff8-183">In **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0dff8-184">b.</span><span class="sxs-lookup"><span data-stu-id="0dff8-184">b.</span></span>  <span data-ttu-id="0dff8-185">Em **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0dff8-185">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0dff8-186">c.</span><span class="sxs-lookup"><span data-stu-id="0dff8-186">c.</span></span> <span data-ttu-id="0dff8-187">Abra seu certificado codificado em base 64 no bloco de notas que baixou do portal do Azure, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="0dff8-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="0dff8-188">d.</span><span class="sxs-lookup"><span data-stu-id="0dff8-188">d.</span></span> <span data-ttu-id="0dff8-189">Em Olá SAML atributo mapeamentos para a caixa de texto Nome hello insira o valor de saudação como **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="0dff8-189">In hello SAML Attribute mappings for hello First Name text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="0dff8-190">e.</span><span class="sxs-lookup"><span data-stu-id="0dff8-190">e.</span></span> <span data-ttu-id="0dff8-191">No mapeamento de atributo de SAML Olá para Olá **Sobrenome** caixa de texto insira o valor de saudação como **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="0dff8-191">In hello SAML Attribute mapping for hello **Last Name** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="0dff8-192">f.</span><span class="sxs-lookup"><span data-stu-id="0dff8-192">f.</span></span> <span data-ttu-id="0dff8-193">No mapeamento de atributo de SAML Olá para Olá **Email** caixa de texto insira o valor de saudação como **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="0dff8-193">In hello SAML Attribute mapping for hello **Email** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="0dff8-194">configuração de saudação toocheck você pode clicar em Olá **teste** botão.</span><span class="sxs-lookup"><span data-stu-id="0dff8-194">toocheck hello configuration you can click on hello **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="0dff8-195">Para teste bem-sucedido, você precisa de Assistente de configuração de saudação toocomplete no AD do Azure e também fornecem acesso toousers ou grupos que podem executar o teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dff8-195">For successful testing you need toocomplete hello configuration wizard in Azure AD and also provide access toousers or groups who can perform hello test.</span></span>

12. <span data-ttu-id="0dff8-196">Habilitar Olá SSO verificando em Olá **habilitar SSO** botão.</span><span class="sxs-lookup"><span data-stu-id="0dff8-196">Enable hello SSO by checking on hello **Enable SSO** button.</span></span>

13. <span data-ttu-id="0dff8-197">Agora clique em Olá **atualização** botão para que todas as configurações de saudação são salvos.</span><span class="sxs-lookup"><span data-stu-id="0dff8-197">Now click on hello **Update** button so that all hello settings are saved.</span></span> <span data-ttu-id="0dff8-198">Isso irá gerar o valor de RelayState hello.</span><span class="sxs-lookup"><span data-stu-id="0dff8-198">This will generate hello RelayState value.</span></span> <span data-ttu-id="0dff8-199">Saudação de cópia RelayState valor, que é gerado na caixa de texto de saudação, cole-o em hello **retransmissão estado** textbox em **Lifesize nuvem domínio e URLs** seção.</span><span class="sxs-lookup"><span data-stu-id="0dff8-199">Copy hello RelayState value, which is generated in hello text box, paste it in hello **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="0dff8-200">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="0dff8-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0dff8-201">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="0dff8-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0dff8-202">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0dff8-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0dff8-203">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0dff8-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="0dff8-204">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0dff8-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="0dff8-206">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0dff8-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dff8-207">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0dff8-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0dff8-209">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="0dff8-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0dff8-211">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dff8-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0dff8-213">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dff8-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0dff8-215">a.</span><span class="sxs-lookup"><span data-stu-id="0dff8-215">a.</span></span> <span data-ttu-id="0dff8-216">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0dff8-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0dff8-217">b.</span><span class="sxs-lookup"><span data-stu-id="0dff8-217">b.</span></span> <span data-ttu-id="0dff8-218">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0dff8-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0dff8-219">c.</span><span class="sxs-lookup"><span data-stu-id="0dff8-219">c.</span></span> <span data-ttu-id="0dff8-220">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="0dff8-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0dff8-221">d.</span><span class="sxs-lookup"><span data-stu-id="0dff8-221">d.</span></span> <span data-ttu-id="0dff8-222">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0dff8-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="0dff8-223">Criação de um usuário de teste do Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="0dff8-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="0dff8-224">Nesta seção, você criará um usuário chamado Brenda Fernandes no Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="0dff8-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="0dff8-225">O Lifesize Cloud oferece suporte ao provisionamento automático de usuário.</span><span class="sxs-lookup"><span data-stu-id="0dff8-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="0dff8-226">Após a autenticação bem-sucedida no AD do Azure, usuário hello será provisionado no aplicativo hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0dff8-226">After successful authentication at Azure AD, hello user will be automatically provisioned in hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0dff8-227">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0dff8-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0dff8-228">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLifesize nuvem.</span><span class="sxs-lookup"><span data-stu-id="0dff8-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLifesize Cloud.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="0dff8-230">**tooassign Britta Simon tooLifesize nuvem, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0dff8-230">**tooassign Britta Simon tooLifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dff8-231">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0dff8-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0dff8-233">Na lista de aplicativos hello, selecione **Lifesize nuvem**.</span><span class="sxs-lookup"><span data-stu-id="0dff8-233">In hello applications list, select **Lifesize Cloud**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="0dff8-235">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0dff8-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="0dff8-237">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0dff8-237">Click **Add** button.</span></span> <span data-ttu-id="0dff8-238">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0dff8-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="0dff8-240">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dff8-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0dff8-241">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0dff8-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0dff8-242">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0dff8-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0dff8-243">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="0dff8-243">Testing single sign-on</span></span>

<span data-ttu-id="0dff8-244">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dff8-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0dff8-245">Quando você clica em nuvem Lifesize bloco no painel de acesso de saudação do hello, você deve obter a página de logon do aplicativo de nuvem Lifesize.</span><span class="sxs-lookup"><span data-stu-id="0dff8-245">When you click hello Lifesize Cloud tile in hello Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="0dff8-246">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0dff8-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0dff8-247">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0dff8-247">Additional resources</span></span>

* [<span data-ttu-id="0dff8-248">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0dff8-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0dff8-249">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0dff8-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

