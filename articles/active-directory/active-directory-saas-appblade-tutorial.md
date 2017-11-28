---
title: "Tutorial: Integração do Azure Active Directory com o AppBlade | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e AppBlade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 06f3d8fcee97945c867bca6f3aebe15ecef04617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="7c071-103">Tutorial: Integração do Active Directory do Azure com o AppBlade</span><span class="sxs-lookup"><span data-stu-id="7c071-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="7c071-104">Neste tutorial, você aprenderá como toointegrate AppBlade com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="7c071-104">In this tutorial, you learn how toointegrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c071-105">Integrando AppBlade com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c071-105">Integrating AppBlade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7c071-106">Você pode controlar no AD do Azure que tenha acesso tooAppBlade</span><span class="sxs-lookup"><span data-stu-id="7c071-106">You can control in Azure AD who has access tooAppBlade</span></span>
- <span data-ttu-id="7c071-107">Você pode habilitar seu usuários tooautomatically get conectado tooAppBlade (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c071-107">You can enable your users tooautomatically get signed-on tooAppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7c071-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7c071-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7c071-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c071-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c071-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7c071-110">Prerequisites</span></span>

<span data-ttu-id="7c071-111">tooconfigure integração do AD do Azure com AppBlade, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c071-111">tooconfigure Azure AD integration with AppBlade, you need hello following items:</span></span>

- <span data-ttu-id="7c071-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c071-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c071-113">Uma assinatura habilitada para logon único do AppBlade</span><span class="sxs-lookup"><span data-stu-id="7c071-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c071-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7c071-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c071-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7c071-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c071-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7c071-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c071-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c071-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c071-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7c071-118">Scenario description</span></span>
<span data-ttu-id="7c071-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7c071-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c071-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="7c071-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c071-121">Adicionando AppBlade da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7c071-121">Adding AppBlade from hello gallery</span></span>
2. <span data-ttu-id="7c071-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c071-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-hello-gallery"></a><span data-ttu-id="7c071-123">Adicionando AppBlade da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7c071-123">Adding AppBlade from hello gallery</span></span>
<span data-ttu-id="7c071-124">integração de saudação tooconfigure de AppBlade no AD do Azure, você precisa tooadd AppBlade da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7c071-124">tooconfigure hello integration of AppBlade into Azure AD, you need tooadd AppBlade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7c071-125">**tooadd AppBlade da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7c071-125">**tooadd AppBlade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c071-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7c071-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7c071-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7c071-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7c071-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7c071-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7c071-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c071-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7c071-133">Na caixa de pesquisa hello, digite **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="7c071-133">In hello search box, type **AppBlade**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="7c071-135">No painel de resultados de saudação, selecione **AppBlade**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7c071-135">In hello results panel, select **AppBlade**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c071-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c071-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c071-138">Nesta seção, você configura e testa o logon único do Azure AD com o AppBlade, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7c071-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7c071-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em AppBlade é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c071-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppBlade is tooa user in Azure AD.</span></span> <span data-ttu-id="7c071-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em AppBlade precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7c071-140">In other words, a link relationship between an Azure AD user and hello related user in AppBlade needs toobe established.</span></span>

<span data-ttu-id="7c071-141">AppBlade, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c071-141">In AppBlade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7c071-142">tooconfigure e teste de logon único do AD do Azure com AppBlade, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c071-142">tooconfigure and test Azure AD single sign-on with AppBlade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7c071-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7c071-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7c071-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c071-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c071-145">**[Criar um usuário de teste AppBlade](#creating-an-appblade-test-user)**  -toohave um equivalente do Britta Simon em AppBlade é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="7c071-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - toohave a counterpart of Britta Simon in AppBlade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c071-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="7c071-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c071-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="7c071-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c071-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c071-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7c071-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo AppBlade.</span><span class="sxs-lookup"><span data-stu-id="7c071-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="7c071-150">**tooconfigure AD do Azure-logon único com AppBlade, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7c071-150">**tooconfigure Azure AD single sign-on with AppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c071-151">Em Olá portal do Azure, Olá **AppBlade** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="7c071-151">In hello Azure portal, on hello **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7c071-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="7c071-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="7c071-155">Em Olá **AppBlade domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c071-155">On hello **AppBlade Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="7c071-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="7c071-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7c071-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="7c071-158">This value is not real.</span></span> <span data-ttu-id="7c071-159">Valor de saudação de atualização com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="7c071-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="7c071-160">Entre em contato com [equipe de suporte do cliente AppBlade](mailto:support@appblade.com) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c071-160">Contact [AppBlade Client support team](mailto:support@appblade.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="7c071-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7c071-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="7c071-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7c071-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7c071-165">tooconfigure logon único no **AppBlade** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="7c071-165">tooconfigure single sign-on on **AppBlade** side, you need toosend hello downloaded **Metadata XML** too[AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="7c071-166">Além disso, peça-los Olá tooconfigure **URL do emissor de SSO** como `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="7c071-166">Also, please ask them tooconfigure hello **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="7c071-167">Essa configuração é necessária para toowork de logon único.</span><span class="sxs-lookup"><span data-stu-id="7c071-167">This setting is required for single sign-on toowork.</span></span>


> [!TIP]
> <span data-ttu-id="7c071-168">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="7c071-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7c071-169">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="7c071-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7c071-170">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7c071-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c071-171">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c071-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c071-172">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c071-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7c071-174">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7c071-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c071-175">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7c071-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7c071-177">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="7c071-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7c071-179">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c071-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7c071-181">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c071-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7c071-183">a.</span><span class="sxs-lookup"><span data-stu-id="7c071-183">a.</span></span> <span data-ttu-id="7c071-184">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c071-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c071-185">b.</span><span class="sxs-lookup"><span data-stu-id="7c071-185">b.</span></span> <span data-ttu-id="7c071-186">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7c071-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7c071-187">c.</span><span class="sxs-lookup"><span data-stu-id="7c071-187">c.</span></span> <span data-ttu-id="7c071-188">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="7c071-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7c071-189">d.</span><span class="sxs-lookup"><span data-stu-id="7c071-189">d.</span></span> <span data-ttu-id="7c071-190">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7c071-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="7c071-191">Criando um usuário de teste do AppBlade</span><span class="sxs-lookup"><span data-stu-id="7c071-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="7c071-192">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no AppBlade.</span><span class="sxs-lookup"><span data-stu-id="7c071-192">hello objective of this section is toocreate a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="7c071-193">O AppBlade dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="7c071-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="7c071-194">**Verifique se o nome de domínio está configurado no AppBlade para o provisionamento de usuário. Depois que esse usuário apenas para just-in-time Olá provisionamento funciona.**</span><span class="sxs-lookup"><span data-stu-id="7c071-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only hello just-in-time user provisioning works.**</span></span>

<span data-ttu-id="7c071-195">Se o usuário Olá tem um endereço de email terminando com domínio Olá configurado por AppBlade para sua conta, e em seguida, o usuário Olá ingressarão automaticamente conta hello como um membro com o nível de permissão Olá especificado, que é "Básico" (um usuário básico que só pode ser instalado aplicativos), "membro da equipe (um usuário que pode carregar novas versões do aplicativo e gerenciar projetos) ou"Administrador"(conta de toohello de privilégios de administrador completo).</span><span class="sxs-lookup"><span data-stu-id="7c071-195">If hello user has an email address ending with hello domain configured by AppBlade for your account, then hello user will automatically join hello account as a member with hello permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges toohello account).</span></span> <span data-ttu-id="7c071-196">Normalmente faria escolha básica e, em seguida, promova os usuários manualmente por meio de um logon de administrador (AppBlade precisa tooconfigure um logon de administração baseada em email com antecedência ou promover um usuário em nome do cliente Olá após o logon).</span><span class="sxs-lookup"><span data-stu-id="7c071-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs tooconfigure either an email-based admin login in advance or promote a user on behalf of hello customer after login).</span></span>

<span data-ttu-id="7c071-197">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="7c071-197">There is no action item for you in this section.</span></span> <span data-ttu-id="7c071-198">Um novo usuário é criado durante uma tentativa tooaccess AppBlade se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="7c071-198">A new user is created during an attempt tooaccess AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="7c071-199">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [a equipe de suporte AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="7c071-199">If you need toocreate a user manually, you need toocontact hello [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7c071-200">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c071-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7c071-201">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAppBlade.</span><span class="sxs-lookup"><span data-stu-id="7c071-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppBlade.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7c071-203">**tooassign Britta Simon tooAppBlade, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7c071-203">**tooassign Britta Simon tooAppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c071-204">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7c071-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7c071-206">Na lista de aplicativos hello, selecione **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="7c071-206">In hello applications list, select **AppBlade**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="7c071-208">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7c071-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7c071-210">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7c071-210">Click **Add** button.</span></span> <span data-ttu-id="7c071-211">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c071-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7c071-213">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c071-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7c071-214">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c071-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c071-215">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c071-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7c071-216">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7c071-216">Testing single sign-on</span></span>

<span data-ttu-id="7c071-217">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="7c071-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="7c071-218">Quando você clica em bloco AppBlade Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour AppBlade aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7c071-218">When you click hello AppBlade tile in hello Access Panel, you should get automatically signed-on tooyour AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7c071-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7c071-219">Additional resources</span></span>

* [<span data-ttu-id="7c071-220">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7c071-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c071-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7c071-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png

