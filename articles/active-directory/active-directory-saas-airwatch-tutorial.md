---
title: "Tutorial: integração do Azure Active Directory com o AirWatch | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e AirWatch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="8d513-103">Tutorial: Integração do Active Directory do Azure ao AirWatch</span><span class="sxs-lookup"><span data-stu-id="8d513-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="8d513-104">Neste tutorial, você aprenderá como toointegrate AirWatch com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="8d513-104">In this tutorial, you learn how toointegrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d513-105">Integrando o AirWatch com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d513-105">Integrating AirWatch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8d513-106">Você pode controlar no AD do Azure que tenha acesso tooAirWatch</span><span class="sxs-lookup"><span data-stu-id="8d513-106">You can control in Azure AD who has access tooAirWatch</span></span>
- <span data-ttu-id="8d513-107">Você pode habilitar seu usuários tooautomatically get conectado tooAirWatch (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8d513-107">You can enable your users tooautomatically get signed-on tooAirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d513-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8d513-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8d513-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d513-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d513-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8d513-110">Prerequisites</span></span>

<span data-ttu-id="8d513-111">tooconfigure integração do AD do Azure com o AirWatch, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d513-111">tooconfigure Azure AD integration with AirWatch, you need hello following items:</span></span>

- <span data-ttu-id="8d513-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8d513-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d513-113">Uma assinatura habilitada para logon único do AirWatch</span><span class="sxs-lookup"><span data-stu-id="8d513-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d513-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8d513-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d513-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8d513-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d513-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8d513-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d513-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d513-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d513-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8d513-118">Scenario description</span></span>
<span data-ttu-id="8d513-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8d513-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d513-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="8d513-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d513-121">Adicionando AirWatch da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8d513-121">Adding AirWatch from hello gallery</span></span>
2. <span data-ttu-id="8d513-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8d513-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-hello-gallery"></a><span data-ttu-id="8d513-123">Adicionando AirWatch da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8d513-123">Adding AirWatch from hello gallery</span></span>
<span data-ttu-id="8d513-124">integração de saudação tooconfigure do AirWatch no AD do Azure, você precisa tooadd AirWatch da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8d513-124">tooconfigure hello integration of AirWatch into Azure AD, you need tooadd AirWatch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8d513-125">**tooadd AirWatch da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8d513-125">**tooadd AirWatch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d513-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8d513-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d513-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8d513-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8d513-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8d513-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8d513-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8d513-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8d513-133">Na caixa de pesquisa hello, digite **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="8d513-133">In hello search box, type **AirWatch**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="8d513-135">No painel de resultados de saudação, selecione **AirWatch**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8d513-135">In hello results panel, select **AirWatch**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d513-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8d513-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d513-138">Nesta seção, você configurará e testará o logon único do Azure AD com o AirWatch, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="8d513-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8d513-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no AirWatch é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d513-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AirWatch is tooa user in Azure AD.</span></span> <span data-ttu-id="8d513-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no AirWatch precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="8d513-140">In other words, a link relationship between an Azure AD user and hello related user in AirWatch needs toobe established.</span></span>

<span data-ttu-id="8d513-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no AirWatch.</span><span class="sxs-lookup"><span data-stu-id="8d513-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in AirWatch.</span></span>

<span data-ttu-id="8d513-142">tooconfigure e teste de logon único do AD do Azure com o AirWatch, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d513-142">tooconfigure and test Azure AD single sign-on with AirWatch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8d513-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8d513-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8d513-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d513-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d513-145">**[Criar um usuário de teste do AirWatch](#creating-a-airwatch-test-user)**  -toohave um equivalente do Britta Simon no AirWatch é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="8d513-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - toohave a counterpart of Britta Simon in AirWatch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d513-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="8d513-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d513-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="8d513-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d513-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d513-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d513-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo AirWatch.</span><span class="sxs-lookup"><span data-stu-id="8d513-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="8d513-150">**tooconfigure AD do Azure-logon único com o AirWatch, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8d513-150">**tooconfigure Azure AD single sign-on with AirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d513-151">Em Olá portal do Azure, Olá **AirWatch** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="8d513-151">In hello Azure portal, on hello **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8d513-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="8d513-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="8d513-155">Em Olá **AirWatch domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d513-155">On hello **AirWatch Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="8d513-157">a.</span><span class="sxs-lookup"><span data-stu-id="8d513-157">a.</span></span> <span data-ttu-id="8d513-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="8d513-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="8d513-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d513-159">b.</span></span> <span data-ttu-id="8d513-160">Em Olá **identificador** texto, o valor do tipo hello como`AirWatch`</span><span class="sxs-lookup"><span data-stu-id="8d513-160">In hello **Identifier** textbox, type hello value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d513-161">Esse valor não é hello real.</span><span class="sxs-lookup"><span data-stu-id="8d513-161">This value is not hello real.</span></span> <span data-ttu-id="8d513-162">Atualize esse valor com a URL de logon real hello.</span><span class="sxs-lookup"><span data-stu-id="8d513-162">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="8d513-163">Entre em contato com [equipe de suporte do cliente do AirWatch](http://www.air-watch.com/company/contact-us/) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="8d513-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) tooget this value.</span></span> 
 
4. <span data-ttu-id="8d513-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8d513-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="8d513-166">Em Olá **AirWatch configuração** seção, clique em **configurar AirWatch** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="8d513-166">On hello **AirWatch Configuration** section, click **Configure AirWatch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8d513-167">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="8d513-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="8d513-169">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8d513-169">Click **Save** button.</span></span>

    <span data-ttu-id="8d513-170">![Configurar Logon Único](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="8d513-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="8d513-171">Em uma janela de navegador web diferente, faça logon no site da empresa tooyour AirWatch como um administrador.</span><span class="sxs-lookup"><span data-stu-id="8d513-171">In a different web browser window, log in tooyour AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="8d513-172">No painel de navegação esquerdo hello, clique em **contas**e, em seguida, clique em **administradores**.</span><span class="sxs-lookup"><span data-stu-id="8d513-172">In hello left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="8d513-173">![Administradores](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administradores")</span><span class="sxs-lookup"><span data-stu-id="8d513-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="8d513-174">Expanda Olá **configurações** menu e clique **serviços de diretório**.</span><span class="sxs-lookup"><span data-stu-id="8d513-174">Expand hello **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="8d513-175">![Configurações](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="8d513-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="8d513-176">Clique em Olá **usuário** guia Olá **DN Base** caixa de texto, digite seu nome de domínio e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="8d513-176">Click hello **User** tab, in hello **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="8d513-177">![Usuário](./media/active-directory-saas-airwatch-tutorial/ic791922.png "Usuário")</span><span class="sxs-lookup"><span data-stu-id="8d513-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="8d513-178">Clique em Olá **Server** guia.</span><span class="sxs-lookup"><span data-stu-id="8d513-178">Click hello **Server** tab.</span></span>
   
   <span data-ttu-id="8d513-179">![Servidor](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Servidor")</span><span class="sxs-lookup"><span data-stu-id="8d513-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="8d513-180">Execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d513-180">Perform hello following steps:</span></span>
    
    <span data-ttu-id="8d513-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span><span class="sxs-lookup"><span data-stu-id="8d513-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="8d513-182">a.</span><span class="sxs-lookup"><span data-stu-id="8d513-182">a.</span></span> <span data-ttu-id="8d513-183">Para **Tipo de Diretório**, selecione **Nenhum**.</span><span class="sxs-lookup"><span data-stu-id="8d513-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="8d513-184">b.</span><span class="sxs-lookup"><span data-stu-id="8d513-184">b.</span></span> <span data-ttu-id="8d513-185">Selecione **Usar SAML para Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="8d513-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="8d513-186">c.</span><span class="sxs-lookup"><span data-stu-id="8d513-186">c.</span></span> <span data-ttu-id="8d513-187">tooupload Olá certificado baixado, clique em **carregar**.</span><span class="sxs-lookup"><span data-stu-id="8d513-187">tooupload hello downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="8d513-188">Em Olá **solicitação** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d513-188">In hello **Request** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="8d513-189">![Solicitação](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Solicitação")</span><span class="sxs-lookup"><span data-stu-id="8d513-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="8d513-190">a.</span><span class="sxs-lookup"><span data-stu-id="8d513-190">a.</span></span> <span data-ttu-id="8d513-191">Para **Tipo de Associação de Solicitação**, selecione **POST**.</span><span class="sxs-lookup"><span data-stu-id="8d513-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="8d513-192">b.</span><span class="sxs-lookup"><span data-stu-id="8d513-192">b.</span></span> <span data-ttu-id="8d513-193">Em Olá portal do Azure, Olá **configurar logon único no Airwatch** página de diálogo, Olá cópia **Single Sign-On URL do serviço SAML** valor e, em seguida, cole-o em Olá **provedor de identidade Única URL de logon** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="8d513-193">In hello Azure portal, on hello **Configure single sign-on at Airwatch** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="8d513-194">c.</span><span class="sxs-lookup"><span data-stu-id="8d513-194">c.</span></span> <span data-ttu-id="8d513-195">Para **Formato de NameID**, selecione **Endereço de Email**.</span><span class="sxs-lookup"><span data-stu-id="8d513-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="8d513-196">d.</span><span class="sxs-lookup"><span data-stu-id="8d513-196">d.</span></span> <span data-ttu-id="8d513-197">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8d513-197">Click **Save**.</span></span>

14. <span data-ttu-id="8d513-198">Clique em Olá **usuário** guia novamente.</span><span class="sxs-lookup"><span data-stu-id="8d513-198">Click hello **User** tab again.</span></span>
    
    <span data-ttu-id="8d513-199">![Usuário](./media/active-directory-saas-airwatch-tutorial/ic791926.png "Usuário")</span><span class="sxs-lookup"><span data-stu-id="8d513-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="8d513-200">Em Olá **atributo** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d513-200">In hello **Attribute** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="8d513-201">![Atributo](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Atributo")</span><span class="sxs-lookup"><span data-stu-id="8d513-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="8d513-202">a.</span><span class="sxs-lookup"><span data-stu-id="8d513-202">a.</span></span> <span data-ttu-id="8d513-203">Em Olá **identificador de objeto** caixa de texto, tipo **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="8d513-203">In hello **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="8d513-204">b.</span><span class="sxs-lookup"><span data-stu-id="8d513-204">b.</span></span> <span data-ttu-id="8d513-205">Em Olá **Username** caixa de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="8d513-205">In hello **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="8d513-206">c.</span><span class="sxs-lookup"><span data-stu-id="8d513-206">c.</span></span> <span data-ttu-id="8d513-207">Em Olá **nome de exibição** caixa de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="8d513-207">In hello **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="8d513-208">d.</span><span class="sxs-lookup"><span data-stu-id="8d513-208">d.</span></span> <span data-ttu-id="8d513-209">Em Olá **nome** caixa de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="8d513-209">In hello **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="8d513-210">e.</span><span class="sxs-lookup"><span data-stu-id="8d513-210">e.</span></span> <span data-ttu-id="8d513-211">Em Olá **Sobrenome** caixa de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="8d513-211">In hello **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="8d513-212">f.</span><span class="sxs-lookup"><span data-stu-id="8d513-212">f.</span></span> <span data-ttu-id="8d513-213">Em Olá **Email** caixa de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="8d513-213">In hello **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="8d513-214">g.</span><span class="sxs-lookup"><span data-stu-id="8d513-214">g.</span></span> <span data-ttu-id="8d513-215">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8d513-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d513-216">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8d513-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d513-217">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d513-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8d513-219">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8d513-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d513-220">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8d513-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d513-222">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="8d513-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d513-224">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d513-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d513-226">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d513-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d513-228">a.</span><span class="sxs-lookup"><span data-stu-id="8d513-228">a.</span></span> <span data-ttu-id="8d513-229">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d513-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d513-230">b.</span><span class="sxs-lookup"><span data-stu-id="8d513-230">b.</span></span> <span data-ttu-id="8d513-231">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d513-231">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="8d513-232">c.</span><span class="sxs-lookup"><span data-stu-id="8d513-232">c.</span></span> <span data-ttu-id="8d513-233">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="8d513-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8d513-234">d.</span><span class="sxs-lookup"><span data-stu-id="8d513-234">d.</span></span> <span data-ttu-id="8d513-235">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8d513-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="8d513-236">Criando um usuário de teste do AirWatch</span><span class="sxs-lookup"><span data-stu-id="8d513-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="8d513-237">tooenable AD do Azure usuários toolog em tooAirWatch, eles devem ser provisionados no tooAirWatch.</span><span class="sxs-lookup"><span data-stu-id="8d513-237">tooenable Azure AD users toolog in tooAirWatch, they must be provisioned in tooAirWatch.</span></span>

* <span data-ttu-id="8d513-238">No caso do AirWatch, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="8d513-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="8d513-239">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8d513-239">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d513-240">Faça logon no tooyour **AirWatch** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="8d513-240">Log in tooyour **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="8d513-241">No painel de navegação Olá no lado esquerdo do hello, clique em **contas**e, em seguida, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="8d513-241">In hello navigation pane on hello left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="8d513-242">![Usuários](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="8d513-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="8d513-243">Em Olá **usuários** menu, clique em **exibição de lista**e, em seguida, clique em **adicionar \> adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="8d513-243">In hello **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="8d513-244">![Adicionar Usuário](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="8d513-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="8d513-245">Em Olá **Adicionar / Editar usuário** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d513-245">On hello **Add / Edit User** dialog, perform hello following steps:</span></span>

   <span data-ttu-id="8d513-246">![Adicionar Usuário](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="8d513-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="8d513-247">Saudação de tipo **Username**, **senha**, **Confirmar senha**, **nome**, **Sobrenome**,  **Endereço de email** de uma válida do Azure relacionadas à conta do Active Directory você deseja tooprovision em Olá caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="8d513-247">Type hello **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="8d513-248">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8d513-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="8d513-249">Você pode usar qualquer ferramenta de criação outros AirWatch usuário conta ou APIs fornecidas pelo AirWatch tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="8d513-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8d513-250">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8d513-250">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8d513-251">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAirWatch.</span><span class="sxs-lookup"><span data-stu-id="8d513-251">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAirWatch.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8d513-253">**tooassign Britta Simon tooAirWatch, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8d513-253">**tooassign Britta Simon tooAirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d513-254">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8d513-254">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8d513-256">Na lista de aplicativos hello, selecione **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="8d513-256">In hello applications list, select **AirWatch**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="8d513-258">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8d513-258">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8d513-260">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8d513-260">Click **Add** button.</span></span> <span data-ttu-id="8d513-261">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8d513-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8d513-263">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d513-263">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8d513-264">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8d513-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d513-265">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8d513-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d513-266">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8d513-266">Testing single sign-on</span></span>

<span data-ttu-id="8d513-267">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d513-267">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8d513-268">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="8d513-268">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="8d513-269">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8d513-269">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8d513-270">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8d513-270">Additional resources</span></span>

* [<span data-ttu-id="8d513-271">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8d513-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d513-272">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d513-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

