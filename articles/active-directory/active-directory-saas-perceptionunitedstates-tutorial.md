---
title: "Tutorial: Integração do Azure Active Directory ao Perception United States (não UltiPro) | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Estados Unidos de percepção (Non-UltiPro)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="4b0f5-103">Tutorial: Integração do Azure Active Directory ao Perception United States (não UltiPro)</span><span class="sxs-lookup"><span data-stu-id="4b0f5-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="4b0f5-104">Neste tutorial, você aprenderá como toointegrate EUA percepção (Non-UltiPro) com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="4b0f5-104">In this tutorial, you learn how toointegrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b0f5-105">Integração dos Estados Unidos de percepção (Non-UltiPro) com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b0f5-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4b0f5-106">Você pode controlar no AD do Azure que tenha acesso tooPerception Estados Unidos (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="4b0f5-106">You can control in Azure AD who has access tooPerception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="4b0f5-107">Você pode habilitar seu usuários tooautomatically get conectado tooPerception Estados Unidos (Non-UltiPro) (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-107">You can enable your users tooautomatically get signed-on tooPerception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4b0f5-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="4b0f5-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b0f5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b0f5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4b0f5-110">Prerequisites</span></span>

<span data-ttu-id="4b0f5-111">tooconfigure integração do Azure AD com percepção dos Estados Unidos (Non-UltiPro), você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b0f5-111">tooconfigure Azure AD integration with Perception United States (Non-UltiPro), you need hello following items:</span></span>

- <span data-ttu-id="4b0f5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b0f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b0f5-113">Uma assinatura habilitada para logon único do Perception United States (não UltiPro)</span><span class="sxs-lookup"><span data-stu-id="4b0f5-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b0f5-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b0f5-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4b0f5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b0f5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b0f5-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b0f5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b0f5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4b0f5-118">Scenario description</span></span>
<span data-ttu-id="4b0f5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b0f5-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="4b0f5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b0f5-121">Adicionar Estados Unidos de percepção (Non-UltiPro) da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4b0f5-121">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
2. <span data-ttu-id="4b0f5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b0f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a><span data-ttu-id="4b0f5-123">Adicionar Estados Unidos de percepção (Non-UltiPro) da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4b0f5-123">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
<span data-ttu-id="4b0f5-124">integração de saudação do tooconfigure de percepção dos Estados Unidos (Non-UltiPro) no AD do Azure, você precisa tooadd dos Estados Unidos de percepção (Non-UltiPro) na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-124">tooconfigure hello integration of Perception United States (Non-UltiPro) into Azure AD, you need tooadd Perception United States (Non-UltiPro) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4b0f5-125">**tooadd EUA percepção (Non-UltiPro) da Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4b0f5-125">**tooadd Perception United States (Non-UltiPro) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b0f5-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="4b0f5-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4b0f5-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="4b0f5-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="4b0f5-133">Na caixa de pesquisa hello, digite **dos Estados Unidos de percepção (Non-UltiPro)**, selecione **dos Estados Unidos de percepção (Non-UltiPro)** no painel de resultados e clique em **adicionar** tooadd de botão aplicativo Hello.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-133">In hello search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![EUA percepção (Non-UltiPro) na lista de resultados de saudação](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4b0f5-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b0f5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4b0f5-136">Nesta seção, você configura e testa o logon único do Azure AD com o Perception United States (não UltiPro) com base em uma usuária de teste chamada “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4b0f5-137">Para toowork de logon único, o AD do Azure precisa tooknow que o usuário de contraparte Olá no percepção dos Estados Unidos (Non-UltiPro) é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Perception United States (Non-UltiPro) is tooa user in Azure AD.</span></span> <span data-ttu-id="4b0f5-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em percepção dos Estados Unidos (Non-UltiPro) precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-138">In other words, a link relationship between an Azure AD user and hello related user in Perception United States (Non-UltiPro) needs toobe established.</span></span>

<span data-ttu-id="4b0f5-139">No percepção dos Estados Unidos (Non-UltiPro), atribua o valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-139">In Perception United States (Non-UltiPro), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4b0f5-140">tooconfigure e teste de logon único do AD do Azure com percepção dos Estados Unidos (Non-UltiPro), você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b0f5-140">tooconfigure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4b0f5-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4b0f5-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b0f5-143">**[Criar um usuário de teste dos Estados Unidos de percepção (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave um equivalente de Britta Simon no percepção dos Estados Unidos (Non-UltiPro) que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - toohave a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b0f5-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b0f5-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4b0f5-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b0f5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4b0f5-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de percepção Brasil (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="4b0f5-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="4b0f5-148">**tooconfigure AD do Azure-logon único com percepção dos Estados Unidos (Non-UltiPro), execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4b0f5-148">**tooconfigure Azure AD single sign-on with Perception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="4b0f5-149">Em Olá portal do Azure, Olá **dos Estados Unidos de percepção (Non-UltiPro)** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-149">In hello Azure portal, on hello **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="4b0f5-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="4b0f5-153">Em Olá **domínio EstadosUnidos percepção (Non-UltiPro) e as URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b0f5-153">On hello **Perception United States (Non-UltiPro) Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações sobre logon único de domínio e URLs do Perception United States (não UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="4b0f5-155">a.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-155">a.</span></span> <span data-ttu-id="4b0f5-156">Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://perception.kanjoya.com/sp`</span><span class="sxs-lookup"><span data-stu-id="4b0f5-156">In hello **Identifier** textbox, type hello URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="4b0f5-157">b.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-157">b.</span></span> <span data-ttu-id="4b0f5-158">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="4b0f5-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b0f5-159">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-159">hello value is not real.</span></span> <span data-ttu-id="4b0f5-160">Você atualizará o valor de saudação com hello real URL de resposta, que é explicada posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-160">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="4b0f5-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="4b0f5-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4b0f5-163">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b0f5-165">Em Olá **dos Estados Unidos de percepção (Non-UltiPro) configuração** seção, clique em **configurar percepção dos Estados Unidos (Non-UltiPro)** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-165">On hello **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4b0f5-166">Saudação de cópia **ID da entidade SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="4b0f5-166">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="4b0f5-167">a.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-167">a.</span></span> <span data-ttu-id="4b0f5-168">Olá **percepção Brasil (Non-UltiPro)** aplicativo requer Olá **ID da entidade SAML** valor, o que você copiou toobe uri codificado.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-168">hello **Perception United States (Non-UltiPro)** application requires hello **SAML Entity ID** value, which you have copied, toobe uri encoded.</span></span> <span data-ttu-id="4b0f5-169">valor de uri codificado do tooget hello, use a seguir Olá vincular:**http://www.url-encode-decode.com/**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-169">tooget hello uri encoded value, use hello following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="4b0f5-170">b.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-170">b.</span></span> <span data-ttu-id="4b0f5-171">Depois de obter o uri de saudação valor codificado combiná-lo com hello **URL de resposta** conforme mencionado abaixo -</span><span class="sxs-lookup"><span data-stu-id="4b0f5-171">After getting hello uri encoded value combine it with hello **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="4b0f5-172">c.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-172">c.</span></span> <span data-ttu-id="4b0f5-173">Olá colar acima do valor em Olá **URL de resposta** textbox em **domínio EstadosUnidos percepção (Non-UltiPro) e as URLs** seção.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-173">Paste hello above value in hello **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Configuração do Perception United States (não UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="4b0f5-175">Em outra janela do navegador, entre no site da empresa dos Estados Unidos de percepção (Non-UltiPro) tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-175">In another browser window, sign on tooyour Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="4b0f5-176">Na barra de ferramentas principal hello, clique em **configurações de conta**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-176">In hello main toolbar, click **Account Settings**.</span></span>

    ![Usuário do Perception United States (não UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="4b0f5-178">Em Olá **configurações de conta** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b0f5-178">On hello **Account Settings** page, perform hello following steps:</span></span>

    ![Usuário do Perception United States (não UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="4b0f5-180">a.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-180">a.</span></span> <span data-ttu-id="4b0f5-181">Em Olá **nome da empresa** caixa de texto Nome do tipo hello de saudação **empresa**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-181">In hello **Company Name** textbox, type hello name of hello **Company**.</span></span>
    
    <span data-ttu-id="4b0f5-182">b.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-182">b.</span></span> <span data-ttu-id="4b0f5-183">Em Olá **nome da conta** caixa de texto Nome do tipo hello de saudação **conta**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-183">In hello **Account Name** textbox, type hello name of hello **Account**.</span></span>

    <span data-ttu-id="4b0f5-184">c.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-184">c.</span></span> <span data-ttu-id="4b0f5-185">Em **padrão resposta-tooEmail** caixa de texto, a saudação de tipo válida **Email**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-185">In **Default Reply-tooEmail** text box, type hello valid **Email**.</span></span>

    <span data-ttu-id="4b0f5-186">d.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-186">d.</span></span> <span data-ttu-id="4b0f5-187">Selecione **Provedor de identidade SSO** como **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="4b0f5-188">Em Olá **configuração SSO** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b0f5-188">On hello **SSO Configuration** page, perform hello following steps:</span></span>

    ![SSOConfig do Perception United States (não UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="4b0f5-190">a.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-190">a.</span></span> <span data-ttu-id="4b0f5-191">Selecione **Tipo de SAML NameID** como **EMAIL**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="4b0f5-192">b.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-192">b.</span></span> <span data-ttu-id="4b0f5-193">Em Olá **nome de configuração de SSO** caixa de texto, nome de saudação do tipo do seu **configuração**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-193">In hello **SSO Configuration Name** textbox, type hello name of your **Configuration**.</span></span>
    
    <span data-ttu-id="4b0f5-194">c.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-194">c.</span></span> <span data-ttu-id="4b0f5-195">Em **nome do provedor de identidade** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-195">In **Identity Provider Name** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="4b0f5-196">d.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-196">d.</span></span> <span data-ttu-id="4b0f5-197">Em **caixa de texto de domínio de SAML**, digite Olá domínio como  **@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="4b0f5-197">In **SAML Domain textbox**, enter hello domain like **@contoso.com**.</span></span>

    <span data-ttu-id="4b0f5-198">e.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-198">e.</span></span> <span data-ttu-id="4b0f5-199">Clique em **carregar novamente** Olá tooupload **Metadata XML** arquivo.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-199">Click on **Upload Again** tooupload hello **Metadata XML** file.</span></span>

    <span data-ttu-id="4b0f5-200">f.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-200">f.</span></span> <span data-ttu-id="4b0f5-201">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="4b0f5-202">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="4b0f5-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4b0f5-203">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4b0f5-204">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b0f5-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4b0f5-205">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b0f5-205">Create an Azure AD test user</span></span>

<span data-ttu-id="4b0f5-206">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="4b0f5-208">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4b0f5-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b0f5-209">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4b0f5-211">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4b0f5-213">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4b0f5-215">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b0f5-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4b0f5-217">a.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-217">a.</span></span> <span data-ttu-id="4b0f5-218">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b0f5-219">b.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-219">b.</span></span> <span data-ttu-id="4b0f5-220">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="4b0f5-221">c.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-221">c.</span></span> <span data-ttu-id="4b0f5-222">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="4b0f5-223">d.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-223">d.</span></span> <span data-ttu-id="4b0f5-224">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="4b0f5-225">Criar um usuário de teste do Perception United States (não UltiPro)</span><span class="sxs-lookup"><span data-stu-id="4b0f5-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="4b0f5-226">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Perception United States (não UltiPro).</span><span class="sxs-lookup"><span data-stu-id="4b0f5-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="4b0f5-227">Trabalhar com [a equipe de suporte dos Estados Unidos de percepção (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd usuários de saudação na plataforma do hello percepção Brasil (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="4b0f5-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd hello users in hello Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4b0f5-228">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b0f5-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4b0f5-229">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPerception EUA (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="4b0f5-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerception United States (Non-UltiPro).</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="4b0f5-231">**tooassign Britta Simon tooPerception EUA (Non-UltiPro), execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4b0f5-231">**tooassign Britta Simon tooPerception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="4b0f5-232">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4b0f5-234">Na lista de aplicativos hello, selecione **dos Estados Unidos de percepção (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-234">In hello applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![link do Hello percepção Brasil (Non-UltiPro) na lista de aplicativos Olá](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="4b0f5-236">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="4b0f5-238">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-238">Click **Add** button.</span></span> <span data-ttu-id="4b0f5-239">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="4b0f5-241">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4b0f5-242">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b0f5-243">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4b0f5-244">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="4b0f5-244">Test single sign-on</span></span>

<span data-ttu-id="4b0f5-245">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b0f5-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4b0f5-246">Quando você clica em um bloco de percepção Brasil (Non-UltiPro) Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo percepção Brasil (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="4b0f5-246">When you click hello Perception United States (Non-UltiPro) tile in hello Access Panel, you should get automatically signed-on tooyour Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="4b0f5-247">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4b0f5-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4b0f5-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4b0f5-248">Additional resources</span></span>

* [<span data-ttu-id="4b0f5-249">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4b0f5-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b0f5-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b0f5-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

