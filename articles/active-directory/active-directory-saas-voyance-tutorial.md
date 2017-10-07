---
title: "Tutorial: Integração do Azure Active Directory com o Voyance | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Voyance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="7f95f-103">Tutorial: Integração do Azure Active Directory com o Voyance</span><span class="sxs-lookup"><span data-stu-id="7f95f-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="7f95f-104">Neste tutorial, você aprenderá como toointegrate Voyance com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="7f95f-104">In this tutorial, you learn how toointegrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f95f-105">Integrando Voyance com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f95f-105">Integrating Voyance with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7f95f-106">Você pode controlar no AD do Azure que tenha acesso tooVoyance</span><span class="sxs-lookup"><span data-stu-id="7f95f-106">You can control in Azure AD who has access tooVoyance</span></span>
- <span data-ttu-id="7f95f-107">Você pode habilitar seu usuários tooautomatically get conectado tooVoyance (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7f95f-107">You can enable your users tooautomatically get signed-on tooVoyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7f95f-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7f95f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7f95f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7f95f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f95f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7f95f-110">Prerequisites</span></span>

<span data-ttu-id="7f95f-111">tooconfigure integração do AD do Azure com Voyance, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f95f-111">tooconfigure Azure AD integration with Voyance, you need hello following items:</span></span>

- <span data-ttu-id="7f95f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7f95f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f95f-113">Uma assinatura do Voyance habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="7f95f-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f95f-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7f95f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f95f-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7f95f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f95f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7f95f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f95f-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f95f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f95f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7f95f-118">Scenario description</span></span>
<span data-ttu-id="7f95f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7f95f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f95f-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="7f95f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f95f-121">Adicionando Voyance da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7f95f-121">Adding Voyance from hello gallery</span></span>
2. <span data-ttu-id="7f95f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7f95f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-hello-gallery"></a><span data-ttu-id="7f95f-123">Adicionando Voyance da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7f95f-123">Adding Voyance from hello gallery</span></span>
<span data-ttu-id="7f95f-124">integração de saudação tooconfigure de Voyance no AD do Azure, você precisa tooadd Voyance da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7f95f-124">tooconfigure hello integration of Voyance into Azure AD, you need tooadd Voyance from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7f95f-125">**tooadd Voyance da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7f95f-125">**tooadd Voyance from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f95f-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7f95f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="7f95f-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7f95f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7f95f-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7f95f-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="7f95f-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7f95f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="7f95f-133">Na caixa de pesquisa hello, digite **Voyance**, selecione **Voyance** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7f95f-133">In hello search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Voyance na lista de resultados de saudação](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7f95f-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f95f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7f95f-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Voyance, com base em uma usuária de teste chamada “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7f95f-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7f95f-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Voyance é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f95f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Voyance is tooa user in Azure AD.</span></span> <span data-ttu-id="7f95f-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Voyance precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7f95f-138">In other words, a link relationship between an Azure AD user and hello related user in Voyance needs toobe established.</span></span>

<span data-ttu-id="7f95f-139">Voyance, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f95f-139">In Voyance, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7f95f-140">tooconfigure e teste de logon único do AD do Azure com Voyance, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f95f-140">tooconfigure and test Azure AD single sign-on with Voyance, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7f95f-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7f95f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7f95f-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f95f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7f95f-143">**[Criar um usuário de teste Voyance](#create-a-voyance-test-user)**  -toohave um equivalente do Britta Simon em Voyance é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="7f95f-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - toohave a counterpart of Britta Simon in Voyance that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7f95f-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="7f95f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7f95f-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="7f95f-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7f95f-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f95f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7f95f-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Voyance.</span><span class="sxs-lookup"><span data-stu-id="7f95f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="7f95f-148">**tooconfigure AD do Azure-logon único com Voyance, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7f95f-148">**tooconfigure Azure AD single sign-on with Voyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f95f-149">Em Olá portal do Azure, Olá **Voyance** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="7f95f-149">In hello Azure portal, on hello **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="7f95f-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="7f95f-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="7f95f-153">Em Olá **Voyance domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="7f95f-153">On hello **Voyance Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Informações de logon único de Domínio e URLs do Voyance para IdP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="7f95f-155">a.</span><span class="sxs-lookup"><span data-stu-id="7f95f-155">a.</span></span> <span data-ttu-id="7f95f-156">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="7f95f-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="7f95f-157">b.</span><span class="sxs-lookup"><span data-stu-id="7f95f-157">b.</span></span> <span data-ttu-id="7f95f-158">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="7f95f-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="7f95f-159">Verificar **Mostrar configurações de URL avançadas** e executar Olá etapa a seguir se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="7f95f-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Informações de logon único de Domínio e URLs do Voyance para SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="7f95f-161">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="7f95f-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7f95f-162">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="7f95f-162">These values are not real.</span></span> <span data-ttu-id="7f95f-163">Atualizar esses valores com hello real identificador, URL de resposta e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="7f95f-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7f95f-164">Entre em contato com [equipe de suporte do cliente Voyance](mailto:support@nyansa.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="7f95f-164">Contact [Voyance Client support team](mailto:support@nyansa.com) tooget these values.</span></span> 

5. <span data-ttu-id="7f95f-165">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7f95f-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="7f95f-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7f95f-167">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="7f95f-169">Em Olá **Voyance configuração** seção, clique em **configurar Voyance** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="7f95f-169">On hello **Voyance Configuration** section, click **Configure Voyance** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7f95f-170">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="7f95f-170">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="7f95f-172">Em uma janela de navegador web diferente, logon tooyour Voyance locatário como um administrador.</span><span class="sxs-lookup"><span data-stu-id="7f95f-172">In a different web browser window, sign-on tooyour Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="7f95f-173">Vá toohello parte superior direita da barra de navegação hello e clique em Olá suspenso que diz "**University Acme**".</span><span class="sxs-lookup"><span data-stu-id="7f95f-173">Go toohello top right corner of hello navigation bar and click on hello drop-down that says "**Acme University**".</span></span>
    
    ![Configurar o logon único no lado do aplicativo – Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="7f95f-175">Clique em "**Configurações de Administração**".</span><span class="sxs-lookup"><span data-stu-id="7f95f-175">Click "**Admin Settings**".</span></span>

    ![Configurar o logon único no lado do aplicativo – Configurações do Administrador](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="7f95f-177">Clique na guia "**Acesso do Usuário**".</span><span class="sxs-lookup"><span data-stu-id="7f95f-177">Click "**User Access**" tab.</span></span>

    ![Configurar o logon único no lado do aplicativo – Acesso do Usuário](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="7f95f-179">Clique em hello "**SSO está desabilitado**" botão tooconfigure AD do Azure como um IdP usando o SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="7f95f-179">Click hello "**SSO is disabled**" button tooconfigure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Configurar o logon único no lado do aplicativo – SSO está desabilitado](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="7f95f-181">Vá muito**SAML v2** seção e executar etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f95f-181">Go too**SAML v2** section and perform below steps:</span></span>

    ![Configurar o logon único no lado do aplicativo – SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="7f95f-183">a.</span><span class="sxs-lookup"><span data-stu-id="7f95f-183">a.</span></span> <span data-ttu-id="7f95f-184">Selecione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="7f95f-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="7f95f-185">b.</span><span class="sxs-lookup"><span data-stu-id="7f95f-185">b.</span></span> <span data-ttu-id="7f95f-186">Colar **Single Sign-On URL do serviço SAML**, que você copiou de saudação portal do Azure em hello **URL de logon IdP** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="7f95f-186">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal Into hello **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="7f95f-187">c.</span><span class="sxs-lookup"><span data-stu-id="7f95f-187">c.</span></span> <span data-ttu-id="7f95f-188">Abra seu certificado codificado na Base64 baixado no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado IdP** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="7f95f-188">Open your downloaded Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="7f95f-189">d.</span><span class="sxs-lookup"><span data-stu-id="7f95f-189">d.</span></span> <span data-ttu-id="7f95f-190">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7f95f-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7f95f-191">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="7f95f-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7f95f-192">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="7f95f-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7f95f-193">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7f95f-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7f95f-194">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f95f-194">Create an Azure AD test user</span></span>

<span data-ttu-id="7f95f-195">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f95f-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="7f95f-197">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7f95f-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f95f-198">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7f95f-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7f95f-200">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="7f95f-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7f95f-202">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f95f-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botão Adicionar de saudação](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7f95f-204">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f95f-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7f95f-206">a.</span><span class="sxs-lookup"><span data-stu-id="7f95f-206">a.</span></span> <span data-ttu-id="7f95f-207">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f95f-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f95f-208">b.</span><span class="sxs-lookup"><span data-stu-id="7f95f-208">b.</span></span> <span data-ttu-id="7f95f-209">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7f95f-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7f95f-210">c.</span><span class="sxs-lookup"><span data-stu-id="7f95f-210">c.</span></span> <span data-ttu-id="7f95f-211">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="7f95f-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7f95f-212">d.</span><span class="sxs-lookup"><span data-stu-id="7f95f-212">d.</span></span> <span data-ttu-id="7f95f-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7f95f-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="7f95f-214">Criar um usuário de teste do Voyance</span><span class="sxs-lookup"><span data-stu-id="7f95f-214">Create a Voyance test user</span></span>

<span data-ttu-id="7f95f-215">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Voyance.</span><span class="sxs-lookup"><span data-stu-id="7f95f-215">hello objective of this section is toocreate a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="7f95f-216">O Voyance dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="7f95f-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="7f95f-217">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="7f95f-217">There is no action item for you in this section.</span></span> <span data-ttu-id="7f95f-218">Um novo usuário é criado durante uma tentativa tooaccess Voyance se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="7f95f-218">A new user is created during an attempt tooaccess Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="7f95f-219">Se você precisar toocreate um usuário manualmente, será necessário toocontact [a equipe de suporte Voyance](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="7f95f-219">If you need toocreate a user manually, you need toocontact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7f95f-220">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7f95f-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7f95f-221">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooVoyance.</span><span class="sxs-lookup"><span data-stu-id="7f95f-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVoyance.</span></span>

![Atribuir função de usuário Olá][200]

<span data-ttu-id="7f95f-223">**tooassign Britta Simon tooVoyance, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7f95f-223">**tooassign Britta Simon tooVoyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f95f-224">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7f95f-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7f95f-226">Na lista de aplicativos hello, selecione **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="7f95f-226">In hello applications list, select **Voyance**.</span></span>

    ![link de Voyance Olá na lista de aplicativos Olá](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="7f95f-228">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7f95f-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="7f95f-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7f95f-230">Click **Add** button.</span></span> <span data-ttu-id="7f95f-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7f95f-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="7f95f-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f95f-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7f95f-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7f95f-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7f95f-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7f95f-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7f95f-236">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="7f95f-236">Test single sign-on</span></span>

<span data-ttu-id="7f95f-237">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f95f-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7f95f-238">Quando você clica em bloco Voyance Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Voyance aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7f95f-238">When you click hello Voyance tile in hello Access Panel, you should get automatically signed-on tooyour Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7f95f-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7f95f-239">Additional resources</span></span>

* [<span data-ttu-id="7f95f-240">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7f95f-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7f95f-241">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7f95f-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

