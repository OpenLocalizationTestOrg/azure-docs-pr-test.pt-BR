---
title: "Tutorial: Integração do Azure Active Directory ao Velpic SAML | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Velpic SAML."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="8143e-103">Tutorial: Integração do Azure Active Directory ao Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="8143e-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="8143e-104">Neste tutorial, você aprenderá como toointegrate Velpic SAML com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="8143e-104">In this tutorial, you learn how toointegrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8143e-105">Integrando Velpic SAML com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="8143e-105">Integrating Velpic SAML with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8143e-106">Você pode controlar no AD do Azure que tenha acesso tooVelpic SAML</span><span class="sxs-lookup"><span data-stu-id="8143e-106">You can control in Azure AD who has access tooVelpic SAML</span></span>
- <span data-ttu-id="8143e-107">Você pode habilitar seu usuários tooautomatically get conectado tooVelpic SAML (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8143e-107">You can enable your users tooautomatically get signed-on tooVelpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8143e-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="8143e-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="8143e-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8143e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8143e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8143e-110">Prerequisites</span></span>

<span data-ttu-id="8143e-111">tooconfigure integração do AD do Azure com Velpic SAML, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="8143e-111">tooconfigure Azure AD integration with Velpic SAML, you need hello following items:</span></span>

- <span data-ttu-id="8143e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8143e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8143e-113">Uma assinatura do Velpic SAML habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="8143e-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8143e-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8143e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8143e-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8143e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8143e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8143e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8143e-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8143e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8143e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8143e-118">Scenario description</span></span>
<span data-ttu-id="8143e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8143e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8143e-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="8143e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8143e-121">Adicionando Velpic SAML da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8143e-121">Adding Velpic SAML from hello gallery</span></span>
2. <span data-ttu-id="8143e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8143e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-hello-gallery"></a><span data-ttu-id="8143e-123">Adicionando Velpic SAML da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8143e-123">Adding Velpic SAML from hello gallery</span></span>
<span data-ttu-id="8143e-124">integração de saudação tooconfigure do Velpic SAML no AD do Azure, você precisa tooadd Velpic SAML na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8143e-124">tooconfigure hello integration of Velpic SAML into Azure AD, you need tooadd Velpic SAML from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8143e-125">**tooadd Velpic SAML da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8143e-125">**tooadd Velpic SAML from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8143e-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8143e-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8143e-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8143e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8143e-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8143e-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8143e-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8143e-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8143e-133">Na caixa de pesquisa hello, digite **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="8143e-133">In hello search box, type **Velpic SAML**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="8143e-135">No painel de resultados de saudação, selecione **Velpic SAML**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8143e-135">In hello results panel, select **Velpic SAML**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8143e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8143e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8143e-138">Nesta seção, você configura e testa o logon único do Azure AD com o Velpic SAML, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="8143e-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8143e-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Velpic SAML é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8143e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Velpic SAML is tooa user in Azure AD.</span></span> <span data-ttu-id="8143e-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Velpic SAML precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="8143e-140">In other words, a link relationship between an Azure AD user and hello related user in Velpic SAML needs toobe established.</span></span>

<span data-ttu-id="8143e-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="8143e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Velpic SAML.</span></span>

<span data-ttu-id="8143e-142">tooconfigure e teste de logon único do AD do Azure com Velpic SAML, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="8143e-142">tooconfigure and test Azure AD single sign-on with Velpic SAML, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8143e-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8143e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8143e-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8143e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8143e-145">**[Criar um usuário de teste Velpic SAML](#creating-a-velpic-saml-test-user)**  -toohave um equivalente do Britta Simon no Velpic SAML que é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="8143e-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - toohave a counterpart of Britta Simon in Velpic SAML that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="8143e-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="8143e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8143e-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="8143e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8143e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8143e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8143e-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="8143e-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="8143e-150">**tooconfigure AD do Azure-logon único com SAML Velpic, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8143e-150">**tooconfigure Azure AD single sign-on with Velpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="8143e-151">No portal de gerenciamento do Azure do hello, no hello **Velpic SAML** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="8143e-151">In hello Azure Management portal, on hello **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8143e-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="8143e-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="8143e-155">Insira os detalhes de saudação em Olá **Velpic SAML domínio e URLs** seção -</span><span class="sxs-lookup"><span data-stu-id="8143e-155">Enter hello details in hello **Velpic SAML Domain and URLs** section-</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="8143e-157">a.</span><span class="sxs-lookup"><span data-stu-id="8143e-157">a.</span></span> <span data-ttu-id="8143e-158">Em Olá **URL de logon** texto, o valor do tipo hello como:`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="8143e-158">In hello **Sign-on URL** textbox, type hello value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="8143e-159">b.</span><span class="sxs-lookup"><span data-stu-id="8143e-159">b.</span></span> <span data-ttu-id="8143e-160">Em Olá **identificador** caixa de texto, colar Olá **'URL do logon único'** valor`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="8143e-160">In hello **Identifier** textbox, paste hello **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="8143e-161">Observe que Olá URL de logon será fornecida pelo Olá team Velpic SAML e o valor de identificador estarão disponível quando você configura Olá plug-in do SSO no lado Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="8143e-161">Please note that hello Sign on URL will be provided by hello Velpic SAML team and Identifier value will be available when you configure hello SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="8143e-162">É necessário toocopy que o valor da página de aplicativo Velpic SAML e cole-o aqui.</span><span class="sxs-lookup"><span data-stu-id="8143e-162">You need toocopy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="8143e-163">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8143e-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="8143e-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8143e-165">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8143e-167">No hello seção de configuração de SAML Velpic, clique em Configurar Velpic SAML tooopen configurar logon na janela.</span><span class="sxs-lookup"><span data-stu-id="8143e-167">On hello Velpic SAML Configuration section, click Configure Velpic SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="8143e-168">Copie Olá SAML ID da entidade de saudação seção de referência rápida.</span><span class="sxs-lookup"><span data-stu-id="8143e-168">Copy hello SAML Entity ID from hello Quick Reference section.</span></span>

7. <span data-ttu-id="8143e-169">Em uma janela diferente do navegador da Web, faça logon no site do Velpic SAML na sua empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="8143e-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="8143e-170">Clique em **gerenciar** guia e vá muito**integração** seção onde você precisa de tooclick em **plug-ins** botão toocreate novo plug-in para entrar.</span><span class="sxs-lookup"><span data-stu-id="8143e-170">Click on **Manage** tab and go too**Integration** section where you need tooclick on **Plugins** button toocreate new plugin for Sign-In.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="8143e-172">Clique em Olá **'Adicionar plug-in'** botão.</span><span class="sxs-lookup"><span data-stu-id="8143e-172">Click on hello **‘Add plugin’** button.</span></span>
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="8143e-174">Clique em Olá **SAML** lado a lado na página de adicionar plug-in de saudação.</span><span class="sxs-lookup"><span data-stu-id="8143e-174">Click on hello **SAML** tile in hello Add Plugin page.</span></span>
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="8143e-176">Insira nome de saudação do hello novo SAML plug-in e clique em Olá **'Add'** botão.</span><span class="sxs-lookup"><span data-stu-id="8143e-176">Enter hello name of hello new SAML plugin and click hello **‘Add’** button.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="8143e-178">Insira os detalhes de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8143e-178">Enter hello details as follows:</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="8143e-180">a.</span><span class="sxs-lookup"><span data-stu-id="8143e-180">a.</span></span> <span data-ttu-id="8143e-181">Em Olá **nome** caixa de texto Nome do tipo saudação do plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="8143e-181">In hello **Name** textbox, type hello name of SAML plugin.</span></span>

    <span data-ttu-id="8143e-182">b.</span><span class="sxs-lookup"><span data-stu-id="8143e-182">b.</span></span> <span data-ttu-id="8143e-183">Em hello **URL do emissor** textbox, colar Olá **ID da entidade SAML** você copiou da saudação **configurar o logon** janela de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8143e-183">In hello **Issuer URL** textbox, paste hello **SAML Entity ID** you copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="8143e-184">c.</span><span class="sxs-lookup"><span data-stu-id="8143e-184">c.</span></span> <span data-ttu-id="8143e-185">Em Olá **configuração do provedor de metadados** carregar Olá arquivo Metadata XML que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8143e-185">In hello **Provider Metadata Config** upload hello Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="8143e-186">d.</span><span class="sxs-lookup"><span data-stu-id="8143e-186">d.</span></span> <span data-ttu-id="8143e-187">Você também pode escolher tooenable SAML apenas durante o provisionamento, permitindo Olá **'Criação automática de novos usuários'** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="8143e-187">You can also choose tooenable SAML just in time provisioning by enabling hello **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="8143e-188">Se um usuário não existe no Velpic e esse sinalizador não estiver habilitado, o logon de saudação do Azure falhará.</span><span class="sxs-lookup"><span data-stu-id="8143e-188">If a user doesn’t exist in Velpic and this flag is not enabled, hello login from Azure will fail.</span></span> <span data-ttu-id="8143e-189">Se o sinalizador Olá será habilitado Olá usuário automaticamente ser provisionados no Velpic no tempo de saudação do logon.</span><span class="sxs-lookup"><span data-stu-id="8143e-189">If hello flag is enabled hello user will automatically be provisioned into Velpic at hello time of login.</span></span> 

    <span data-ttu-id="8143e-190">e.</span><span class="sxs-lookup"><span data-stu-id="8143e-190">e.</span></span> <span data-ttu-id="8143e-191">Saudação de cópia **URL do logon único** da caixa de texto de saudação e colar no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8143e-191">Copy hello **Single sign on URL** from hello text box and paste it in hello Azure portal.</span></span>
    
    <span data-ttu-id="8143e-192">f.</span><span class="sxs-lookup"><span data-stu-id="8143e-192">f.</span></span> <span data-ttu-id="8143e-193">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8143e-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8143e-194">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8143e-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="8143e-195">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8143e-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8143e-197">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8143e-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8143e-198">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8143e-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8143e-200">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="8143e-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8143e-202">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8143e-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8143e-204">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8143e-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8143e-206">a.</span><span class="sxs-lookup"><span data-stu-id="8143e-206">a.</span></span> <span data-ttu-id="8143e-207">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8143e-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8143e-208">b.</span><span class="sxs-lookup"><span data-stu-id="8143e-208">b.</span></span> <span data-ttu-id="8143e-209">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8143e-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8143e-210">c.</span><span class="sxs-lookup"><span data-stu-id="8143e-210">c.</span></span> <span data-ttu-id="8143e-211">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="8143e-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8143e-212">d.</span><span class="sxs-lookup"><span data-stu-id="8143e-212">d.</span></span> <span data-ttu-id="8143e-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8143e-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="8143e-214">Criando um usuário de teste no Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="8143e-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="8143e-215">Esta etapa geralmente não é necessária como aplicativo hello dá suporte apenas durante o provisionamento do usuário.</span><span class="sxs-lookup"><span data-stu-id="8143e-215">This step is usually not required as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="8143e-216">Se o provisionamento de usuário automático de saudação não estiver habilitado, em seguida, criação manual do usuário pode ser feita conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="8143e-216">If hello automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="8143e-217">Entre no site da empresa do seu Velpic SAML como um administrador e execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8143e-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="8143e-218">Clique na guia gerenciar e vá tooUsers seção, clique no novo usuários tooadd de botão.</span><span class="sxs-lookup"><span data-stu-id="8143e-218">Click on Manage tab and go tooUsers section, then click on New button tooadd users.</span></span>

    ![adicionar usuário](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="8143e-220">Em Olá **"Criar novo usuário"** caixa de diálogo de página, execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8143e-220">On hello **“Create New User”** dialog page, perform hello following steps.</span></span>

    ![usuário](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="8143e-222">a.</span><span class="sxs-lookup"><span data-stu-id="8143e-222">a.</span></span> <span data-ttu-id="8143e-223">Em Olá **nome** caixa de texto, tipo hello nome Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8143e-223">In hello **First Name** textbox, type hello first name of Britta Simon.</span></span>

    <span data-ttu-id="8143e-224">b.</span><span class="sxs-lookup"><span data-stu-id="8143e-224">b.</span></span> <span data-ttu-id="8143e-225">Em Olá **Sobrenome** caixa de texto, digite Olá sobrenome do Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8143e-225">In hello **Last Name** textbox, type hello last name of Britta Simon.</span></span>

    <span data-ttu-id="8143e-226">c.</span><span class="sxs-lookup"><span data-stu-id="8143e-226">c.</span></span> <span data-ttu-id="8143e-227">Em Olá **nome de usuário** caixa de texto, nome de usuário do tipo saudação do Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8143e-227">In hello **User Name** textbox, type hello user name of Britta Simon.</span></span>

    <span data-ttu-id="8143e-228">d.</span><span class="sxs-lookup"><span data-stu-id="8143e-228">d.</span></span> <span data-ttu-id="8143e-229">Em Olá **Email** caixa de texto, tipo hello endereço de email da conta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8143e-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="8143e-230">e.</span><span class="sxs-lookup"><span data-stu-id="8143e-230">e.</span></span> <span data-ttu-id="8143e-231">O restante das informações de saudação é opcional, que você pode preenchê-lo se necessário.</span><span class="sxs-lookup"><span data-stu-id="8143e-231">Rest of hello information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="8143e-232">f.</span><span class="sxs-lookup"><span data-stu-id="8143e-232">f.</span></span> <span data-ttu-id="8143e-233">Clique em **SALVAR**.</span><span class="sxs-lookup"><span data-stu-id="8143e-233">Click **SAVE**.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8143e-234">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8143e-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8143e-235">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooVelpic seu acesso SAML.</span><span class="sxs-lookup"><span data-stu-id="8143e-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooVelpic SAML.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8143e-237">**tooassign Britta Simon tooVelpic SAML, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8143e-237">**tooassign Britta Simon tooVelpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="8143e-238">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8143e-238">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8143e-240">Na lista de aplicativos hello, selecione **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="8143e-240">In hello applications list, select **Velpic SAML**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="8143e-242">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8143e-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8143e-244">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8143e-244">Click **Add** button.</span></span> <span data-ttu-id="8143e-245">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8143e-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8143e-247">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="8143e-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8143e-248">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8143e-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8143e-249">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8143e-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8143e-250">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8143e-250">Testing single sign-on</span></span>

<span data-ttu-id="8143e-251">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="8143e-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="8143e-252">Quando você clica em Olá Velpic SAML bloco no painel de acesso de saudação, você deve obter a página de logon do aplicativo Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="8143e-252">When you click hello Velpic SAML tile in hello Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="8143e-253">Você deve ver Olá **'Fazer logon com o AD do Azure'** botão na página de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="8143e-253">You should see hello **‘Log In With Azure AD’** button on hello sign in page.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="8143e-255">Clique em Olá **'Fazer logon com o AD do Azure'** botão toolog em tooVelpic usando sua conta do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8143e-255">Click on hello **‘Log In With Azure AD’** button toolog in tooVelpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8143e-256">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8143e-256">Additional resources</span></span>

* [<span data-ttu-id="8143e-257">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8143e-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8143e-258">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8143e-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

