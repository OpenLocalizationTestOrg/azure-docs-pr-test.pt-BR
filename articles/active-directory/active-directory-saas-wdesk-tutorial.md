---
title: "Tutorial: Integração do Azure Active Directory ao Wdesk | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="9cf0f-103">Tutorial: Integração do Azure Active Directory ao Wdesk</span><span class="sxs-lookup"><span data-stu-id="9cf0f-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="9cf0f-104">Neste tutorial, você aprenderá como toointegrate Wdesk com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="9cf0f-104">In this tutorial, you learn how toointegrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9cf0f-105">Integrando Wdesk com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-105">Integrating Wdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9cf0f-106">Você pode controlar no AD do Azure que tenha acesso tooWdesk</span><span class="sxs-lookup"><span data-stu-id="9cf0f-106">You can control in Azure AD who has access tooWdesk</span></span>
- <span data-ttu-id="9cf0f-107">Você pode habilitar seu usuários tooautomatically get conectado tooWdesk (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9cf0f-107">You can enable your users tooautomatically get signed-on tooWdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9cf0f-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9cf0f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9cf0f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="9cf0f-110">[O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9cf0f-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cf0f-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9cf0f-111">Prerequisites</span></span>

<span data-ttu-id="9cf0f-112">tooconfigure integração do AD do Azure com Wdesk, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-112">tooconfigure Azure AD integration with Wdesk, you need hello following items:</span></span>

- <span data-ttu-id="9cf0f-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9cf0f-113">An Azure AD subscription</span></span>
- <span data-ttu-id="9cf0f-114">Uma assinatura do Wdesk habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="9cf0f-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9cf0f-115">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9cf0f-116">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9cf0f-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9cf0f-118">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9cf0f-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9cf0f-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9cf0f-119">Scenario description</span></span>
<span data-ttu-id="9cf0f-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9cf0f-121">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9cf0f-122">Adicionando Wdesk da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9cf0f-122">Adding Wdesk from hello gallery</span></span>
2. <span data-ttu-id="9cf0f-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9cf0f-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-hello-gallery"></a><span data-ttu-id="9cf0f-124">Adicionando Wdesk da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9cf0f-124">Adding Wdesk from hello gallery</span></span>
<span data-ttu-id="9cf0f-125">integração de saudação tooconfigure de Wdesk no AD do Azure, você precisa tooadd Wdesk da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-125">tooconfigure hello integration of Wdesk into Azure AD, you need tooadd Wdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9cf0f-126">**tooadd Wdesk da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9cf0f-126">**tooadd Wdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf0f-127">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9cf0f-129">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9cf0f-130">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-130">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9cf0f-132">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9cf0f-134">Na caixa de pesquisa hello, digite **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-134">In hello search box, type **Wdesk**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="9cf0f-136">No painel de resultados de saudação, selecione **Wdesk**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-136">In hello results panel, select **Wdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9cf0f-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9cf0f-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9cf0f-139">Nesta seção, você configurará e testará o logon único do Azure AD com o Wdesk, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9cf0f-140">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Wdesk é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="9cf0f-141">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Wdesk precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-141">In other words, a link relationship between an Azure AD user and hello related user in Wdesk needs toobe established.</span></span>

<span data-ttu-id="9cf0f-142">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Wdesk.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wdesk.</span></span>

<span data-ttu-id="9cf0f-143">tooconfigure e teste de logon único do AD do Azure com Wdesk, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-143">tooconfigure and test Azure AD single sign-on with Wdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9cf0f-144">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9cf0f-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9cf0f-146">**[Criar um usuário de teste Wdesk](#creating-a-wdesk-test-user)**  -toohave um equivalente do Britta Simon em Wdesk é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - toohave a counterpart of Britta Simon in Wdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9cf0f-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9cf0f-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9cf0f-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf0f-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9cf0f-150">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Wdesk.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="9cf0f-151">**tooconfigure AD do Azure-logon único com Wdesk, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9cf0f-151">**tooconfigure Azure AD single sign-on with Wdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf0f-152">Em Olá portal do Azure, Olá **Wdesk** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-152">In hello Azure portal, on hello **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9cf0f-154">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="9cf0f-156">Em Olá **Wdesk domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-156">On hello **Wdesk Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="9cf0f-158">a.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-158">a.</span></span> <span data-ttu-id="9cf0f-159">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="9cf0f-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="9cf0f-160">b.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-160">b.</span></span> <span data-ttu-id="9cf0f-161">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="9cf0f-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="9cf0f-162">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="9cf0f-163">Se desejar que o aplicativo hello tooconfigure **SP** iniciada modo, executar Olá etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-163">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following step:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="9cf0f-165">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="9cf0f-165">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9cf0f-166">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-166">These values are not real.</span></span> <span data-ttu-id="9cf0f-167">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9cf0f-168">Você pode obter esses valores do portal de WDesk quando você configura Olá SSO.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-168">You get these values from WDesk portal when you configure hello SSO.</span></span> 
  
5. <span data-ttu-id="9cf0f-169">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="9cf0f-171">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9cf0f-171">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9cf0f-173">Em uma janela de navegador web diferente, tooWdesk logon como um administrador de segurança.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-173">In a different web browser window, login tooWdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="9cf0f-174">No hello parte inferior esquerda, clique em **Admin** e escolha **administrador da conta**:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-174">In hello bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Configurar Logon Único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="9cf0f-176">Wdesk administrador, navegue muito**segurança**, em seguida, **SAML** > **configurações SAML**:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-176">In Wdesk Admin, navigate too**Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="9cf0f-178">Em **configurações gerais**, verificar Olá **habilitar SAML logon único**:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-178">Under **General Settings**, check hello **Enable SAML Single Sign On**:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="9cf0f-180">Em **detalhes do provedor de serviço**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-180">Under **Service Provider Details**, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="9cf0f-182">a.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-182">a.</span></span> <span data-ttu-id="9cf0f-183">Saudação de cópia **URL de logon** e cole-o na **Url de logon** caixa de texto no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-183">Copy hello **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="9cf0f-184">b.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-184">b.</span></span> <span data-ttu-id="9cf0f-185">Saudação de cópia **Url de metadados** e cole-o na **identificador** caixa de texto no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-185">Copy hello **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="9cf0f-186">c.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-186">c.</span></span> <span data-ttu-id="9cf0f-187">Saudação de cópia **consumidor url** e cole-o na **Url de resposta** caixa de texto no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-187">Copy hello **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="9cf0f-188">d.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-188">d.</span></span> <span data-ttu-id="9cf0f-189">Clique em **salvar** nas alterações de saudação toosave portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-189">Click **Save** on Azure portal toosave hello changes.</span></span>      

12. <span data-ttu-id="9cf0f-190">Clique em **IdP configurar** tooopen **editar configurações de IdP** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-190">Click **Configure IdP Settings** tooopen **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="9cf0f-191">Clique em **Escolher arquivo** toolocate Olá **Metadata.xml** arquivo salvo no portal do Azure, em seguida, carregá-lo.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-191">Click **Choose File** toolocate hello **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="9cf0f-193">Clique em **Salvar alterações**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-193">Click **Save changes**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="9cf0f-195">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="9cf0f-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9cf0f-196">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9cf0f-197">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9cf0f-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9cf0f-198">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9cf0f-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="9cf0f-199">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9cf0f-201">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9cf0f-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf0f-202">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9cf0f-204">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9cf0f-206">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9cf0f-208">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9cf0f-210">a.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-210">a.</span></span> <span data-ttu-id="9cf0f-211">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9cf0f-212">b.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-212">b.</span></span> <span data-ttu-id="9cf0f-213">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9cf0f-214">c.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-214">c.</span></span> <span data-ttu-id="9cf0f-215">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9cf0f-216">d.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-216">d.</span></span> <span data-ttu-id="9cf0f-217">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="9cf0f-218">Criar um usuário de teste do Wdesk</span><span class="sxs-lookup"><span data-stu-id="9cf0f-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="9cf0f-219">tooenable AD do Azure usuários toolog em tooWdesk, eles devem ser provisionados no Wdesk.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-219">tooenable Azure AD users toolog in tooWdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="9cf0f-220">No Wdesk, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="9cf0f-221">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9cf0f-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf0f-222">Faça logon em tooWdesk como um administrador de segurança.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-222">Log in tooWdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="9cf0f-223">Navegue muito**Admin** > **conta de administrador**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-223">Navigate too**Admin** > **Account Admin**.</span></span>

     ![Configurar Logon Único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="9cf0f-225">Clique em **Membros**, sob **Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="9cf0f-226">Agora clique **Adicionar membro** tooopen **Adicionar membro** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-226">Now click **Add Member** tooopen **Add Member** dialog box.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="9cf0f-228">Em **usuário** texto, digite o nome de usuário de saudação do usuário como  **brittasimon@contoso.com**  e clique em **continuar** botão.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-228">In **User** text box, enter hello username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="9cf0f-230">Insira os detalhes de saudação conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-230">Enter hello details as shown below:</span></span>
  
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="9cf0f-232">a.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-232">a.</span></span> <span data-ttu-id="9cf0f-233">Em **email** texto, digite o email de saudação do usuário como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="9cf0f-233">In **E-mail** text box, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="9cf0f-234">b.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-234">b.</span></span> <span data-ttu-id="9cf0f-235">Em **nome** texto, digite o nome saudação do usuário como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-235">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="9cf0f-236">c.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-236">c.</span></span> <span data-ttu-id="9cf0f-237">Em **Sobrenome** texto, digite o sobrenome de saudação do usuário como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-237">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

7. <span data-ttu-id="9cf0f-238">Clique no botão **Salvar Membro**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-238">Click **Save Member** button.</span></span>  

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9cf0f-240">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9cf0f-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9cf0f-241">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWdesk.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWdesk.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9cf0f-243">**tooassign Britta Simon tooWdesk, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9cf0f-243">**tooassign Britta Simon tooWdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf0f-244">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9cf0f-246">Na lista de aplicativos hello, selecione **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-246">In hello applications list, select **Wdesk**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="9cf0f-248">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9cf0f-250">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-250">Click **Add** button.</span></span> <span data-ttu-id="9cf0f-251">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9cf0f-253">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9cf0f-254">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9cf0f-255">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9cf0f-256">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9cf0f-256">Testing single sign-on</span></span>

<span data-ttu-id="9cf0f-257">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-257">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9cf0f-258">Quando você clica em bloco Wdesk Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Wdesk aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-258">When you click hello Wdesk tile in hello Access Panel, you should get automatically signed-on tooyour Wdesk application.</span></span>
<span data-ttu-id="9cf0f-259">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9cf0f-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9cf0f-260">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9cf0f-260">Additional resources</span></span>

* [<span data-ttu-id="9cf0f-261">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9cf0f-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cf0f-262">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9cf0f-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

