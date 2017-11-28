---
title: "Tutorial: integração do Azure Active Directory com o GaggleAMP | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e GaggleAMP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9761019a79f935b6695a5ae1214c256c887df457
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="9ac92-103">Tutorial: Integração do Active Directory do Azure com o GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="9ac92-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="9ac92-104">Neste tutorial, você aprenderá como toointegrate GaggleAMP com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="9ac92-104">In this tutorial, you learn how toointegrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9ac92-105">Integrando GaggleAMP com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ac92-105">Integrating GaggleAMP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9ac92-106">Você pode controlar no AD do Azure que tenha acesso tooGaggleAMP</span><span class="sxs-lookup"><span data-stu-id="9ac92-106">You can control in Azure AD who has access tooGaggleAMP</span></span>
- <span data-ttu-id="9ac92-107">Você pode habilitar seu usuários tooautomatically get conectado tooGaggleAMP (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ac92-107">You can enable your users tooautomatically get signed-on tooGaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9ac92-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9ac92-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9ac92-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9ac92-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ac92-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9ac92-110">Prerequisites</span></span>

<span data-ttu-id="9ac92-111">tooconfigure integração do AD do Azure com GaggleAMP, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ac92-111">tooconfigure Azure AD integration with GaggleAMP, you need hello following items:</span></span>

- <span data-ttu-id="9ac92-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ac92-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9ac92-113">Uma assinatura do GaggleAMP com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="9ac92-113">A GaggleAMP single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9ac92-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9ac92-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9ac92-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9ac92-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9ac92-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9ac92-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9ac92-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9ac92-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9ac92-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9ac92-118">Scenario description</span></span>
<span data-ttu-id="9ac92-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9ac92-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9ac92-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="9ac92-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9ac92-121">Adicionando GaggleAMP da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9ac92-121">Adding GaggleAMP from hello gallery</span></span>
2. <span data-ttu-id="9ac92-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ac92-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-hello-gallery"></a><span data-ttu-id="9ac92-123">Adicionando GaggleAMP da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9ac92-123">Adding GaggleAMP from hello gallery</span></span>
<span data-ttu-id="9ac92-124">integração de saudação tooconfigure de GaggleAMP no AD do Azure, você precisa tooadd GaggleAMP da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9ac92-124">tooconfigure hello integration of GaggleAMP into Azure AD, you need tooadd GaggleAMP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9ac92-125">**tooadd GaggleAMP da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9ac92-125">**tooadd GaggleAMP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ac92-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9ac92-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9ac92-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9ac92-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9ac92-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9ac92-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9ac92-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ac92-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9ac92-133">Na caixa de pesquisa hello, digite **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="9ac92-133">In hello search box, type **GaggleAMP**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. <span data-ttu-id="9ac92-135">No painel de resultados de saudação, selecione **GaggleAMP**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9ac92-135">In hello results panel, select **GaggleAMP**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9ac92-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ac92-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9ac92-138">Nesta seção, você configura e testa o logon único do Azure AD com o GaggleAMP com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="9ac92-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9ac92-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em GaggleAMP é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac92-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GaggleAMP is tooa user in Azure AD.</span></span> <span data-ttu-id="9ac92-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em GaggleAMP precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9ac92-140">In other words, a link relationship between an Azure AD user and hello related user in GaggleAMP needs toobe established.</span></span>

<span data-ttu-id="9ac92-141">GaggleAMP, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ac92-141">In GaggleAMP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9ac92-142">tooconfigure e teste de logon único do AD do Azure com GaggleAMP, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ac92-142">tooconfigure and test Azure AD single sign-on with GaggleAMP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9ac92-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9ac92-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9ac92-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9ac92-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9ac92-145">**[Criar um usuário de teste GaggleAMP](#creating-a-gaggleamp-test-user)**  -toohave um equivalente do Britta Simon em GaggleAMP é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="9ac92-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - toohave a counterpart of Britta Simon in GaggleAMP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9ac92-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="9ac92-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9ac92-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="9ac92-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9ac92-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ac92-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9ac92-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="9ac92-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="9ac92-150">**tooconfigure AD do Azure-logon único com GaggleAMP, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9ac92-150">**tooconfigure Azure AD single sign-on with GaggleAMP, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ac92-151">Em Olá portal do Azure, Olá **GaggleAMP** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="9ac92-151">In hello Azure portal, on hello **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9ac92-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="9ac92-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. <span data-ttu-id="9ac92-155">Em Olá **GaggleAMP domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ac92-155">On hello **GaggleAMP Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="9ac92-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.gaggleamp.com`</span><span class="sxs-lookup"><span data-stu-id="9ac92-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.gaggleamp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9ac92-158">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="9ac92-158">hello value is not real.</span></span> <span data-ttu-id="9ac92-159">Valor de saudação de atualização com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="9ac92-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="9ac92-160">Entre em contato com [equipe de suporte do cliente GaggleAMP](mailto:sales@gaggleamp.com) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ac92-160">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="9ac92-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9ac92-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. <span data-ttu-id="9ac92-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9ac92-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9ac92-165">Em Olá **GaggleAMP configuração** seção, clique em **configurar GaggleAMP** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="9ac92-165">On hello **GaggleAMP Configuration** section, click **Configure GaggleAMP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9ac92-166">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="9ac92-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. <span data-ttu-id="9ac92-168">Em outra instância do navegador, navegue toohello página SSO do SAML criada para você por Olá alguns equipe de suporte (por exemplo: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="9ac92-168">In another browser instance, navigate toohello SAML SSO page created for you by hello Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

8. <span data-ttu-id="9ac92-169">Em seu **SSO do SAML** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ac92-169">On your **SAML SSO** page, perform hello following steps:</span></span>  
   
    ![Logon único do GaggleAMP](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    <span data-ttu-id="9ac92-171">a.</span><span class="sxs-lookup"><span data-stu-id="9ac92-171">a.</span></span> <span data-ttu-id="9ac92-172">Em Olá **emissor do provedor de identidade** caixa de texto valor Olá colar **URL do emissor** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac92-172">In hello **Identity Provider Issuer** textbox, paste hello value of **Issuer URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="9ac92-173">b.</span><span class="sxs-lookup"><span data-stu-id="9ac92-173">b.</span></span> <span data-ttu-id="9ac92-174">Em Olá **URL provedor de identidade Single Sign-On** caixa de texto valor Olá colar **o URL de serviço de logon único** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac92-174">In hello **Identity Provider Single Sign-On URL** textbox, paste hello  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="9ac92-175">c.</span><span class="sxs-lookup"><span data-stu-id="9ac92-175">c.</span></span> <span data-ttu-id="9ac92-176">Clique em **Salvar**</span><span class="sxs-lookup"><span data-stu-id="9ac92-176">Click **Save**</span></span>      

    <span data-ttu-id="9ac92-177">d.</span><span class="sxs-lookup"><span data-stu-id="9ac92-177">d.</span></span> <span data-ttu-id="9ac92-178">Enviar Olá **certificado (Base64)** certificado tooyour [a equipe de suporte GaggleAMP](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="9ac92-178">Send hello **Certificate (Base64)** certificate tooyour [GaggleAMP support team](mailto:sales@gaggleamp.com).</span></span>

> [!TIP]
> <span data-ttu-id="9ac92-179">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="9ac92-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9ac92-180">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="9ac92-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9ac92-181">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9ac92-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9ac92-182">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ac92-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="9ac92-183">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac92-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9ac92-185">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9ac92-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ac92-186">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9ac92-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9ac92-188">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="9ac92-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9ac92-190">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ac92-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9ac92-192">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ac92-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9ac92-194">a.</span><span class="sxs-lookup"><span data-stu-id="9ac92-194">a.</span></span> <span data-ttu-id="9ac92-195">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9ac92-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9ac92-196">b.</span><span class="sxs-lookup"><span data-stu-id="9ac92-196">b.</span></span> <span data-ttu-id="9ac92-197">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9ac92-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9ac92-198">c.</span><span class="sxs-lookup"><span data-stu-id="9ac92-198">c.</span></span> <span data-ttu-id="9ac92-199">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="9ac92-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9ac92-200">d.</span><span class="sxs-lookup"><span data-stu-id="9ac92-200">d.</span></span> <span data-ttu-id="9ac92-201">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9ac92-201">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="9ac92-202">Criação de um usuário de teste do GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="9ac92-202">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="9ac92-203">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="9ac92-203">hello objective of this section is toocreate a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="9ac92-204">O GaggleAMP dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="9ac92-204">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="9ac92-205">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="9ac92-205">There is no action item for you in this section.</span></span> <span data-ttu-id="9ac92-206">Um novo usuário é criado durante uma tentativa tooaccess GaggleAMP se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="9ac92-206">A new user is created during an attempt tooaccess GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9ac92-207">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ac92-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9ac92-208">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooGaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="9ac92-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGaggleAMP.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9ac92-210">**tooassign Britta Simon tooGaggleAMP, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9ac92-210">**tooassign Britta Simon tooGaggleAMP, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ac92-211">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9ac92-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9ac92-213">Na lista de aplicativos hello, selecione **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="9ac92-213">In hello applications list, select **GaggleAMP**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. <span data-ttu-id="9ac92-215">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9ac92-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9ac92-217">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9ac92-217">Click **Add** button.</span></span> <span data-ttu-id="9ac92-218">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ac92-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9ac92-220">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ac92-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9ac92-221">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ac92-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9ac92-222">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ac92-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9ac92-223">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9ac92-223">Testing single sign-on</span></span>

<span data-ttu-id="9ac92-224">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="9ac92-224">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="9ac92-225">Quando você clica em bloco GaggleAMP Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour GaggleAMP aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9ac92-225">When you click hello GaggleAMP tile in hello Access Panel, you should get automatically signed-on tooyour GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ac92-226">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9ac92-226">Additional resources</span></span>

* [<span data-ttu-id="9ac92-227">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9ac92-227">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ac92-228">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9ac92-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

