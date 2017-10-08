---
title: "Tutorial: Integração do Azure Active Directory com o Printix | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Printix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 654810116091eb52912b377cc97afef803ee816e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="f1e7f-103">Tutorial: integração do Azure Active Directory com o Printix</span><span class="sxs-lookup"><span data-stu-id="f1e7f-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="f1e7f-104">Neste tutorial, você aprenderá como toointegrate Printix com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f1e7f-104">In this tutorial, you learn how toointegrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1e7f-105">Integrando Printix com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1e7f-105">Integrating Printix with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f1e7f-106">Você pode controlar no AD do Azure que tenha acesso tooPrintix</span><span class="sxs-lookup"><span data-stu-id="f1e7f-106">You can control in Azure AD who has access tooPrintix</span></span>
- <span data-ttu-id="f1e7f-107">Você pode habilitar seu usuários tooautomatically get conectado tooPrintix (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1e7f-107">You can enable your users tooautomatically get signed-on tooPrintix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1e7f-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f1e7f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f1e7f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1e7f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1e7f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f1e7f-110">Prerequisites</span></span>

<span data-ttu-id="f1e7f-111">tooconfigure integração do AD do Azure com Printix, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1e7f-111">tooconfigure Azure AD integration with Printix, you need hello following items:</span></span>

- <span data-ttu-id="f1e7f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1e7f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1e7f-113">Uma assinatura habilitada para logon único do Printix</span><span class="sxs-lookup"><span data-stu-id="f1e7f-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1e7f-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1e7f-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f1e7f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1e7f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1e7f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1e7f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1e7f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f1e7f-118">Scenario description</span></span>
<span data-ttu-id="f1e7f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1e7f-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="f1e7f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1e7f-121">Adicionando Printix da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f1e7f-121">Adding Printix from hello gallery</span></span>
2. <span data-ttu-id="f1e7f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1e7f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-hello-gallery"></a><span data-ttu-id="f1e7f-123">Adicionando Printix da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f1e7f-123">Adding Printix from hello gallery</span></span>
<span data-ttu-id="f1e7f-124">integração de saudação tooconfigure de Printix no AD do Azure, você precisa tooadd Printix da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-124">tooconfigure hello integration of Printix into Azure AD, you need tooadd Printix from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f1e7f-125">**tooadd Printix da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f1e7f-125">**tooadd Printix from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1e7f-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1e7f-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f1e7f-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f1e7f-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f1e7f-133">Na caixa de pesquisa hello, digite **Printix**.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-133">In hello search box, type **Printix**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="f1e7f-135">No painel de resultados de saudação, selecione **Printix**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-135">In hello results panel, select **Printix**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1e7f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1e7f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1e7f-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Printix, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f1e7f-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Printix é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Printix is tooa user in Azure AD.</span></span> <span data-ttu-id="f1e7f-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Printix precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-140">In other words, a link relationship between an Azure AD user and hello related user in Printix needs toobe established.</span></span>

<span data-ttu-id="f1e7f-141">Printix, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-141">In Printix, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f1e7f-142">tooconfigure e teste de logon único do AD do Azure com Printix, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1e7f-142">tooconfigure and test Azure AD single sign-on with Printix, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f1e7f-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f1e7f-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1e7f-145">**[Criar um usuário de teste Printix](#creating-a-printix-test-user)**  -toohave um equivalente do Britta Simon em Printix é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - toohave a counterpart of Britta Simon in Printix that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1e7f-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1e7f-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1e7f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1e7f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1e7f-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Printix.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="f1e7f-150">**tooconfigure AD do Azure-logon único com Printix, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f1e7f-150">**tooconfigure Azure AD single sign-on with Printix, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1e7f-151">Em Olá portal do Azure, Olá **Printix** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-151">In hello Azure portal, on hello **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f1e7f-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="f1e7f-155">Em Olá **Printix domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1e7f-155">On hello **Printix Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="f1e7f-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="f1e7f-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1e7f-158">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-158">hello value is not real.</span></span> <span data-ttu-id="f1e7f-159">Valor de saudação de atualização com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f1e7f-160">Entre em contato com [equipe de suporte do cliente Printix](mailto:support@printix.net) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-160">Contact [Printix Client support team](mailto:support@printix.net) tooget hello value.</span></span> 
 
4. <span data-ttu-id="f1e7f-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="f1e7f-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f1e7f-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f1e7f-165">Locatário de Printix tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-165">Sign-on tooyour Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="f1e7f-166">No menu de saudação na parte superior do hello, clique Olá ícone no canto superior direito da saudação e selecione "**autenticação**".</span><span class="sxs-lookup"><span data-stu-id="f1e7f-166">In hello menu on hello top, click hello icon at hello upper right corner and select "**Authentication**".</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="f1e7f-168">Em Olá **instalação** guia, selecione **autenticação habilitar Azure/Office 365**</span><span class="sxs-lookup"><span data-stu-id="f1e7f-168">On hello **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="f1e7f-170">Em Olá **Azure** guia texto de toohello de URL de metadados de federação de entrada de "**documento de metadados de Federação**".</span><span class="sxs-lookup"><span data-stu-id="f1e7f-170">On hello **Azure** tab, input federation metadata URL toohello textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="f1e7f-171">Anexar o arquivo xml de metadados Olá que você baixou do AD do Azure muito[a equipe de suporte Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="f1e7f-171">Attach hello metadata xml file which you downloaded from Azure AD too[Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="f1e7f-172">Em seguida, eles carregar o arquivo xml de saudação e fornecem uma URL de metadados de Federação.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-172">Then they upload hello xml file and provide a federation metadata URL.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="f1e7f-174">Clique em hello "**teste**"botão e clique em"**Okey**" botão se Olá teste foi bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-174">Click hello "**Test**" button and click "**OK**" button if hello test was successful.</span></span>
   
     <span data-ttu-id="f1e7f-175">Página do active directory do Azure será exibido depois de clicar em Olá **teste** botão.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-175">Azure active directory page will show after clicking hello **test** button.</span></span> <span data-ttu-id="f1e7f-176">"teste de saudação foi bem-sucedida" aqui significa depois de inserir as credenciais de saudação da sua conta de teste do Azure, que será exibida uma mensagem de "configurações testadas Okey". Em seguida, clique em Olá **Okey** botão.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-176">"hello test was successful" here means after entering hello credentials of your Azure test account it will pop up a message "Settings tested OK".Then click hello **OK** button.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="f1e7f-178">Clique em Olá **salvar** no botão "**autenticação**" página.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-178">Click hello **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="f1e7f-179">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="f1e7f-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f1e7f-180">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f1e7f-181">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1e7f-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1e7f-182">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1e7f-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1e7f-183">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f1e7f-185">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f1e7f-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1e7f-186">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1e7f-188">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1e7f-190">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1e7f-192">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1e7f-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1e7f-194">a.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-194">a.</span></span> <span data-ttu-id="f1e7f-195">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1e7f-196">b.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-196">b.</span></span> <span data-ttu-id="f1e7f-197">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1e7f-198">c.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-198">c.</span></span> <span data-ttu-id="f1e7f-199">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f1e7f-200">d.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-200">d.</span></span> <span data-ttu-id="f1e7f-201">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="f1e7f-202">Criação de um usuário de teste do Printix</span><span class="sxs-lookup"><span data-stu-id="f1e7f-202">Creating a Printix test user</span></span>

<span data-ttu-id="f1e7f-203">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Printix.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-203">hello objective of this section is toocreate a user called Britta Simon in Printix.</span></span> <span data-ttu-id="f1e7f-204">O Printix dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="f1e7f-205">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-205">There is no action item for you in this section.</span></span> <span data-ttu-id="f1e7f-206">Um novo usuário é criado durante uma tentativa tooaccess Printix se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-206">A new user is created during an attempt tooaccess Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="f1e7f-207">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [a equipe de suporte Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="f1e7f-207">If you need toocreate a user manually, you need toocontact hello [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f1e7f-208">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1e7f-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f1e7f-209">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPrintix.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPrintix.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f1e7f-211">**tooassign Britta Simon tooPrintix, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f1e7f-211">**tooassign Britta Simon tooPrintix, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1e7f-212">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f1e7f-214">Na lista de aplicativos hello, selecione **Printix**.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-214">In hello applications list, select **Printix**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="f1e7f-216">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f1e7f-218">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-218">Click **Add** button.</span></span> <span data-ttu-id="f1e7f-219">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f1e7f-221">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f1e7f-222">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1e7f-223">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1e7f-224">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f1e7f-224">Testing single sign-on</span></span>

<span data-ttu-id="f1e7f-225">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f1e7f-226">Quando você clica em bloco Printix Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Printix aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1e7f-226">When you click hello Printix tile in hello Access Panel, you should get automatically signed-on tooyour Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1e7f-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f1e7f-227">Additional resources</span></span>

* [<span data-ttu-id="f1e7f-228">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f1e7f-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1e7f-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1e7f-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

