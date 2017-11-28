---
title: "Tutorial: Integração do Azure Active Directory ao Autotask Workplace | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Autotask no local de trabalho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="3dabe-103">Tutorial: Integração do Azure Active Directory ao Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="3dabe-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="3dabe-104">Neste tutorial, você aprenderá como toointegrate Autotask no local de trabalho com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="3dabe-104">In this tutorial, you learn how toointegrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3dabe-105">Integrando Autotask no local de trabalho com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="3dabe-105">Integrating Autotask Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3dabe-106">Você pode controlar no AD do Azure que tenha acesso tooAutotask no local de trabalho</span><span class="sxs-lookup"><span data-stu-id="3dabe-106">You can control in Azure AD who has access tooAutotask Workplace</span></span>
- <span data-ttu-id="3dabe-107">Você pode habilitar seu usuários tooautomatically get conectado tooAutotask no local de trabalho (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3dabe-107">You can enable your users tooautomatically get signed-on tooAutotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3dabe-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3dabe-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3dabe-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3dabe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3dabe-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3dabe-110">Prerequisites</span></span>

<span data-ttu-id="3dabe-111">tooconfigure integração do AD do Azure com Autotask no local de trabalho, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3dabe-111">tooconfigure Azure AD integration with Autotask Workplace, you need hello following items:</span></span>

- <span data-ttu-id="3dabe-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3dabe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3dabe-113">Uma assinatura habilitada para logon único do Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="3dabe-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="3dabe-114">Você deve ser um administrador ou superadministrador no local de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3dabe-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="3dabe-115">Você deve ter uma conta de administrador no hello AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dabe-115">You must have an administrator account in hello Azure AD.</span></span>
- <span data-ttu-id="3dabe-116">usuários de saudação que utilizam este recurso devem ter contas no local de trabalho e hello AD do Azure e seus endereços de email para ambos devem corresponder.</span><span class="sxs-lookup"><span data-stu-id="3dabe-116">hello users that will utilize this feature must have accounts within Workplace and hello Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="3dabe-117">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3dabe-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3dabe-118">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3dabe-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3dabe-119">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3dabe-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3dabe-120">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3dabe-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3dabe-121">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3dabe-121">Scenario description</span></span>
<span data-ttu-id="3dabe-122">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3dabe-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3dabe-123">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="3dabe-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3dabe-124">Adicionando Autotask no local de trabalho na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3dabe-124">Adding Autotask Workplace from hello gallery</span></span>
2. <span data-ttu-id="3dabe-125">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3dabe-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-hello-gallery"></a><span data-ttu-id="3dabe-126">Adicionando Autotask no local de trabalho na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3dabe-126">Adding Autotask Workplace from hello gallery</span></span>
<span data-ttu-id="3dabe-127">integração de saudação tooconfigure do local de trabalho Autotask no AD do Azure, você precisa tooadd Autotask no local de trabalho da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3dabe-127">tooconfigure hello integration of Autotask Workplace into Azure AD, you need tooadd Autotask Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3dabe-128">**tooadd Autotask no local de trabalho na Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3dabe-128">**tooadd Autotask Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dabe-129">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3dabe-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="3dabe-131">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3dabe-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3dabe-132">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3dabe-132">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="3dabe-134">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3dabe-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="3dabe-136">Na caixa de pesquisa hello, digite **Autotask no local de trabalho**, selecione **Autotask trabalho** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3dabe-136">In hello search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de local de trabalho Autotask em Olá](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3dabe-138">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dabe-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3dabe-139">Nesta seção, você configura e testa o logon único do Azure AD com o Autotask Workplace, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3dabe-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3dabe-140">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na área de trabalho Autotask é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dabe-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Autotask Workplace is tooa user in Azure AD.</span></span> <span data-ttu-id="3dabe-141">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na área de trabalho Autotask precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3dabe-141">In other words, a link relationship between an Azure AD user and hello related user in Autotask Workplace needs toobe established.</span></span>

<span data-ttu-id="3dabe-142">Na área de trabalho Autotask, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="3dabe-142">In Autotask Workplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3dabe-143">tooconfigure e teste de logon único do AD do Azure com Autotask de espaço de trabalho, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="3dabe-143">tooconfigure and test Azure AD single sign-on with Autotask Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3dabe-144">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3dabe-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3dabe-145">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3dabe-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3dabe-146">**[Criar um usuário de teste do local de trabalho Autotask](#create-an-autotask-workplace-test-user)**  -toohave um equivalente do Britta Simon na área de trabalho Autotask que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="3dabe-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - toohave a counterpart of Britta Simon in Autotask Workplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3dabe-147">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="3dabe-147">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3dabe-148">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="3dabe-148">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3dabe-149">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dabe-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3dabe-150">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de área de trabalho Autotask.</span><span class="sxs-lookup"><span data-stu-id="3dabe-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="3dabe-151">**tooconfigure AD do Azure-logon único com o local de trabalho Autotask execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3dabe-151">**tooconfigure Azure AD single sign-on with Autotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dabe-152">Em Olá portal do Azure, Olá **Autotask trabalho** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="3dabe-152">In hello Azure portal, on hello **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="3dabe-154">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="3dabe-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="3dabe-156">Se desejar que o aplicativo hello tooconfigure **IDP** iniciada modo, executar Olá seguindo as etapas na Olá **URLs e domínio do local de trabalho Autotask** seção:</span><span class="sxs-lookup"><span data-stu-id="3dabe-156">If you wish tooconfigure hello application in **IDP** initiated mode, perform hello following steps on hello **Autotask Workplace Domain and URLs** section:</span></span>

    ![Informações de logon único de Domínio e URLs do Autotask Workplace para IdP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="3dabe-158">a.</span><span class="sxs-lookup"><span data-stu-id="3dabe-158">a.</span></span> <span data-ttu-id="3dabe-159">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="3dabe-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="3dabe-160">b.</span><span class="sxs-lookup"><span data-stu-id="3dabe-160">b.</span></span> <span data-ttu-id="3dabe-161">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="3dabe-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="3dabe-162">Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado, verifique **Mostrar configurações de URL avançadas** e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3dabe-162">If you wish tooconfigure hello application in **SP** initiated mode, check **Show advanced URL settings** and perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Autotask Workplace para SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="3dabe-164">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="3dabe-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3dabe-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="3dabe-165">These values are not real.</span></span> <span data-ttu-id="3dabe-166">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="3dabe-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3dabe-167">Entre em contato com [equipe de suporte do cliente de área de trabalho Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="3dabe-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget these values.</span></span> 

5. <span data-ttu-id="3dabe-168">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3dabe-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="3dabe-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3dabe-170">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="3dabe-172">Em uma janela de navegador web diferente, o logon tooWorkplace Online usando Olá credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="3dabe-172">In a different web browser window, Log in tooWorkplace Online using hello administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="3dabe-173">Ao configurar Olá IdP, um subdomínio precisará toobe especificado.</span><span class="sxs-lookup"><span data-stu-id="3dabe-173">When configuring hello IdP, a subdomain will need toobe specified.</span></span> <span data-ttu-id="3dabe-174">subdomínio de correta de saudação do tooconfirm, logon tooWorkplace on-line.</span><span class="sxs-lookup"><span data-stu-id="3dabe-174">tooconfirm hello correct subdomain, login tooWorkplace Online.</span></span> <span data-ttu-id="3dabe-175">Depois de conectado, manter Observação toohello subdomínio Olá URL.</span><span class="sxs-lookup"><span data-stu-id="3dabe-175">Once logged in, make note toohello subdomain in hello URL.</span></span>
    ><span data-ttu-id="3dabe-176">subdomínio Olá faz parte de saudação entre hello "https://" e ".awp.autotask.net/" e deve ser EUA, UE, autoridade de certificação ou Austrália.</span><span class="sxs-lookup"><span data-stu-id="3dabe-176">hello subdomain is hello part between hello “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="3dabe-177">Vá muito**configuração** > **Single Sign-On** e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3dabe-177">Go too**Configuration** > **Single Sign-On** and perform hello following steps:</span></span>

    ![Configuração de Logon Único do Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="3dabe-179">a.</span><span class="sxs-lookup"><span data-stu-id="3dabe-179">a.</span></span> <span data-ttu-id="3dabe-180">Selecione Olá **arquivo de metadados XML** opção e, em seguida, carregar Olá **Metadata XML** baixado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dabe-180">Select hello **XML Metadata File** option, and then upload hello **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="3dabe-181">b.</span><span class="sxs-lookup"><span data-stu-id="3dabe-181">b.</span></span> <span data-ttu-id="3dabe-182">Clique em **Habilitar SSO**.</span><span class="sxs-lookup"><span data-stu-id="3dabe-182">Click **Enable SSO**.</span></span>
    
    ![Configuração de aprovação de Logon Único do Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="3dabe-184">c.</span><span class="sxs-lookup"><span data-stu-id="3dabe-184">c.</span></span> <span data-ttu-id="3dabe-185">Selecione Olá **confirmar essas informações estão corretas e eu confio neste IdP** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="3dabe-185">Select hello **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="3dabe-186">d.</span><span class="sxs-lookup"><span data-stu-id="3dabe-186">d.</span></span> <span data-ttu-id="3dabe-187">Clique em **Aprovar**.</span><span class="sxs-lookup"><span data-stu-id="3dabe-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="3dabe-188">Se você precisar de assistência com a configuração Autotask no local de trabalho, consulte [essa página](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget assistência com sua conta da empresa.</span><span class="sxs-lookup"><span data-stu-id="3dabe-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="3dabe-189">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="3dabe-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3dabe-190">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="3dabe-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3dabe-191">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3dabe-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3dabe-192">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dabe-192">Create an Azure AD test user</span></span>

<span data-ttu-id="3dabe-193">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dabe-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="3dabe-195">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3dabe-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dabe-196">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="3dabe-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3dabe-198">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3dabe-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3dabe-200">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3dabe-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3dabe-202">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3dabe-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3dabe-204">a.</span><span class="sxs-lookup"><span data-stu-id="3dabe-204">a.</span></span> <span data-ttu-id="3dabe-205">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3dabe-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3dabe-206">b.</span><span class="sxs-lookup"><span data-stu-id="3dabe-206">b.</span></span> <span data-ttu-id="3dabe-207">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3dabe-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="3dabe-208">c.</span><span class="sxs-lookup"><span data-stu-id="3dabe-208">c.</span></span> <span data-ttu-id="3dabe-209">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="3dabe-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="3dabe-210">d.</span><span class="sxs-lookup"><span data-stu-id="3dabe-210">d.</span></span> <span data-ttu-id="3dabe-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3dabe-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="3dabe-212">Criar um usuário de teste do Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="3dabe-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="3dabe-213">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Autotask.</span><span class="sxs-lookup"><span data-stu-id="3dabe-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="3dabe-214">Trabalhe com [a equipe de suporte local de trabalho Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd usuários Olá Olá plataforma Autotask no local de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3dabe-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd hello users in hello Autotask Workplace platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3dabe-215">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3dabe-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="3dabe-216">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAutotask no local de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3dabe-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAutotask Workplace.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="3dabe-218">**tooassign Britta Simon tooAutotask no local de trabalho, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3dabe-218">**tooassign Britta Simon tooAutotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="3dabe-219">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3dabe-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3dabe-221">Na lista de aplicativos hello, selecione **Autotask trabalho**.</span><span class="sxs-lookup"><span data-stu-id="3dabe-221">In hello applications list, select **Autotask Workplace**.</span></span>

    ![Olá link Autotask no local de trabalho na lista de aplicativos Olá](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="3dabe-223">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3dabe-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="3dabe-225">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3dabe-225">Click **Add** button.</span></span> <span data-ttu-id="3dabe-226">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3dabe-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="3dabe-228">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="3dabe-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3dabe-229">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3dabe-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3dabe-230">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3dabe-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3dabe-231">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="3dabe-231">Test single sign-on</span></span>

<span data-ttu-id="3dabe-232">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="3dabe-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3dabe-233">Quando você clica em Olá Autotask no local de trabalho lado a lado no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de área de trabalho Autotask.</span><span class="sxs-lookup"><span data-stu-id="3dabe-233">When you click hello Autotask Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Autotask Workplace application.</span></span>
<span data-ttu-id="3dabe-234">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3dabe-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3dabe-235">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3dabe-235">Additional resources</span></span>

* [<span data-ttu-id="3dabe-236">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3dabe-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3dabe-237">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3dabe-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

