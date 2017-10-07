---
title: "Tutorial: Integração do Azure Active Directory com o Work.com | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="84ea9-103">Tutorial: Integração do Active Directory do Azure com o Work.com</span><span class="sxs-lookup"><span data-stu-id="84ea9-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="84ea9-104">Neste tutorial, você aprenderá como toointegrate Work.com com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="84ea9-104">In this tutorial, you learn how toointegrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="84ea9-105">Integrando o Work.com com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="84ea9-105">Integrating Work.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="84ea9-106">Você pode controlar no AD do Azure que tenha acesso tooWork.com</span><span class="sxs-lookup"><span data-stu-id="84ea9-106">You can control in Azure AD who has access tooWork.com</span></span>
- <span data-ttu-id="84ea9-107">Você pode habilitar seus usuários tooautomatically get conectado tooWork.com (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="84ea9-107">You can enable your users tooautomatically get signed-on tooWork.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="84ea9-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="84ea9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="84ea9-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="84ea9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84ea9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="84ea9-110">Prerequisites</span></span>

<span data-ttu-id="84ea9-111">tooconfigure integração do AD do Azure com o Work.com, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="84ea9-111">tooconfigure Azure AD integration with Work.com, you need hello following items:</span></span>

- <span data-ttu-id="84ea9-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="84ea9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="84ea9-113">Uma assinatura do Work.com habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="84ea9-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84ea9-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="84ea9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="84ea9-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="84ea9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="84ea9-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="84ea9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="84ea9-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84ea9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="84ea9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="84ea9-118">Scenario description</span></span>
<span data-ttu-id="84ea9-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="84ea9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="84ea9-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="84ea9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="84ea9-121">Adicionar Work.com da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="84ea9-121">Add Work.com from hello gallery</span></span>
2. <span data-ttu-id="84ea9-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="84ea9-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-hello-gallery"></a><span data-ttu-id="84ea9-123">Adicionar Work.com da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="84ea9-123">Add Work.com from hello gallery</span></span>
<span data-ttu-id="84ea9-124">integração de saudação tooconfigure da Work.com no AD do Azure, você precisa tooadd Work.com na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="84ea9-124">tooconfigure hello integration of Work.com into Azure AD, you need tooadd Work.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="84ea9-125">**tooadd Work.com da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="84ea9-125">**tooadd Work.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="84ea9-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="84ea9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="84ea9-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="84ea9-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="84ea9-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="84ea9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="84ea9-133">Na caixa de pesquisa hello, digite **Work.com**, selecione **Work.com** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="84ea9-133">In hello search box, type **Work.com**, select **Work.com** from results panel then click **Add** button tooadd hello application.</span></span>

    ![Adicionar da galeria](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="84ea9-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="84ea9-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="84ea9-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Work.com, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="84ea9-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="84ea9-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na Work.com é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="84ea9-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Work.com is tooa user in Azure AD.</span></span> <span data-ttu-id="84ea9-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na Work.com precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="84ea9-138">In other words, a link relationship between an Azure AD user and hello related user in Work.com needs toobe established.</span></span>

<span data-ttu-id="84ea9-139">Na Work.com, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="84ea9-139">In Work.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="84ea9-140">tooconfigure e teste de logon único do AD do Azure com o Work.com, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="84ea9-140">tooconfigure and test Azure AD single sign-on with Work.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="84ea9-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="84ea9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="84ea9-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="84ea9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84ea9-143">**[Criar um usuário de teste do Work.com](#create-a-workcom-test-user)**  -toohave um equivalente do Britta Simon na Work.com que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="84ea9-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - toohave a counterpart of Britta Simon in Work.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="84ea9-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="84ea9-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84ea9-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="84ea9-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="84ea9-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="84ea9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="84ea9-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo da Work.com.</span><span class="sxs-lookup"><span data-stu-id="84ea9-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="84ea9-148">tooconfigure logon único, você precisa ainda toosetup um nome de domínio personalizado do Work.com.</span><span class="sxs-lookup"><span data-stu-id="84ea9-148">tooconfigure single sign-on, you need toosetup a custom Work.com domain name yet.</span></span> <span data-ttu-id="84ea9-149">Você precisa toodefine pelo menos um domínio nome, teste seu nome de domínio e implantá-lo tooyour toda a organização.</span><span class="sxs-lookup"><span data-stu-id="84ea9-149">You need toodefine at least a domain name, test your domain name, and deploy it tooyour entire organization.</span></span>

<span data-ttu-id="84ea9-150">**tooconfigure AD do Azure-logon único com o Work.com, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="84ea9-150">**tooconfigure Azure AD single sign-on with Work.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="84ea9-151">Em Olá portal do Azure, Olá **Work.com** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-151">In hello Azure portal, on hello **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="84ea9-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="84ea9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Logon único baseado em SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="84ea9-155">Em Olá **Work.com domínio e URLs** , execute o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="84ea9-155">On hello **Work.com Domain and URLs** section, perform hello following:</span></span>

    ![Seção Domínio e URLs do Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="84ea9-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="84ea9-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="84ea9-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="84ea9-158">This value is not real.</span></span> <span data-ttu-id="84ea9-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="84ea9-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="84ea9-160">Entre em contato com [equipe de suporte do cliente Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="84ea9-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) tooget this value.</span></span> 

4. <span data-ttu-id="84ea9-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="84ea9-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="84ea9-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="84ea9-163">Click **Save** button.</span></span>

    ![Botão Salvar](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="84ea9-165">Em Olá **Work.com configuração** seção, clique em **configurar Work.com** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="84ea9-165">On hello **Work.com Configuration** section, click **Configure Work.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="84ea9-166">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="84ea9-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Seção Configuração do Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="84ea9-168">Faça logon no tooyour locatário do Work.com como administrador.</span><span class="sxs-lookup"><span data-stu-id="84ea9-168">Log in tooyour Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="84ea9-169">Vá muito**instalação**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-169">Go too**Setup**.</span></span>
   
    <span data-ttu-id="84ea9-170">![Configuração](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="84ea9-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="84ea9-171">No painel de navegação à esquerda do hello, no hello **administrar** seção, clique em **gerenciamento de domínio** tooexpand Olá seção relacionada e, em seguida, clique em **meu domínio** tooopen Olá  **Meu domínio** página.</span><span class="sxs-lookup"><span data-stu-id="84ea9-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
    <span data-ttu-id="84ea9-172">![Meu Domínio](./media/active-directory-saas-work-com-tutorial/ic767825.png "Meu Domínio")</span><span class="sxs-lookup"><span data-stu-id="84ea9-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="84ea9-173">tooverify seu domínio foi configurado corretamente, certifique-se de que ela está em "**etapa 4 implantado tooUsers**" e examine seu "**minhas configurações de domínio**".</span><span class="sxs-lookup"><span data-stu-id="84ea9-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="84ea9-174">![Domínio implantado tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser domínio implantado")</span><span class="sxs-lookup"><span data-stu-id="84ea9-174">![Domain Deployed tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="84ea9-175">Faça logon no tooyour locatário do Work.com.</span><span class="sxs-lookup"><span data-stu-id="84ea9-175">Log in tooyour Work.com tenant.</span></span>

12. <span data-ttu-id="84ea9-176">Vá muito**instalação**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-176">Go too**Setup**.</span></span>
    
    <span data-ttu-id="84ea9-177">![Configuração](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="84ea9-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="84ea9-178">Expanda Olá **controles de segurança** menu e clique **configurações de logon único**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-178">Expand hello **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="84ea9-179">![Configurações de Logon Único](./media/active-directory-saas-work-com-tutorial/ic794113.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="84ea9-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="84ea9-180">Em Olá **configurações de logon único** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="84ea9-180">On hello **Single Sign-On Settings** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="84ea9-181">![SAML habilitado](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML habilitado")</span><span class="sxs-lookup"><span data-stu-id="84ea9-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="84ea9-182">a.</span><span class="sxs-lookup"><span data-stu-id="84ea9-182">a.</span></span> <span data-ttu-id="84ea9-183">Selecione **SAML Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="84ea9-184">b.</span><span class="sxs-lookup"><span data-stu-id="84ea9-184">b.</span></span> <span data-ttu-id="84ea9-185">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-185">Click **New**.</span></span>

15. <span data-ttu-id="84ea9-186">Em Olá **configurações de logon único SAML** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="84ea9-186">In hello **SAML Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="84ea9-187">![Configurações de Logon Único do SAML](./media/active-directory-saas-work-com-tutorial/ic794114.png "Configurações de Logon Único do SAML")</span><span class="sxs-lookup"><span data-stu-id="84ea9-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="84ea9-188">a.</span><span class="sxs-lookup"><span data-stu-id="84ea9-188">a.</span></span> <span data-ttu-id="84ea9-189">Em Olá **nome** caixa de texto, digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="84ea9-189">In hello **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="84ea9-190">Fornecer um valor para **nome** preencher automaticamente Olá **nome da API** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="84ea9-190">Providing a value for **Name** does automatically populate hello **API Name** textbox.</span></span>
    
    <span data-ttu-id="84ea9-191">b.</span><span class="sxs-lookup"><span data-stu-id="84ea9-191">b.</span></span> <span data-ttu-id="84ea9-192">Em **emissor** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="84ea9-192">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="84ea9-193">c.</span><span class="sxs-lookup"><span data-stu-id="84ea9-193">c.</span></span> <span data-ttu-id="84ea9-194">certificado do tooupload Olá baixado do portal do Azure, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-194">tooupload hello downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="84ea9-195">d.</span><span class="sxs-lookup"><span data-stu-id="84ea9-195">d.</span></span> <span data-ttu-id="84ea9-196">Em Olá **Id da entidade** caixa de texto, tipo `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="84ea9-196">In hello **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="84ea9-197">e.</span><span class="sxs-lookup"><span data-stu-id="84ea9-197">e.</span></span> <span data-ttu-id="84ea9-198">Como **tipo de identidade SAML**, selecione **asserção contém Olá ID de Federação do objeto de usuário Olá**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-198">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
    
    <span data-ttu-id="84ea9-199">f.</span><span class="sxs-lookup"><span data-stu-id="84ea9-199">f.</span></span> <span data-ttu-id="84ea9-200">Como **local da identidade do SAML**, selecione **identidade está no elemento Nameidentifier Olá Olá declaração assunto**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-200">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>
    
    <span data-ttu-id="84ea9-201">g.</span><span class="sxs-lookup"><span data-stu-id="84ea9-201">g.</span></span> <span data-ttu-id="84ea9-202">Em **URL de logon do provedor de identidade** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="84ea9-202">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="84ea9-203">h.</span><span class="sxs-lookup"><span data-stu-id="84ea9-203">h.</span></span> <span data-ttu-id="84ea9-204">Em **URL de Logout do provedor de identidade** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="84ea9-204">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="84ea9-205">i.</span><span class="sxs-lookup"><span data-stu-id="84ea9-205">i.</span></span> <span data-ttu-id="84ea9-206">Para **Associação de Solicitação Iniciada pelo Provedor de Serviços**, selecione **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="84ea9-207">j.</span><span class="sxs-lookup"><span data-stu-id="84ea9-207">j.</span></span> <span data-ttu-id="84ea9-208">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-208">Click **Save**.</span></span>

16. <span data-ttu-id="84ea9-209">No portal clássico do Work.com, no painel de navegação esquerdo hello, clique em **gerenciamento de domínio** tooexpand Olá seção relacionada e, em seguida, clique em **meu domínio** tooopen Olá **meu domínio**página.</span><span class="sxs-lookup"><span data-stu-id="84ea9-209">In your Work.com classic portal, on hello left navigation pane, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="84ea9-210">![Meu Domínio](./media/active-directory-saas-work-com-tutorial/ic794115.png "Meu Domínio")</span><span class="sxs-lookup"><span data-stu-id="84ea9-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="84ea9-211">Em Olá **meu domínio** página Olá **identidade visual da página de logon** seção, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-211">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="84ea9-212">![Identidade Visual da Página de Logon](./media/active-directory-saas-work-com-tutorial/ic767826.png "Identidade Visual da Página de Logon")</span><span class="sxs-lookup"><span data-stu-id="84ea9-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="84ea9-213">Em Olá **identidade visual da página de logon** página Olá **serviço de autenticação** seção, o nome de saudação do seu **configurações de SSO do SAML** é exibido.</span><span class="sxs-lookup"><span data-stu-id="84ea9-213">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="84ea9-214">Selecione-o e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="84ea9-215">![Identidade Visual da Página de Logon](./media/active-directory-saas-work-com-tutorial/ic784366.png "Identidade Visual da Página de Logon")</span><span class="sxs-lookup"><span data-stu-id="84ea9-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="84ea9-216">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="84ea9-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="84ea9-217">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="84ea9-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="84ea9-218">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="84ea9-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="84ea9-219">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="84ea9-219">Create an Azure AD test user</span></span>
<span data-ttu-id="84ea9-220">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="84ea9-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="84ea9-222">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="84ea9-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="84ea9-223">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="84ea9-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="84ea9-225">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Usuários e grupos -> Todos os usuários](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="84ea9-227">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="84ea9-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Adicionar](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="84ea9-229">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="84ea9-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Página da caixa de diálogo do usuário](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="84ea9-231">a.</span><span class="sxs-lookup"><span data-stu-id="84ea9-231">a.</span></span> <span data-ttu-id="84ea9-232">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="84ea9-233">b.</span><span class="sxs-lookup"><span data-stu-id="84ea9-233">b.</span></span> <span data-ttu-id="84ea9-234">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="84ea9-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="84ea9-235">c.</span><span class="sxs-lookup"><span data-stu-id="84ea9-235">c.</span></span> <span data-ttu-id="84ea9-236">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="84ea9-237">d.</span><span class="sxs-lookup"><span data-stu-id="84ea9-237">d.</span></span> <span data-ttu-id="84ea9-238">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="84ea9-239">Criar um usuário de teste do Work.com</span><span class="sxs-lookup"><span data-stu-id="84ea9-239">Create a Work.com test user</span></span>
<span data-ttu-id="84ea9-240">Para o Active Directory do Azure usuários toobe capaz de toosign no, eles devem ser provisionados tooWork.com. No caso de saudação do Work.com, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="84ea9-240">For Azure Active Directory users toobe able toosign in, they must be provisioned tooWork.com. In hello case of Work.com, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="84ea9-241">tooconfigure provisionamento de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="84ea9-241">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="84ea9-242">Faça logon no tooyour site da empresa Work.com como administrador.</span><span class="sxs-lookup"><span data-stu-id="84ea9-242">Sign on tooyour Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="84ea9-243">Vá muito**instalação**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-243">Go too**Setup**.</span></span>
   
    <span data-ttu-id="84ea9-244">![Configuração](./media/active-directory-saas-work-com-tutorial/IC794108.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="84ea9-244">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="84ea9-245">Vá muito**gerenciar usuários \> usuários**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-245">Go too**Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="84ea9-246">![Gerenciar Usuários](./media/active-directory-saas-work-com-tutorial/IC784369.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="84ea9-246">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="84ea9-247">Clique em **Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-247">Click **New User**.</span></span>
   
    <span data-ttu-id="84ea9-248">![Todos os Usuários](./media/active-directory-saas-work-com-tutorial/IC794117.png "Todos os Usuários")</span><span class="sxs-lookup"><span data-stu-id="84ea9-248">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="84ea9-249">Olá seção editar usuários, executar Olá seguindo as etapas, em atributos de um válida do Azure relacionados de conta do AD desejados tooprovision para Olá caixas de texto:</span><span class="sxs-lookup"><span data-stu-id="84ea9-249">In hello User Edit section, perform hello following steps, in attributes of a valid Azure AD account you want tooprovision into hello related textboxes:</span></span>
   
    <span data-ttu-id="84ea9-250">![Editar Usuário](./media/active-directory-saas-work-com-tutorial/ic794118.png "Editar Usuário")</span><span class="sxs-lookup"><span data-stu-id="84ea9-250">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="84ea9-251">a.</span><span class="sxs-lookup"><span data-stu-id="84ea9-251">a.</span></span> <span data-ttu-id="84ea9-252">Em Olá **nome** caixa de texto, Olá tipo **nome** do usuário Olá **Britta**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-252">In hello **First Name** textbox, type hello **first name** of hello user **Britta**.</span></span>
    
    <span data-ttu-id="84ea9-253">b.</span><span class="sxs-lookup"><span data-stu-id="84ea9-253">b.</span></span> <span data-ttu-id="84ea9-254">Em Olá **Sobrenome** caixa de texto, Olá tipo **Sobrenome** do usuário Olá **Simon**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-254">In hello **Last Name** textbox, type hello **last name** of hello user **Simon**.</span></span>
    
    <span data-ttu-id="84ea9-255">c.</span><span class="sxs-lookup"><span data-stu-id="84ea9-255">c.</span></span> <span data-ttu-id="84ea9-256">Em Olá **Alias** caixa de texto, Olá tipo **nome** do usuário Olá **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-256">In hello **Alias** textbox, type hello **name** of hello user **BrittaS**.</span></span>
    
    <span data-ttu-id="84ea9-257">d.</span><span class="sxs-lookup"><span data-stu-id="84ea9-257">d.</span></span> <span data-ttu-id="84ea9-258">Em Olá **Email** caixa de texto, Olá tipo **endereço de email** do usuário  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="84ea9-258">In hello **Email** textbox, type hello **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="84ea9-259">e.</span><span class="sxs-lookup"><span data-stu-id="84ea9-259">e.</span></span> <span data-ttu-id="84ea9-260">Em Olá **nome de usuário** caixa de texto, digite um nome de usuário do usuário como  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="84ea9-260">In hello **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="84ea9-261">f.</span><span class="sxs-lookup"><span data-stu-id="84ea9-261">f.</span></span> <span data-ttu-id="84ea9-262">Em Olá **apelido** caixa de texto, digite um **apelido** do usuário **Simon**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-262">In hello **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="84ea9-263">g.</span><span class="sxs-lookup"><span data-stu-id="84ea9-263">g.</span></span> <span data-ttu-id="84ea9-264">Selecione **Função**, **Licença de Usuário** e **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-264">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="84ea9-265">h.</span><span class="sxs-lookup"><span data-stu-id="84ea9-265">h.</span></span> <span data-ttu-id="84ea9-266">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-266">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="84ea9-267">proprietário de conta do AD do Azure Olá receberá um email com uma conta de saudação do link tooconfirm antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="84ea9-267">hello Azure AD account holder will get an email including a link tooconfirm hello account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="84ea9-268">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="84ea9-268">Assign hello Azure AD test user</span></span>

<span data-ttu-id="84ea9-269">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWork.com.</span><span class="sxs-lookup"><span data-stu-id="84ea9-269">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWork.com.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="84ea9-271">**tooassign Britta Simon tooWork.com, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="84ea9-271">**tooassign Britta Simon tooWork.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="84ea9-272">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-272">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="84ea9-274">Na lista de aplicativos hello, selecione **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-274">In hello applications list, select **Work.com**.</span></span>

    ![Work.com na lista do aplicativo](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="84ea9-276">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-276">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="84ea9-278">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="84ea9-278">Click **Add** button.</span></span> <span data-ttu-id="84ea9-279">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="84ea9-279">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="84ea9-281">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="84ea9-281">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="84ea9-282">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="84ea9-282">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="84ea9-283">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="84ea9-283">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="84ea9-284">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="84ea9-284">Test single sign-on</span></span>

<span data-ttu-id="84ea9-285">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="84ea9-285">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="84ea9-286">Quando você clica em bloco Work.com Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo da Work.com.</span><span class="sxs-lookup"><span data-stu-id="84ea9-286">When you click hello Work.com tile in hello Access Panel, you should get automatically signed-on tooyour Work.com application.</span></span>
<span data-ttu-id="84ea9-287">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="84ea9-287">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84ea9-288">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="84ea9-288">Additional resources</span></span>

* [<span data-ttu-id="84ea9-289">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="84ea9-289">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84ea9-290">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="84ea9-290">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

