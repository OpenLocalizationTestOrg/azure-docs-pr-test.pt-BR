---
title: "Tutorial: Integração do Azure Active Directory com o 8x8 Virtual Office | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e 8x8 Virtual Office."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: df5c5de77285cd3912b68cc3b1e3eee274aa951c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="b520c-103">Tutorial: Integração do Azure Active Directory com o 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="b520c-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="b520c-104">Neste tutorial, você aprenderá como toointegrate 8x8 Office Virtual com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="b520c-104">In this tutorial, you learn how toointegrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b520c-105">Integrando 8x8 Office Virtual com o Azure AD fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="b520c-105">Integrating 8x8 Virtual Office with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b520c-106">Você pode controlar no AD do Azure que tenha acesso too8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="b520c-106">You can control in Azure AD who has access too8x8 Virtual Office</span></span>
- <span data-ttu-id="b520c-107">Você pode habilitar os usuários a obter tooautomatically assinado no too8x8 Virtual do Office (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b520c-107">You can enable your users tooautomatically get signed-on too8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b520c-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b520c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b520c-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b520c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b520c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b520c-110">Prerequisites</span></span>

<span data-ttu-id="b520c-111">tooconfigure integração do AD do Azure com 8x8 Virtual Office, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="b520c-111">tooconfigure Azure AD integration with 8x8 Virtual Office, you need hello following items:</span></span>

- <span data-ttu-id="b520c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b520c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b520c-113">Uma assinatura habilitada para logon único do 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="b520c-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b520c-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b520c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b520c-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b520c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b520c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b520c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b520c-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b520c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b520c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b520c-118">Scenario description</span></span>
<span data-ttu-id="b520c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b520c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b520c-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="b520c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b520c-121">Adicionando 8x8 Virtual Office da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b520c-121">Adding 8x8 Virtual Office from hello gallery</span></span>
2. <span data-ttu-id="b520c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b520c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-hello-gallery"></a><span data-ttu-id="b520c-123">Adicionando 8x8 Virtual Office da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b520c-123">Adding 8x8 Virtual Office from hello gallery</span></span>
<span data-ttu-id="b520c-124">integração de Olá tooconfigure do Office de Virtual 8x8 no AD do Azure, você precisa tooadd 8x8 Office Virtual da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="b520c-124">tooconfigure hello integration of 8x8 Virtual Office into Azure AD, you need tooadd 8x8 Virtual Office from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b520c-125">**tooadd 8x8 Office Virtual da Galeria hello, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b520c-125">**tooadd 8x8 Virtual Office from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b520c-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b520c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b520c-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b520c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b520c-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b520c-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="b520c-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b520c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="b520c-133">Na caixa de pesquisa hello, digite **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="b520c-133">In hello search box, type **8x8 Virtual Office**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="b520c-135">No painel de resultados de saudação, selecione **8x8 Virtual Office**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b520c-135">In hello results panel, select **8x8 Virtual Office**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b520c-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b520c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b520c-138">Nesta seção, você configura e testa o logon único do Azure AD com o 8x8 Virtual Office, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="b520c-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b520c-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá 8x8 Virtual escritório é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b520c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 8x8 Virtual Office is tooa user in Azure AD.</span></span> <span data-ttu-id="b520c-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em 8x8 Office Virtual precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b520c-140">In other words, a link relationship between an Azure AD user and hello related user in 8x8 Virtual Office needs toobe established.</span></span>

<span data-ttu-id="b520c-141">8x8 Virtual Office, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="b520c-141">In 8x8 Virtual Office, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b520c-142">tooconfigure e teste de logon único do AD do Azure com 8x8 Virtual Office, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="b520c-142">tooconfigure and test Azure AD single sign-on with 8x8 Virtual Office, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b520c-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b520c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b520c-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b520c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b520c-145">**[Criar um usuário de teste do Office Virtual 8x8](#creating-a-8x8-virtual-office-test-user)**  -toohave um equivalente do Britta Simon 8x8 Virtual escritório que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="b520c-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - toohave a counterpart of Britta Simon in 8x8 Virtual Office that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b520c-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="b520c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b520c-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="b520c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b520c-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b520c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b520c-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Office Virtual 8x8.</span><span class="sxs-lookup"><span data-stu-id="b520c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="b520c-150">**tooconfigure logon único do AD do Azure com o Office de Virtual 8x8, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b520c-150">**tooconfigure Azure AD single sign-on with 8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="b520c-151">Em Olá portal do Azure, Olá **8x8 Virtual Office** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="b520c-151">In hello Azure portal, on hello **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="b520c-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="b520c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="b520c-155">Em Olá **URLs e domínio Virtual 8x8** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b520c-155">On hello **8x8 Virtual Office Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="b520c-157">a.</span><span class="sxs-lookup"><span data-stu-id="b520c-157">a.</span></span> <span data-ttu-id="b520c-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="b520c-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="b520c-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="b520c-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="b520c-160">b.</span><span class="sxs-lookup"><span data-stu-id="b520c-160">b.</span></span> <span data-ttu-id="b520c-161">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="b520c-161">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="b520c-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="b520c-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b520c-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="b520c-163">These values are not real.</span></span> <span data-ttu-id="b520c-164">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="b520c-164">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="b520c-165">Entre em contato com [equipe de suporte do Office Virtual 8x8](https://www.8x8.com/about-us/contact-us) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="b520c-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) tooget these values.</span></span>
 


4. <span data-ttu-id="b520c-166">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Raw)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="b520c-166">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="b520c-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b520c-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b520c-170">Em Olá **8x8 Virtual Office configuração** seção, clique em **Office Virtual configurar 8x8** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="b520c-170">On hello **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b520c-171">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="b520c-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="b520c-173">Locatário do Office Virtual tooyour logon 8x8 como um administrador.</span><span class="sxs-lookup"><span data-stu-id="b520c-173">Sign-on tooyour 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="b520c-174">Selecione **Virtual Office Account Mgr** no painel do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b520c-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Configurar no lado do aplicativo](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="b520c-176">Selecione **Business** toomanage de conta e clique em **entrar** botão.</span><span class="sxs-lookup"><span data-stu-id="b520c-176">Select **Business** account toomanage and click **Sign In** button.</span></span>
   
    ![Configurar no lado do aplicativo](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="b520c-178">Clique em **contas** guia na lista de saudação do menu.</span><span class="sxs-lookup"><span data-stu-id="b520c-178">Click **Accounts** tab in hello menu list.</span></span>
   
    ![Configurar no lado do aplicativo](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="b520c-180">Clique em **Single Sign On** na lista de saudação de contas.</span><span class="sxs-lookup"><span data-stu-id="b520c-180">Click **Single Sign On** in hello list of Accounts.</span></span>
   
    ![Configurar no lado do aplicativo](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="b520c-182">Selecione **Logon Único** em Método de autenticação e clique em **SAML**.</span><span class="sxs-lookup"><span data-stu-id="b520c-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Configurar no lado do aplicativo](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="b520c-184">Cópia **URL SSO SAML**, **Sing Out URL de serviço único** e **URL do emissor** do AD do Azure muito**URL de entrada**, **sair da URL**  e **URL do emissor** no escritório Virtual 8x8.</span><span class="sxs-lookup"><span data-stu-id="b520c-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD too**Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Configurar no lado do aplicativo](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="b520c-186">Clique em **navegador** botão certificado de saudação tooupload que você baixou do AD do Azure e, em seguida, clique em Olá **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="b520c-186">Click **Browser** button tooupload hello certificate which you downloaded from Azure AD, and click hello **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="b520c-187">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="b520c-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b520c-188">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="b520c-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b520c-189">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b520c-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b520c-190">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b520c-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="b520c-191">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b520c-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="b520c-193">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b520c-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b520c-194">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b520c-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b520c-196">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="b520c-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b520c-198">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b520c-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b520c-200">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b520c-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b520c-202">a.</span><span class="sxs-lookup"><span data-stu-id="b520c-202">a.</span></span> <span data-ttu-id="b520c-203">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b520c-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b520c-204">b.</span><span class="sxs-lookup"><span data-stu-id="b520c-204">b.</span></span> <span data-ttu-id="b520c-205">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b520c-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b520c-206">c.</span><span class="sxs-lookup"><span data-stu-id="b520c-206">c.</span></span> <span data-ttu-id="b520c-207">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="b520c-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b520c-208">d.</span><span class="sxs-lookup"><span data-stu-id="b520c-208">d.</span></span> <span data-ttu-id="b520c-209">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b520c-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="b520c-210">Criar um usuário de teste no 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="b520c-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="b520c-211">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon 8x8 Virtual escritório.</span><span class="sxs-lookup"><span data-stu-id="b520c-211">hello objective of this section is toocreate a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="b520c-212">O 8x8 Virtual Office dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="b520c-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="b520c-213">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="b520c-213">There is no action item for you in this section.</span></span> <span data-ttu-id="b520c-214">Um novo usuário é criado durante uma tentativa tooaccess 8x8 Virtual Office se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="b520c-214">A new user is created during an attempt tooaccess 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="b520c-215">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [equipe de suporte do Office Virtual 8x8](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="b520c-215">If you need toocreate a user manually, you need toocontact hello [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b520c-216">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b520c-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b520c-217">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso too8x8 Virtual do Office.</span><span class="sxs-lookup"><span data-stu-id="b520c-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too8x8 Virtual Office.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="b520c-219">**tooassign Britta Simon too8x8 Virtual do Office, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b520c-219">**tooassign Britta Simon too8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="b520c-220">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b520c-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="b520c-222">Na lista de aplicativos hello, selecione **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="b520c-222">In hello applications list, select **8x8 Virtual Office**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="b520c-224">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b520c-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="b520c-226">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b520c-226">Click **Add** button.</span></span> <span data-ttu-id="b520c-227">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b520c-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="b520c-229">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="b520c-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b520c-230">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b520c-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b520c-231">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b520c-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b520c-232">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="b520c-232">Testing single sign-on</span></span>

<span data-ttu-id="b520c-233">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="b520c-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b520c-234">Quando você clica em bloco Virtual Office Olá 8x8 Olá painel de acesso, você deve obter um aplicativo do Office Virtual automaticamente assinado em tooyour 8x8.</span><span class="sxs-lookup"><span data-stu-id="b520c-234">When you click hello 8x8 Virtual Office tile in hello Access Panel, you should get automatically signed-on tooyour 8x8 Virtual Office application.</span></span>
<span data-ttu-id="b520c-235">Para obter mais informações sobre o painel de acesso, consulte [Introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="b520c-235">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b520c-236">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b520c-236">Additional resources</span></span>

* [<span data-ttu-id="b520c-237">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b520c-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b520c-238">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b520c-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

