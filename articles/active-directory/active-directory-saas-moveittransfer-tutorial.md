---
title: "Tutorial: Integração do Azure Active Directory com o MOVEit Transfer - Azure AD integration | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e transferência MOVEit - integração do AD do Azure."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="e7354-103">Tutorial: Integração do Azure Active Directory com o MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="e7354-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="e7354-104">Neste tutorial, você aprenderá como toointegrate MOVEit transferência - integração do AD do Azure com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="e7354-104">In this tutorial, you learn how toointegrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7354-105">Integrar MOVEit transferência - integração do AD do Azure com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7354-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e7354-106">Você pode controlar no AD do Azure que tenha acesso tooMOVEit transferência - integração do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7354-106">You can control in Azure AD who has access tooMOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="e7354-107">Você pode habilitar seu usuários tooautomatically get conectado tooMOVEit transferência - integração do AD do Azure (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7354-107">You can enable your users tooautomatically get signed-on tooMOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e7354-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7354-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e7354-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7354-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7354-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e7354-110">Prerequisites</span></span>

<span data-ttu-id="e7354-111">tooconfigure integração do AD do Azure com transferência MOVEit - integração do AD do Azure, você precisará Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7354-111">tooconfigure Azure AD integration with MOVEit Transfer - Azure AD integration, you need hello following items:</span></span>

- <span data-ttu-id="e7354-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e7354-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7354-113">Uma assinatura do MOVEit Transfer - Azure AD integration habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="e7354-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7354-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e7354-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7354-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e7354-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7354-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e7354-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7354-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7354-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7354-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e7354-118">Scenario description</span></span>
<span data-ttu-id="e7354-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e7354-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7354-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="e7354-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7354-121">Adicionando MOVEit transferência - integração do AD do Azure da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e7354-121">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
2. <span data-ttu-id="e7354-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e7354-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a><span data-ttu-id="e7354-123">Adicionando MOVEit transferência - integração do AD do Azure da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e7354-123">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
<span data-ttu-id="e7354-124">integração de saudação tooconfigure de transferência MOVEit - integração do AD do Azure no AD do Azure, você precisa tooadd MOVEit transferência - integração do AD do Azure da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e7354-124">tooconfigure hello integration of MOVEit Transfer - Azure AD integration into Azure AD, you need tooadd MOVEit Transfer - Azure AD integration from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e7354-125">**tooadd MOVEit transferência - integração do AD do Azure da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e7354-125">**tooadd MOVEit Transfer - Azure AD integration from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7354-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e7354-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="e7354-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e7354-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e7354-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e7354-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="e7354-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7354-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="e7354-133">Na caixa de pesquisa hello, digite **MOVEit transferência - integração do Azure AD**, selecione **MOVEit transferência - integração do Azure AD** no painel de resultados e clique em **adicionar** saudação do botão tooadd aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e7354-133">In hello search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Transferência de MOVEit - integração do AD do Azure na lista de resultados de saudação](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e7354-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7354-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e7354-136">Nesta seção, você configurará e testará o logon único do Azure AD com o MOVEit Transfer - Azure AD integration, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e7354-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e7354-137">Para toowork de logon único, AD do Azure precisa tooknow que usuário de contraparte Olá na transferência MOVEit - integração do AD do Azure é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7354-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MOVEit Transfer - Azure AD integration is tooa user in Azure AD.</span></span> <span data-ttu-id="e7354-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na transferência MOVEit - integração do AD do Azure precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="e7354-138">In other words, a link relationship between an Azure AD user and hello related user in MOVEit Transfer - Azure AD integration needs toobe established.</span></span>

<span data-ttu-id="e7354-139">Transferência MOVEit - integração do AD do Azure, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7354-139">In MOVEit Transfer - Azure AD integration, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e7354-140">tooconfigure e teste de logon único do AD do Azure com transferência MOVEit - integração do AD do Azure, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7354-140">tooconfigure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e7354-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e7354-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e7354-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7354-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7354-143">**[Criar uma transferência MOVEit - usuário de teste de integração do AD do Azure](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - toohave um equivalente do Britta Simon na transferência MOVEit - integração de AD do Azure que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="e7354-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - toohave a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7354-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="e7354-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7354-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="e7354-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e7354-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7354-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e7354-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em sua transferência MOVEit - aplicativo de integração do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7354-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="e7354-148">**tooconfigure AD do Azure-logon único com transferência MOVEit - integração do AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e7354-148">**tooconfigure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7354-149">Em Olá portal do Azure, Olá **MOVEit transferência - integração do Azure AD** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="e7354-149">In hello Azure portal, on hello **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="e7354-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="e7354-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="e7354-153">Em Olá **MOVEit transferência - integração do Azure AD domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7354-153">On hello **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="e7354-155">a.</span><span class="sxs-lookup"><span data-stu-id="e7354-155">a.</span></span> <span data-ttu-id="e7354-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="e7354-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="e7354-157">b.</span><span class="sxs-lookup"><span data-stu-id="e7354-157">b.</span></span> <span data-ttu-id="e7354-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="e7354-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="e7354-159">c.</span><span class="sxs-lookup"><span data-stu-id="e7354-159">c.</span></span> <span data-ttu-id="e7354-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="e7354-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="e7354-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e7354-161">These values are not real.</span></span> <span data-ttu-id="e7354-162">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="e7354-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e7354-163">Você pode consultar esses valores posteriormente em **URL de metadados do provedor de serviço** seção ou entre em contato com [MOVEit transferência - a equipe de suporte de cliente de integração do AD do Azure](https://community.ipswitch.com/s/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="e7354-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) tooget these values.</span></span>

4. <span data-ttu-id="e7354-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e7354-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="e7354-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e7354-166">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="e7354-168">Logon tooyour MOVEit transferência locatário como um administrador.</span><span class="sxs-lookup"><span data-stu-id="e7354-168">Sign on tooyour MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="e7354-169">No painel de navegação esquerdo hello, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="e7354-169">On hello left navigation pane, click **Settings**.</span></span>

    ![Seção Configurações no lado do aplicativo](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="e7354-171">Clique no link **Logon Único** que está em **Políticas de Segurança -> Autenticação de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="e7354-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Políticas de segurança no lado do aplicativo](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="e7354-173">Clique em documento de metadados de Olá Olá URL de metadados link toodownload.</span><span class="sxs-lookup"><span data-stu-id="e7354-173">Click hello Metadata URL link toodownload hello metadata document.</span></span>

    ![URL de metadados do provedor de serviço](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="e7354-175">Verifique se **entityID** corresponde **identificador** em Olá **MOVEit transferência - integração do Azure AD domínio e URLs** seção.</span><span class="sxs-lookup"><span data-stu-id="e7354-175">Verify **entityID** matches **Identifier** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="e7354-176">Verifique se **AssertionConsumerService** corresponde a URL local **URL de resposta** em Olá **MOVEit transferência - integração do Azure AD domínio e URLs** seção.</span><span class="sxs-lookup"><span data-stu-id="e7354-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="e7354-178">Clique em **Adicionar provedor de identidade** botão tooadd um novo provedor de identidade federada.</span><span class="sxs-lookup"><span data-stu-id="e7354-178">Click **Add Identity Provider** button tooadd a new Federated Identity Provider.</span></span>

    ![Adicionar Provedor de Identidade](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="e7354-180">Clique em **procurar...**  tooselect Olá arquivo de metadados que você baixou do portal do Azure, clique em **Adicionar provedor de identidade** Olá tooupload o arquivo baixado.</span><span class="sxs-lookup"><span data-stu-id="e7354-180">Click **Browse...** tooselect hello metadata file which you downloaded from Azure portal, then click **Add Identity Provider** tooupload hello downloaded file.</span></span>

    ![Provedor de identidade SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="e7354-182">Selecione "**Sim**" como **habilitado** em Olá **editar configurações de provedor de identidade federada...**  página e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="e7354-182">Select "**Yes**" as **Enabled** in hello **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Configurações de Provedor de Identidade Federado](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="e7354-184">Em Olá **Editar federado identidade do provedor de configurações do usuário** página, execute Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7354-184">In hello **Edit Federated Identity Provider User Settings** page, perform hello following actions:</span></span>
    
    ![Edite Configurações de Provedor de Identidade Federado](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="e7354-186">a.</span><span class="sxs-lookup"><span data-stu-id="e7354-186">a.</span></span> <span data-ttu-id="e7354-187">Selecione **SAML NameID** como **Nome de logon**.</span><span class="sxs-lookup"><span data-stu-id="e7354-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="e7354-188">b.</span><span class="sxs-lookup"><span data-stu-id="e7354-188">b.</span></span> <span data-ttu-id="e7354-189">Selecione **outros** como **nome completo** e em Olá **nome do atributo** caixa de texto, coloque o valor de saudação: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="e7354-189">Select **Other** as **Full name** and in hello **Attribute name** textbox put hello value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="e7354-190">c.</span><span class="sxs-lookup"><span data-stu-id="e7354-190">c.</span></span> <span data-ttu-id="e7354-191">Selecione **outros** como **Email** e em Olá **nome do atributo** caixa de texto, coloque o valor de saudação: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="e7354-191">Select **Other** as **Email** and in hello **Attribute name** textbox put hello value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="e7354-192">d.</span><span class="sxs-lookup"><span data-stu-id="e7354-192">d.</span></span> <span data-ttu-id="e7354-193">Selecione **Sim** para **Criação automática de conta no momento da conexão**.</span><span class="sxs-lookup"><span data-stu-id="e7354-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="e7354-194">e.</span><span class="sxs-lookup"><span data-stu-id="e7354-194">e.</span></span> <span data-ttu-id="e7354-195">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e7354-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="e7354-196">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="e7354-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e7354-197">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="e7354-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e7354-198">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7354-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e7354-199">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7354-199">Create an Azure AD test user</span></span>

<span data-ttu-id="e7354-200">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7354-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="e7354-202">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e7354-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7354-203">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="e7354-203">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e7354-205">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="e7354-205">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e7354-207">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7354-207">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e7354-209">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7354-209">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e7354-211">a.</span><span class="sxs-lookup"><span data-stu-id="e7354-211">a.</span></span> <span data-ttu-id="e7354-212">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7354-212">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7354-213">b.</span><span class="sxs-lookup"><span data-stu-id="e7354-213">b.</span></span> <span data-ttu-id="e7354-214">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7354-214">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e7354-215">c.</span><span class="sxs-lookup"><span data-stu-id="e7354-215">c.</span></span> <span data-ttu-id="e7354-216">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="e7354-216">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e7354-217">d.</span><span class="sxs-lookup"><span data-stu-id="e7354-217">d.</span></span> <span data-ttu-id="e7354-218">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e7354-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="e7354-219">Crie um usuário de teste do MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="e7354-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="e7354-220">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon na transferência MOVEit - integração do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7354-220">hello objective of this section is toocreate a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="e7354-221">O MOVEit Transfer - Azure AD integration dá suporte ao provisionamento just-in-time, que você habilitou.</span><span class="sxs-lookup"><span data-stu-id="e7354-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="e7354-222">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="e7354-222">There is no action item for you in this section.</span></span> <span data-ttu-id="e7354-223">Um novo usuário é criado durante uma tentativa tooaccess MOVEit transferência - integração do AD do Azure se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="e7354-223">A new user is created during an attempt tooaccess MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="e7354-224">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [MOVEit transferência - a equipe de suporte de cliente de integração do AD do Azure](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="e7354-224">If you need toocreate a user manually, you need toocontact hello [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e7354-225">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e7354-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e7354-226">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMOVEit transferência - integração do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7354-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMOVEit Transfer - Azure AD integration.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="e7354-228">**tooassign Britta Simon tooMOVEit transferência - integração do AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e7354-228">**tooassign Britta Simon tooMOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7354-229">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e7354-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e7354-231">Na lista de aplicativos hello, selecione **MOVEit transferência - integração do Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="e7354-231">In hello applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![Olá MOVEit transferência - integração do AD do Azure link na lista de aplicativos Olá](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="e7354-233">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e7354-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="e7354-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e7354-235">Click **Add** button.</span></span> <span data-ttu-id="e7354-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7354-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="e7354-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7354-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e7354-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7354-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7354-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7354-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e7354-241">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="e7354-241">Test single sign-on</span></span>

<span data-ttu-id="e7354-242">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="e7354-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="e7354-243">Quando você clica em Olá MOVEit transferência - bloco de integração do AD do Azure em Olá painel de acesso, você deve obter automaticamente assinado em tooyour MOVEit transferência - aplicativo de integração do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7354-243">When you click hello MOVEit Transfer - Azure AD integration tile in hello Access Panel, you should get automatically signed-on tooyour MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e7354-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e7354-244">Additional resources</span></span>

* [<span data-ttu-id="e7354-245">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e7354-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7354-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e7354-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

