---
title: "Tutorial: integração do Azure Active Directory ao Mixpanel | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Mixpanel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 8da8aaefee3558c37babe3e10aeba4224ceffa16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="278ec-103">Tutorial: Integração do Active Directory do Azure com o Mixpanel</span><span class="sxs-lookup"><span data-stu-id="278ec-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="278ec-104">Neste tutorial, você aprenderá como toointegrate Mixpanel com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="278ec-104">In this tutorial, you learn how toointegrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="278ec-105">Integrando Mixpanel com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="278ec-105">Integrating Mixpanel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="278ec-106">Você pode controlar no AD do Azure que tenha acesso tooMixpanel</span><span class="sxs-lookup"><span data-stu-id="278ec-106">You can control in Azure AD who has access tooMixpanel</span></span>
- <span data-ttu-id="278ec-107">Você pode habilitar seu usuários tooautomatically get conectado tooMixpanel (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="278ec-107">You can enable your users tooautomatically get signed-on tooMixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="278ec-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="278ec-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="278ec-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="278ec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="278ec-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="278ec-110">Prerequisites</span></span>

<span data-ttu-id="278ec-111">tooconfigure integração do AD do Azure com Mixpanel, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="278ec-111">tooconfigure Azure AD integration with Mixpanel, you need hello following items:</span></span>

- <span data-ttu-id="278ec-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="278ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="278ec-113">Uma assinatura habilitada para logon único do Mixpanel</span><span class="sxs-lookup"><span data-stu-id="278ec-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="278ec-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="278ec-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="278ec-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="278ec-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="278ec-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="278ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="278ec-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="278ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="278ec-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="278ec-118">Scenario description</span></span>
<span data-ttu-id="278ec-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="278ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="278ec-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="278ec-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="278ec-121">Adicionando Mixpanel da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="278ec-121">Adding Mixpanel from hello gallery</span></span>
2. <span data-ttu-id="278ec-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="278ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-hello-gallery"></a><span data-ttu-id="278ec-123">Adicionando Mixpanel da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="278ec-123">Adding Mixpanel from hello gallery</span></span>
<span data-ttu-id="278ec-124">integração de saudação tooconfigure de Mixpanel no AD do Azure, você precisa tooadd Mixpanel da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="278ec-124">tooconfigure hello integration of Mixpanel into Azure AD, you need tooadd Mixpanel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="278ec-125">**tooadd Mixpanel da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="278ec-125">**tooadd Mixpanel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="278ec-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="278ec-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="278ec-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="278ec-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="278ec-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="278ec-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="278ec-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="278ec-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="278ec-133">Na caixa de pesquisa hello, digite **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="278ec-133">In hello search box, type **Mixpanel**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="278ec-135">No painel de resultados de saudação, selecione **Mixpanel**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="278ec-135">In hello results panel, select **Mixpanel**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="278ec-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="278ec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="278ec-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Mixpanel, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="278ec-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="278ec-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Mixpanel é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="278ec-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mixpanel is tooa user in Azure AD.</span></span> <span data-ttu-id="278ec-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Mixpanel precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="278ec-140">In other words, a link relationship between an Azure AD user and hello related user in Mixpanel needs toobe established.</span></span>

<span data-ttu-id="278ec-141">Mixpanel, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="278ec-141">In Mixpanel, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="278ec-142">tooconfigure e teste de logon único do AD do Azure com Mixpanel, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="278ec-142">tooconfigure and test Azure AD single sign-on with Mixpanel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="278ec-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="278ec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="278ec-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="278ec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="278ec-145">**[Criar um usuário de teste Mixpanel](#creating-a-mixpanel-test-user)**  -toohave um equivalente do Britta Simon em Mixpanel é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="278ec-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - toohave a counterpart of Britta Simon in Mixpanel that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="278ec-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="278ec-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="278ec-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="278ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="278ec-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="278ec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="278ec-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="278ec-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="278ec-150">**tooconfigure AD do Azure-logon único com Mixpanel, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="278ec-150">**tooconfigure Azure AD single sign-on with Mixpanel, perform hello following steps:**</span></span>

1. <span data-ttu-id="278ec-151">Em Olá portal do Azure, Olá **Mixpanel** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="278ec-151">In hello Azure portal, on hello **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="278ec-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="278ec-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="278ec-155">Em Olá **Mixpanel domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="278ec-155">On hello **Mixpanel Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="278ec-157">Em Olá **URL de logon** caixa de texto, digite um URL como:`https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="278ec-157">In hello **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="278ec-158">Registre-se em [https://mixpanel.com/register/](https://mixpanel.com/register/) tooset backup suas credenciais de logon e contato Olá [Mixpanel a equipe de suporte](mailto:support@mixpanel.com) tooenable configurações de SSO para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="278ec-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) tooset up your login credentials and  contact hello [Mixpanel support team](mailto:support@mixpanel.com) tooenable SSO settings for your tenant.</span></span> <span data-ttu-id="278ec-159">Você também poderá obter o valor da URL de Entrada, se for necessário, da equipe de suporte do Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="278ec-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="278ec-160">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="278ec-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="278ec-162">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="278ec-162">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="278ec-164">Em Olá **Mixpanel configuração** seção, clique em **configurar Mixpanel** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="278ec-164">On hello **Mixpanel Configuration** section, click **Configure Mixpanel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="278ec-165">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="278ec-165">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="278ec-167">Em uma janela de navegador diferente, logon tooyour Mixpanel aplicativo como um administrador.</span><span class="sxs-lookup"><span data-stu-id="278ec-167">In a different browser window, sign-on tooyour Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="278ec-168">Na parte inferior da página de saudação, clique em Olá pouco **engrenagem** ícone no canto esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="278ec-168">On bottom of hello page, click hello little **gear** icon in hello left corner.</span></span> 
   
    ![Logon único do Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="278ec-170">Clique em Olá **segurança de acesso** guia e, em seguida, clique em **alterar configurações**.</span><span class="sxs-lookup"><span data-stu-id="278ec-170">Click hello **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Configurações do Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="278ec-172">Em Olá **alterar seu certificado** página da caixa de diálogo, clique em **Escolher arquivo** tooupload seu certificado baixado e clique **próximo**.</span><span class="sxs-lookup"><span data-stu-id="278ec-172">On hello **Change your certificate** dialog page, click **Choose file** tooupload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Configurações do Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="278ec-174">Na caixa de texto do URL de autenticação de Olá em Olá **alterar a URL de autenticação** página de diálogo Colar Olá valor **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="278ec-174">In hello authentication URL textbox on hello **Change your authentication  URL** dialog page, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Configurações do Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="278ec-176">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="278ec-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="278ec-177">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="278ec-177">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="278ec-178">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="278ec-178">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="278ec-179">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="278ec-179">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="278ec-180">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="278ec-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="278ec-181">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="278ec-181">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="278ec-183">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="278ec-183">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="278ec-184">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="278ec-184">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="278ec-186">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="278ec-186">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="278ec-188">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="278ec-188">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="278ec-190">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="278ec-190">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="278ec-192">a.</span><span class="sxs-lookup"><span data-stu-id="278ec-192">a.</span></span> <span data-ttu-id="278ec-193">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="278ec-193">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="278ec-194">b.</span><span class="sxs-lookup"><span data-stu-id="278ec-194">b.</span></span> <span data-ttu-id="278ec-195">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="278ec-195">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="278ec-196">c.</span><span class="sxs-lookup"><span data-stu-id="278ec-196">c.</span></span> <span data-ttu-id="278ec-197">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="278ec-197">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="278ec-198">d.</span><span class="sxs-lookup"><span data-stu-id="278ec-198">d.</span></span> <span data-ttu-id="278ec-199">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="278ec-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="278ec-200">Criação de um usuário de teste do Mixpanel</span><span class="sxs-lookup"><span data-stu-id="278ec-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="278ec-201">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="278ec-201">hello objective of this section is toocreate a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="278ec-202">Faça logon no tooyour Mixpanel site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="278ec-202">Sign on tooyour Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="278ec-203">Na parte inferior de saudação da página Olá, clique em Olá engrenagem pequeno botão Olá Olá de tooopen canto esquerdo **configurações** janela.</span><span class="sxs-lookup"><span data-stu-id="278ec-203">On hello bottom of hello page, click hello little gear button on hello left corner tooopen hello **Settings** window.</span></span>

3. <span data-ttu-id="278ec-204">Clique em Olá **equipe** guia.</span><span class="sxs-lookup"><span data-stu-id="278ec-204">Click hello **Team** tab.</span></span>

4. <span data-ttu-id="278ec-205">Em Olá **membro da equipe** caixa de texto, digite o endereço de email de Britta saudação do Azure.</span><span class="sxs-lookup"><span data-stu-id="278ec-205">In hello **team member** textbox, type Britta's email address in hello Azure.</span></span>
   
    ![Configurações do Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="278ec-207">Clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="278ec-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="278ec-208">Olá usuário verá um tooset email perfil hello.</span><span class="sxs-lookup"><span data-stu-id="278ec-208">hello user will get an email tooset up hello profile.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="278ec-209">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="278ec-209">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="278ec-210">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMixpanel.</span><span class="sxs-lookup"><span data-stu-id="278ec-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMixpanel.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="278ec-212">**tooassign Britta Simon tooMixpanel, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="278ec-212">**tooassign Britta Simon tooMixpanel, perform hello following steps:**</span></span>

1. <span data-ttu-id="278ec-213">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="278ec-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="278ec-215">Na lista de aplicativos hello, selecione **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="278ec-215">In hello applications list, select **Mixpanel**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="278ec-217">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="278ec-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="278ec-219">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="278ec-219">Click **Add** button.</span></span> <span data-ttu-id="278ec-220">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="278ec-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="278ec-222">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="278ec-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="278ec-223">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="278ec-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="278ec-224">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="278ec-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="278ec-225">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="278ec-225">Testing single sign-on</span></span>

<span data-ttu-id="278ec-226">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="278ec-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="278ec-227">Quando você clica em bloco Mixpanel Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Mixpanel aplicativo.</span><span class="sxs-lookup"><span data-stu-id="278ec-227">When you click hello Mixpanel tile in hello Access Panel, you should get automatically signed-on tooyour Mixpanel application.</span></span>
<span data-ttu-id="278ec-228">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="278ec-228">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="278ec-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="278ec-229">Additional resources</span></span>

* [<span data-ttu-id="278ec-230">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="278ec-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="278ec-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="278ec-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

