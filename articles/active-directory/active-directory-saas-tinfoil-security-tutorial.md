---
title: "Tutorial: integração do Azure Active Directory com o TINFOIL SECURITY | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="a3823-103">Tutorial: integração do Azure Active Directory com o TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="a3823-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="a3823-104">Neste tutorial, você aprenderá como toointegrate TINFOIL SECURITY com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="a3823-104">In this tutorial, you learn how toointegrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a3823-105">Integração do TINFOIL SECURITY com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3823-105">Integrating TINFOIL SECURITY with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a3823-106">Você pode controlar no AD do Azure que tenha acesso tooTINFOIL segurança</span><span class="sxs-lookup"><span data-stu-id="a3823-106">You can control in Azure AD who has access tooTINFOIL SECURITY</span></span>
- <span data-ttu-id="a3823-107">Você pode habilitar seu usuários tooautomatically get conectado tooTINFOIL segurança (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a3823-107">You can enable your users tooautomatically get signed-on tooTINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a3823-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a3823-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a3823-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a3823-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3823-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a3823-110">Prerequisites</span></span>

<span data-ttu-id="a3823-111">tooconfigure integração do AD do Azure com TINFOIL SECURITY, é necessário Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3823-111">tooconfigure Azure AD integration with TINFOIL SECURITY, you need hello following items:</span></span>

- <span data-ttu-id="a3823-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a3823-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a3823-113">Uma assinatura do TINFOIL SECURITY habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="a3823-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a3823-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a3823-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a3823-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a3823-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a3823-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a3823-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a3823-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3823-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a3823-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a3823-118">Scenario description</span></span>
<span data-ttu-id="a3823-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a3823-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a3823-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="a3823-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a3823-121">Adicionar TINFOIL SECURITY da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a3823-121">Add TINFOIL SECURITY from hello gallery</span></span>
2. <span data-ttu-id="a3823-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3823-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-hello-gallery"></a><span data-ttu-id="a3823-123">Adicionar TINFOIL SECURITY da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a3823-123">Add TINFOIL SECURITY from hello gallery</span></span>
<span data-ttu-id="a3823-124">integração de saudação tooconfigure do TINFOIL SECURITY no AD do Azure, você precisa tooadd TINFOIL SECURITY na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a3823-124">tooconfigure hello integration of TINFOIL SECURITY into Azure AD, you need tooadd TINFOIL SECURITY from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a3823-125">**tooadd TINFOIL SECURITY da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a3823-125">**tooadd TINFOIL SECURITY from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3823-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a3823-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a3823-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a3823-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a3823-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a3823-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a3823-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a3823-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a3823-133">Na caixa de pesquisa hello, digite **TINFOIL SECURITY**, selecione **TINFOIL SECURITY** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a3823-133">In hello search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button tooadd hello application.</span></span>

    ![TINFOIL SECURITY da galeria](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a3823-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3823-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a3823-136">Nesta seção, você configurará e testará o logon único do Azure AD com o TINFOIL SECURITY com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a3823-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a3823-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no TINFOIL SECURITY é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3823-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TINFOIL SECURITY is tooa user in Azure AD.</span></span> <span data-ttu-id="a3823-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no TINFOIL SECURITY precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a3823-138">In other words, a link relationship between an Azure AD user and hello related user in TINFOIL SECURITY needs toobe established.</span></span>

<span data-ttu-id="a3823-139">TINFOIL SECURITY, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3823-139">In TINFOIL SECURITY, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a3823-140">tooconfigure e teste de logon único do AD do Azure com TINFOIL SECURITY, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3823-140">tooconfigure and test Azure AD single sign-on with TINFOIL SECURITY, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a3823-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a3823-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a3823-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3823-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a3823-143">**[Criar um usuário de teste do TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave um equivalente do Britta Simon no TINFOIL SECURITY que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="a3823-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - toohave a counterpart of Britta Simon in TINFOIL SECURITY that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a3823-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="a3823-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a3823-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="a3823-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a3823-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3823-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a3823-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="a3823-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="a3823-148">**tooconfigure AD do Azure-logon único com TINFOIL SECURITY, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a3823-148">**tooconfigure Azure AD single sign-on with TINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3823-149">Em Olá portal do Azure, Olá **TINFOIL SECURITY** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="a3823-149">In hello Azure portal, on hello **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a3823-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="a3823-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Logon baseado em SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="a3823-153">Em Olá **TINFOIL SECURITY domínio e URLs** seção, hello usuário não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure.</span><span class="sxs-lookup"><span data-stu-id="a3823-153">On hello **TINFOIL SECURITY Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="a3823-155">Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** valor.</span><span class="sxs-lookup"><span data-stu-id="a3823-155">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value.</span></span>

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="a3823-157">mapeamentos de atributo do tooadd Olá necessária, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3823-157">tooadd hello required attribute mappings, perform hello following steps:</span></span>
    
    <span data-ttu-id="a3823-158">![Atributos](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="a3823-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="a3823-159">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="a3823-159">Attribute Name</span></span>    |   <span data-ttu-id="a3823-160">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="a3823-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="a3823-161">accountid</span><span class="sxs-lookup"><span data-stu-id="a3823-161">accountid</span></span> | <span data-ttu-id="a3823-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="a3823-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="a3823-163">a.</span><span class="sxs-lookup"><span data-stu-id="a3823-163">a.</span></span> <span data-ttu-id="a3823-164">Clique em **adicionar atributo de usuário**.</span><span class="sxs-lookup"><span data-stu-id="a3823-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="a3823-165">![ADICIONAR atributo](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="a3823-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="a3823-166">![ADICIONAR atributo](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="a3823-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="a3823-167">b.</span><span class="sxs-lookup"><span data-stu-id="a3823-167">b.</span></span> <span data-ttu-id="a3823-168">Em Olá **nome do atributo** caixa de texto, tipo **accountid**.</span><span class="sxs-lookup"><span data-stu-id="a3823-168">In hello **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="a3823-169">c.</span><span class="sxs-lookup"><span data-stu-id="a3823-169">c.</span></span> <span data-ttu-id="a3823-170">Em Olá **o valor do atributo** caixa de texto, colar Olá conta valor da ID que você obterá mais tarde no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3823-170">In hello **Attribute Value** textbox, paste hello account ID value which you will get later on hello tutorial.</span></span>
    
    <span data-ttu-id="a3823-171">d.</span><span class="sxs-lookup"><span data-stu-id="a3823-171">d.</span></span> <span data-ttu-id="a3823-172">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a3823-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="a3823-173">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a3823-173">Click **Save** button.</span></span>

    ![Botão Salvar](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="a3823-175">Em Olá **TINFOIL SECURITY Configuration** seção, clique em **configurar TINFOIL SECURITY** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="a3823-175">On hello **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a3823-176">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="a3823-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="a3823-178">Em uma janela diferente do navegador da Web, faça logon no site da empresa TINFOIL SECURITY como administrador.</span><span class="sxs-lookup"><span data-stu-id="a3823-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="a3823-179">Na barra de ferramentas de saudação na parte superior do hello, clique em **minha conta**.</span><span class="sxs-lookup"><span data-stu-id="a3823-179">In hello toolbar on hello top, click **My Account**.</span></span>
   
    <span data-ttu-id="a3823-180">![Painel](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Painel")</span><span class="sxs-lookup"><span data-stu-id="a3823-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="a3823-181">Clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="a3823-181">Click **Security**.</span></span>
   
    <span data-ttu-id="a3823-182">![Segurança](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="a3823-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="a3823-183">Em Olá **Single Sign-On** configuração de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3823-183">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="a3823-184">![Logon Único](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="a3823-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="a3823-185">a.</span><span class="sxs-lookup"><span data-stu-id="a3823-185">a.</span></span> <span data-ttu-id="a3823-186">Selecione **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="a3823-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="a3823-187">b.</span><span class="sxs-lookup"><span data-stu-id="a3823-187">b.</span></span> <span data-ttu-id="a3823-188">Clique em **Configuração Manual**.</span><span class="sxs-lookup"><span data-stu-id="a3823-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="a3823-189">c.</span><span class="sxs-lookup"><span data-stu-id="a3823-189">c.</span></span> <span data-ttu-id="a3823-190">Em **URL de postagem de SAML** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a3823-190">In **SAML Post URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="a3823-191">d.</span><span class="sxs-lookup"><span data-stu-id="a3823-191">d.</span></span> <span data-ttu-id="a3823-192">Em **impressão digital do certificado SAML** caixa de texto valor Olá colar **impressão digital** que você copiou de **o certificado de autenticação SAML** seção.</span><span class="sxs-lookup"><span data-stu-id="a3823-192">In **SAML Certificate Fingerprint** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="a3823-193">e.</span><span class="sxs-lookup"><span data-stu-id="a3823-193">e.</span></span> <span data-ttu-id="a3823-194">Cópia **seu ID de conta** valor e cole o valor de saudação em **o valor do atributo** textbox em **Adicionar atributo** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3823-194">Copy **Your Account ID** value and paste hello value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="a3823-195">f.</span><span class="sxs-lookup"><span data-stu-id="a3823-195">f.</span></span> <span data-ttu-id="a3823-196">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a3823-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a3823-197">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="a3823-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a3823-198">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="a3823-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a3823-199">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a3823-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a3823-200">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3823-200">Create an Azure AD test user</span></span>
<span data-ttu-id="a3823-201">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3823-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a3823-203">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a3823-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3823-204">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a3823-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a3823-206">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="a3823-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="a3823-207">Usuários e grupos -> Todos os usuários</span><span class="sxs-lookup"><span data-stu-id="a3823-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a3823-208">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3823-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Usuário](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a3823-210">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3823-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a3823-212">a.</span><span class="sxs-lookup"><span data-stu-id="a3823-212">a.</span></span> <span data-ttu-id="a3823-213">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a3823-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a3823-214">b.</span><span class="sxs-lookup"><span data-stu-id="a3823-214">b.</span></span> <span data-ttu-id="a3823-215">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a3823-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a3823-216">c.</span><span class="sxs-lookup"><span data-stu-id="a3823-216">c.</span></span> <span data-ttu-id="a3823-217">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="a3823-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a3823-218">d.</span><span class="sxs-lookup"><span data-stu-id="a3823-218">d.</span></span> <span data-ttu-id="a3823-219">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a3823-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="a3823-220">Criar um usuário de teste do TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="a3823-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="a3823-221">Em ordem tooenable AD do Azure usuários toolog no TINFOIL SECURITY, eles devem ser provisionados no TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="a3823-221">In order tooenable Azure AD users toolog into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="a3823-222">No caso de saudação do TINFOIL SECURITY, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="a3823-222">In hello case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="a3823-223">**tooget um usuário provisionado, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a3823-223">**tooget a user provisioned, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3823-224">Se o usuário Olá faz parte de uma conta da empresa, será necessário muito[entre em contato com a equipe de suporte do TINFOIL SECURITY Olá](https://www.tinfoilsecurity.com/contact) tooget Olá conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="a3823-224">If hello user is a part of an Enterprise account, you need too[contact hello TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) tooget hello user account created.</span></span>

2. <span data-ttu-id="a3823-225">Se Olá é um usuário regular do TINFOIL SECURITY SaaS, usuário Olá pode adicionar tooany um colaborador de sites saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="a3823-225">If hello user is a regular TINFOIL SECURITY SaaS user, then hello user can add a collaborator tooany of hello user’s sites.</span></span> <span data-ttu-id="a3823-226">Email desse aciona um toosend de processo especificado um convite toohello toocreate uma nova conta de usuário do TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="a3823-226">This triggers a process toosend an invitation toohello specified email toocreate a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="a3823-227">Você pode usar qualquer ferramenta de criação outros TINFOIL SECURITY usuário conta ou APIs fornecidas pelo TINFOIL SECURITY tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3823-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY tooprovision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a3823-228">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a3823-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a3823-229">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTINFOIL segurança.</span><span class="sxs-lookup"><span data-stu-id="a3823-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTINFOIL SECURITY.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a3823-231">**tooassign Britta Simon tooTINFOIL segurança, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a3823-231">**tooassign Britta Simon tooTINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3823-232">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a3823-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a3823-234">Na lista de aplicativos hello, selecione **TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="a3823-234">In hello applications list, select **TINFOIL SECURITY**.</span></span>

    ![selecione TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="a3823-236">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a3823-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a3823-238">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a3823-238">Click **Add** button.</span></span> <span data-ttu-id="a3823-239">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a3823-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a3823-241">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3823-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a3823-242">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a3823-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a3823-243">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a3823-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a3823-244">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="a3823-244">Test single sign-on</span></span>

<span data-ttu-id="a3823-245">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3823-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a3823-246">Quando você clica em bloco TINFOIL SECURITY Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="a3823-246">When you click hello TINFOIL SECURITY tile in hello Access Panel, you should get automatically signed-on tooyour TINFOIL SECURITY application.</span></span> <span data-ttu-id="a3823-247">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a3823-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a3823-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a3823-248">Additional resources</span></span>

* [<span data-ttu-id="a3823-249">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a3823-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a3823-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a3823-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

