---
title: "Tutorial: Integração do Azure Active Directory com o Mimecast Admin Console | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Console de Admin do Mimecast."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="5000e-103">Tutorial: Integração do Azure Active Directory com o Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="5000e-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="5000e-104">Neste tutorial, você aprenderá como toointegrate do Console de Admin do Mimecast com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="5000e-104">In this tutorial, you learn how toointegrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5000e-105">Integração do Console de Admin do Mimecast com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="5000e-105">Integrating Mimecast Admin Console with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5000e-106">Você pode controlar no AD do Azure que tenha acesso tooMimecast Console de administração.</span><span class="sxs-lookup"><span data-stu-id="5000e-106">You can control in Azure AD who has access tooMimecast Admin Console.</span></span>
- <span data-ttu-id="5000e-107">Você pode habilitar seu usuários tooautomatically get conectado tooMimecast Console de administração (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5000e-107">You can enable your users tooautomatically get signed-on tooMimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5000e-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5000e-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="5000e-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5000e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5000e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5000e-110">Prerequisites</span></span>

<span data-ttu-id="5000e-111">tooconfigure integração do AD do Azure com o Console de Admin do Mimecast, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="5000e-111">tooconfigure Azure AD integration with Mimecast Admin Console, you need hello following items:</span></span>

- <span data-ttu-id="5000e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5000e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5000e-113">Uma assinatura do Mimecast Admin Console com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="5000e-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5000e-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5000e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5000e-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5000e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5000e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5000e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5000e-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5000e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5000e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5000e-118">Scenario description</span></span>
<span data-ttu-id="5000e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5000e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5000e-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="5000e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5000e-121">Adicionar o Console de Admin do Mimecast da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5000e-121">Adding Mimecast Admin Console from hello gallery</span></span>
2. <span data-ttu-id="5000e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5000e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a><span data-ttu-id="5000e-123">Adicionar o Console de Admin do Mimecast da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5000e-123">Adding Mimecast Admin Console from hello gallery</span></span>
<span data-ttu-id="5000e-124">integração de saudação tooconfigure do Console de Admin do Mimecast no AD do Azure, você precisa tooadd Console de Admin do Mimecast da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5000e-124">tooconfigure hello integration of Mimecast Admin Console into Azure AD, you need tooadd Mimecast Admin Console from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5000e-125">**tooadd Console de Admin do Mimecast da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5000e-125">**tooadd Mimecast Admin Console from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5000e-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5000e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="5000e-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5000e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5000e-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5000e-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="5000e-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5000e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="5000e-133">Na caixa de pesquisa hello, digite **Console de Admin do Mimecast**, selecione **Console de Admin do Mimecast** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5000e-133">In hello search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Console de Admin do Mimecast na lista de resultados de saudação](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5000e-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5000e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5000e-136">Nesta seção, você configura e testa o logon único do Azure AD com o Mimecast Admin Console, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="5000e-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5000e-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Console de Admin do Mimecast é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5000e-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Admin Console is tooa user in Azure AD.</span></span> <span data-ttu-id="5000e-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Console de Admin do Mimecast precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="5000e-138">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Admin Console needs toobe established.</span></span>

<span data-ttu-id="5000e-139">No Console de Admin do Mimecast, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="5000e-139">In Mimecast Admin Console, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5000e-140">tooconfigure e teste de logon único do AD do Azure com o Console de Admin do Mimecast, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="5000e-140">tooconfigure and test Azure AD single sign-on with Mimecast Admin Console, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5000e-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5000e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5000e-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5000e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5000e-143">**[Criar um usuário de teste do Console de Admin do Mimecast](#create-a-mimecast-admin-console-test-user)**  -toohave um equivalente do Britta Simon no Console de Admin do Mimecast que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="5000e-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - toohave a counterpart of Britta Simon in Mimecast Admin Console that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5000e-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="5000e-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5000e-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="5000e-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5000e-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5000e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5000e-147">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de Console de Admin do Mimecast.</span><span class="sxs-lookup"><span data-stu-id="5000e-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="5000e-148">**tooconfigure logon único do AD do Azure com o Console de Admin do Mimecast, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5000e-148">**tooconfigure Azure AD single sign-on with Mimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="5000e-149">Em Olá portal do Azure, Olá **Console de Admin do Mimecast** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="5000e-149">In hello Azure portal, on hello **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="5000e-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="5000e-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="5000e-153">Em Olá **URLs e domínio de Console de Admin do Mimecast** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5000e-153">On hello **Mimecast Admin Console Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="5000e-155">Em Olá **URL de logon** caixa de texto, digite a URL de saudação:</span><span class="sxs-lookup"><span data-stu-id="5000e-155">In hello **Sign-on URL** textbox, type hello URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="5000e-156">a URL de logon Olá é a região específica.</span><span class="sxs-lookup"><span data-stu-id="5000e-156">hello sign on URL is region specific.</span></span>

4. <span data-ttu-id="5000e-157">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5000e-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="5000e-159">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5000e-159">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5000e-161">Em Olá **configuração de Console de Admin do Mimecast** seção, clique em **configurar o Console de Admin do Mimecast** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="5000e-161">On hello **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5000e-162">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="5000e-162">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="5000e-164">Em outra janela do navegador da Web, faça logon em seu Mimecast Admin Console como um administrador.</span><span class="sxs-lookup"><span data-stu-id="5000e-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="5000e-165">Vá muito**serviços \> aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="5000e-165">Go too**Services \> Application**.</span></span>

    <span data-ttu-id="5000e-166">![Serviços](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Serviços")</span><span class="sxs-lookup"><span data-stu-id="5000e-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="5000e-167">Clique em **Perfis de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="5000e-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="5000e-168">![Perfis de Autenticação](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Perfis de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="5000e-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="5000e-169">Clique em **Novo Perfil de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="5000e-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="5000e-170">![Novos Perfis de Autenticação](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "Novos Perfis de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="5000e-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="5000e-171">Em Olá **o perfil de autenticação** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5000e-171">In hello **Authentication Profile** section, perform hello following steps:</span></span>

    <span data-ttu-id="5000e-172">![Perfil de Autenticação](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Perfil de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="5000e-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="5000e-173">a.</span><span class="sxs-lookup"><span data-stu-id="5000e-173">a.</span></span> <span data-ttu-id="5000e-174">Em Olá **descrição** caixa de texto, digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="5000e-174">In hello **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="5000e-175">b.</span><span class="sxs-lookup"><span data-stu-id="5000e-175">b.</span></span> <span data-ttu-id="5000e-176">Selecione **Impor Autenticação SAML para o Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="5000e-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="5000e-177">c.</span><span class="sxs-lookup"><span data-stu-id="5000e-177">c.</span></span> <span data-ttu-id="5000e-178">Como **Provedor**, selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5000e-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="5000e-179">d.</span><span class="sxs-lookup"><span data-stu-id="5000e-179">d.</span></span> <span data-ttu-id="5000e-180">Colar **ID da entidade SAML**, que você copiou de saudação portal do Azure em hello **URL do emissor** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="5000e-180">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="5000e-181">e.</span><span class="sxs-lookup"><span data-stu-id="5000e-181">e.</span></span> <span data-ttu-id="5000e-182">Colar **Single Sign-On URL do serviço SAML**, que você copiou de saudação portal do Azure em hello **URL de logon** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="5000e-182">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Login URL** textbox.</span></span>

    <span data-ttu-id="5000e-183">f.</span><span class="sxs-lookup"><span data-stu-id="5000e-183">f.</span></span> <span data-ttu-id="5000e-184">Colar **Single Sign-On URL do serviço SAML**, que você copiou de saudação portal do Azure em hello **URL de Logout** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="5000e-184">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="5000e-185">Olá valor de URL de logon e o valor de URL de Logout de saudação são para hello Console de Admin do Mimecast Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="5000e-185">hello Login URL value and hello Logout URL value are for hello Mimecast Admin Console hello same.</span></span>
    
    <span data-ttu-id="5000e-186">g.</span><span class="sxs-lookup"><span data-stu-id="5000e-186">g.</span></span> <span data-ttu-id="5000e-187">Abra seu certificado de base 64 é baixado do portal do Azure no bloco de notas, remova a primeira linha de saudação ("*--*") e a última linha de saudação ("*--*"), Olá cópia restantes conteúdo dele na área de transferência e, em seguida, cole-o toohello **certificado do provedor de identidade (metadados)** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="5000e-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove hello first line (“*--*“) and hello last line (“*--*“), copy hello remaining content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="5000e-188">h.</span><span class="sxs-lookup"><span data-stu-id="5000e-188">h.</span></span> <span data-ttu-id="5000e-189">Selecione **Permitir Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="5000e-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="5000e-190">i.</span><span class="sxs-lookup"><span data-stu-id="5000e-190">i.</span></span> <span data-ttu-id="5000e-191">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5000e-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5000e-192">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="5000e-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5000e-193">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="5000e-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5000e-194">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5000e-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5000e-195">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5000e-195">Create an Azure AD test user</span></span>

<span data-ttu-id="5000e-196">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5000e-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="5000e-198">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5000e-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5000e-199">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="5000e-199">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5000e-201">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="5000e-201">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5000e-203">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5000e-203">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5000e-205">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5000e-205">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5000e-207">a.</span><span class="sxs-lookup"><span data-stu-id="5000e-207">a.</span></span> <span data-ttu-id="5000e-208">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5000e-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5000e-209">b.</span><span class="sxs-lookup"><span data-stu-id="5000e-209">b.</span></span> <span data-ttu-id="5000e-210">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5000e-210">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="5000e-211">c.</span><span class="sxs-lookup"><span data-stu-id="5000e-211">c.</span></span> <span data-ttu-id="5000e-212">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="5000e-212">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="5000e-213">d.</span><span class="sxs-lookup"><span data-stu-id="5000e-213">d.</span></span> <span data-ttu-id="5000e-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5000e-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="5000e-215">Criar um usuário de teste do Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="5000e-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="5000e-216">Ordem tooenable AD do Azure usuários toolog no Console de Admin do Mimecast, eles devem ser provisionados no Console de Admin do Mimecast.</span><span class="sxs-lookup"><span data-stu-id="5000e-216">In order tooenable Azure AD users toolog into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="5000e-217">No caso de saudação do Console de Admin do Mimecast, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="5000e-217">In hello case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="5000e-218">Antes de criar os usuários, você precisa tooregister um domínio.</span><span class="sxs-lookup"><span data-stu-id="5000e-218">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="5000e-219">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5000e-219">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="5000e-220">Logon tooyour **Console de Admin do Mimecast** como administrador.</span><span class="sxs-lookup"><span data-stu-id="5000e-220">Sign on tooyour **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="5000e-221">Vá muito**diretórios \> interno**.</span><span class="sxs-lookup"><span data-stu-id="5000e-221">Go too**Directories \> Internal**.</span></span>
   
   <span data-ttu-id="5000e-222">![Diretórios](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Diretórios")</span><span class="sxs-lookup"><span data-stu-id="5000e-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="5000e-223">Clique em **Registrar Novo Domínio**.</span><span class="sxs-lookup"><span data-stu-id="5000e-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="5000e-224">![Registrar Novo Domínio](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Registrar Novo Domínio")</span><span class="sxs-lookup"><span data-stu-id="5000e-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="5000e-225">Depois de criar o novo domínio, clique em **Novo Endereço**.</span><span class="sxs-lookup"><span data-stu-id="5000e-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="5000e-226">![Novo Endereço](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "Novo Endereço")</span><span class="sxs-lookup"><span data-stu-id="5000e-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="5000e-227">Na caixa de diálogo Olá de novo endereço, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5000e-227">In hello new address dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="5000e-228">![Salvar](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Salvar")</span><span class="sxs-lookup"><span data-stu-id="5000e-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="5000e-229">a.</span><span class="sxs-lookup"><span data-stu-id="5000e-229">a.</span></span> <span data-ttu-id="5000e-230">Saudação de tipo **endereço de Email**, **nome Global**, **senha**, e **Confirmar senha** atributos de um AD do Azure válidas de conta você deseja tooprovision em Olá relacionados caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="5000e-230">Type hello **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>

   <span data-ttu-id="5000e-231">b.</span><span class="sxs-lookup"><span data-stu-id="5000e-231">b.</span></span> <span data-ttu-id="5000e-232">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5000e-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="5000e-233">Você pode usar qualquer outra ferramenta de criação de conta de usuário do Console de Admin do Mimecast ou APIs fornecidas por contas de usuário do Console de Admin do Mimecast tooprovision AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5000e-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console tooprovision Azure AD user accounts.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5000e-234">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5000e-234">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5000e-235">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMimecast Console de administração.</span><span class="sxs-lookup"><span data-stu-id="5000e-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Admin Console.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="5000e-237">**tooassign Britta Simon tooMimecast Console de administração, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5000e-237">**tooassign Britta Simon tooMimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="5000e-238">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5000e-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5000e-240">Na lista de aplicativos hello, selecione **Console de Admin do Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="5000e-240">In hello applications list, select **Mimecast Admin Console**.</span></span>

    ![link do Console de Admin do Mimecast Olá na lista de aplicativos Olá](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="5000e-242">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5000e-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="5000e-244">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5000e-244">Click **Add** button.</span></span> <span data-ttu-id="5000e-245">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5000e-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="5000e-247">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="5000e-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5000e-248">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5000e-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5000e-249">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5000e-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5000e-250">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="5000e-250">Test single sign-on</span></span>

<span data-ttu-id="5000e-251">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5000e-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5000e-252">Quando você clica em um bloco de Console de Admin do Mimecast Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Console de Admin do Mimecast.</span><span class="sxs-lookup"><span data-stu-id="5000e-252">When you click hello Mimecast Admin Console tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Admin Console application.</span></span>
<span data-ttu-id="5000e-253">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5000e-253">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5000e-254">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5000e-254">Additional resources</span></span>

* [<span data-ttu-id="5000e-255">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5000e-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5000e-256">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5000e-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

