---
title: "Tutorial: integração do Azure Active Directory com o Workstars | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Workstars."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 86250d7538f058d2a821ded7dda0b2fc185d80df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="64a5b-103">Tutorial: integração do Azure Active Directory com o Workstars</span><span class="sxs-lookup"><span data-stu-id="64a5b-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="64a5b-104">Neste tutorial, você aprenderá como toointegrate Workstars com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="64a5b-104">In this tutorial, you learn how toointegrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64a5b-105">Integrando Workstars com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="64a5b-105">Integrating Workstars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="64a5b-106">Você pode controlar no AD do Azure que tenha acesso tooWorkstars.</span><span class="sxs-lookup"><span data-stu-id="64a5b-106">You can control in Azure AD who has access tooWorkstars.</span></span>
- <span data-ttu-id="64a5b-107">Você pode habilitar seus usuários tooautomatically get conectado tooWorkstars (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="64a5b-107">You can enable your users tooautomatically get signed-on tooWorkstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="64a5b-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="64a5b-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="64a5b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64a5b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64a5b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="64a5b-110">Prerequisites</span></span>

<span data-ttu-id="64a5b-111">tooconfigure integração do AD do Azure com Workstars, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="64a5b-111">tooconfigure Azure AD integration with Workstars, you need hello following items:</span></span>

- <span data-ttu-id="64a5b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64a5b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="64a5b-113">Uma assinatura do Workstars habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="64a5b-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="64a5b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="64a5b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="64a5b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="64a5b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="64a5b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="64a5b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="64a5b-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64a5b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64a5b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="64a5b-118">Scenario description</span></span>
<span data-ttu-id="64a5b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="64a5b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="64a5b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="64a5b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64a5b-121">Adicionando Workstars da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="64a5b-121">Adding Workstars from hello gallery</span></span>
2. <span data-ttu-id="64a5b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64a5b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-hello-gallery"></a><span data-ttu-id="64a5b-123">Adicionando Workstars da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="64a5b-123">Adding Workstars from hello gallery</span></span>
<span data-ttu-id="64a5b-124">integração de saudação tooconfigure de Workstars no AD do Azure, você precisa tooadd Workstars da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="64a5b-124">tooconfigure hello integration of Workstars into Azure AD, you need tooadd Workstars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="64a5b-125">**tooadd Workstars da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="64a5b-125">**tooadd Workstars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="64a5b-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="64a5b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="64a5b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="64a5b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="64a5b-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64a5b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="64a5b-133">Na caixa de pesquisa hello, digite **Workstars**, selecione **Workstars** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="64a5b-133">In hello search box, type **Workstars**, select **Workstars** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workstars na lista de resultados de saudação](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="64a5b-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a5b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="64a5b-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Workstars, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="64a5b-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="64a5b-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Workstars é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="64a5b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workstars is tooa user in Azure AD.</span></span> <span data-ttu-id="64a5b-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Workstars precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="64a5b-138">In other words, a link relationship between an Azure AD user and hello related user in Workstars needs toobe established.</span></span>

<span data-ttu-id="64a5b-139">Workstars, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="64a5b-139">In Workstars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="64a5b-140">tooconfigure e teste de logon único do AD do Azure com Workstars, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="64a5b-140">tooconfigure and test Azure AD single sign-on with Workstars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="64a5b-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="64a5b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="64a5b-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64a5b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64a5b-143">**[Criar um usuário de teste Workstars](#create-a-workstars-test-user)**  -toohave um equivalente do Britta Simon em Workstars é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="64a5b-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - toohave a counterpart of Britta Simon in Workstars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="64a5b-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="64a5b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64a5b-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="64a5b-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="64a5b-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a5b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="64a5b-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Workstars.</span><span class="sxs-lookup"><span data-stu-id="64a5b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="64a5b-148">**tooconfigure AD do Azure-logon único com Workstars, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="64a5b-148">**tooconfigure Azure AD single sign-on with Workstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="64a5b-149">Em Olá portal do Azure, Olá **Workstars** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-149">In hello Azure portal, on hello **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="64a5b-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="64a5b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="64a5b-153">Em Olá **Workstars domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="64a5b-153">On hello **Workstars Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="64a5b-155">a.</span><span class="sxs-lookup"><span data-stu-id="64a5b-155">a.</span></span> <span data-ttu-id="64a5b-156">Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="64a5b-156">In hello **Identifier** textbox, type hello URL: `https://workstars.com`</span></span>

    <span data-ttu-id="64a5b-157">b.</span><span class="sxs-lookup"><span data-stu-id="64a5b-157">b.</span></span> <span data-ttu-id="64a5b-158">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="64a5b-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="64a5b-159">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="64a5b-159">hello value is not real.</span></span> <span data-ttu-id="64a5b-160">Valor de saudação de atualização com hello URL de resposta real.</span><span class="sxs-lookup"><span data-stu-id="64a5b-160">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="64a5b-161">Entre em contato com [Workstars equipe de suporte](https://support.workstars.com) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="64a5b-161">Contact [Workstars support team](https://support.workstars.com) tooget hello value.</span></span>
 
4. <span data-ttu-id="64a5b-162">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="64a5b-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="64a5b-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="64a5b-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="64a5b-166">Em Olá **Workstars configuração** seção, clique em **configurar Workstars** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="64a5b-166">On hello **Workstars Configuration** section, click **Configure Workstars** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="64a5b-167">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="64a5b-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="64a5b-169">Em outra janela do navegador, entre no site da empresa Workstars tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="64a5b-169">In another browser window, sign on tooyour Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="64a5b-170">Na barra de ferramentas principal hello, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-170">In hello main toolbar, click **Settings**.</span></span>

    ![Configurações do Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="64a5b-172">Vá muito**logon** > **configurações**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-172">Go too**Sign On** > **Settings**.</span></span>

    ![Logon do Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Configurações do Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="64a5b-175">Em Olá **única entrada em SAML () - configurações** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="64a5b-175">On hello **Single Sign On (SAML) - Settings** page, perform hello following steps:</span></span>
    
    ![SAML do Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="64a5b-177">a.</span><span class="sxs-lookup"><span data-stu-id="64a5b-177">a.</span></span> <span data-ttu-id="64a5b-178">Na caixa de texto **Nome do Provedor de Identidade**, digite **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="64a5b-179">b.</span><span class="sxs-lookup"><span data-stu-id="64a5b-179">b.</span></span> <span data-ttu-id="64a5b-180">Em hello **ID de entidade do provedor de identidade** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="64a5b-180">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="64a5b-181">c.</span><span class="sxs-lookup"><span data-stu-id="64a5b-181">c.</span></span> <span data-ttu-id="64a5b-182">Copie o conteúdo de Olá Olá baixado do arquivo de certificado no bloco de notas e, em seguida, cole-o em Olá **x509 certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="64a5b-182">Copy hello content of hello downloaded certificate file in notepad, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="64a5b-183">d.</span><span class="sxs-lookup"><span data-stu-id="64a5b-183">d.</span></span> <span data-ttu-id="64a5b-184">Em Olá **URL SSO SAML** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="64a5b-184">In hello **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="64a5b-185">e.</span><span class="sxs-lookup"><span data-stu-id="64a5b-185">e.</span></span> <span data-ttu-id="64a5b-186">Em Olá **URL de Logout remoto** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="64a5b-186">In hello **Remote Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="64a5b-187">f.</span><span class="sxs-lookup"><span data-stu-id="64a5b-187">f.</span></span> <span data-ttu-id="64a5b-188">Selecione **ID de Nome** como **Email (Padrão)**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="64a5b-189">g.</span><span class="sxs-lookup"><span data-stu-id="64a5b-189">g.</span></span> <span data-ttu-id="64a5b-190">Clique em **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="64a5b-191">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="64a5b-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="64a5b-192">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="64a5b-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="64a5b-193">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="64a5b-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="64a5b-194">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a5b-194">Create an Azure AD test user</span></span>

<span data-ttu-id="64a5b-195">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="64a5b-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="64a5b-197">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="64a5b-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="64a5b-198">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="64a5b-198">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="64a5b-200">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-200">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="64a5b-202">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64a5b-202">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="64a5b-204">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="64a5b-204">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="64a5b-206">a.</span><span class="sxs-lookup"><span data-stu-id="64a5b-206">a.</span></span> <span data-ttu-id="64a5b-207">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-207">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="64a5b-208">b.</span><span class="sxs-lookup"><span data-stu-id="64a5b-208">b.</span></span> <span data-ttu-id="64a5b-209">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64a5b-209">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="64a5b-210">c.</span><span class="sxs-lookup"><span data-stu-id="64a5b-210">c.</span></span> <span data-ttu-id="64a5b-211">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="64a5b-211">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="64a5b-212">d.</span><span class="sxs-lookup"><span data-stu-id="64a5b-212">d.</span></span> <span data-ttu-id="64a5b-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="64a5b-214">Criar um usuário de teste do Workstars</span><span class="sxs-lookup"><span data-stu-id="64a5b-214">Create a Workstars test user</span></span>

<span data-ttu-id="64a5b-215">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Workstars.</span><span class="sxs-lookup"><span data-stu-id="64a5b-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="64a5b-216">Trabalhar com [Workstars equipe de suporte](https://support.workstars.com) tooadd usuários de saudação na plataforma de Workstars hello.</span><span class="sxs-lookup"><span data-stu-id="64a5b-216">Work with [Workstars support team](https://support.workstars.com) tooadd hello users in hello Workstars platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="64a5b-217">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="64a5b-217">Assign hello Azure AD test user</span></span>

<span data-ttu-id="64a5b-218">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWorkstars.</span><span class="sxs-lookup"><span data-stu-id="64a5b-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkstars.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="64a5b-220">**tooassign Britta Simon tooWorkstars, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="64a5b-220">**tooassign Britta Simon tooWorkstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="64a5b-221">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="64a5b-223">Na lista de aplicativos hello, selecione **Workstars**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-223">In hello applications list, select **Workstars**.</span></span>

    ![link de Workstars Olá na lista de aplicativos Olá](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="64a5b-225">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="64a5b-227">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="64a5b-227">Click **Add** button.</span></span> <span data-ttu-id="64a5b-228">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64a5b-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="64a5b-230">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="64a5b-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="64a5b-231">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64a5b-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="64a5b-232">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64a5b-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="64a5b-233">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="64a5b-233">Test single sign-on</span></span>

<span data-ttu-id="64a5b-234">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="64a5b-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="64a5b-235">Quando você clica em Olá Workstars bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Workstars aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64a5b-235">When you click hello Workstars tile in hello Access Panel, you should get automatically signed-on tooyour Workstars application.</span></span>
<span data-ttu-id="64a5b-236">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="64a5b-236">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="64a5b-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="64a5b-237">Additional resources</span></span>

* [<span data-ttu-id="64a5b-238">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="64a5b-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64a5b-239">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="64a5b-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

