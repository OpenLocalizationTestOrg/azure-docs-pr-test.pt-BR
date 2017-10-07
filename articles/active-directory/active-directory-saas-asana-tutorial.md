---
title: "Tutorial: Integração do Azure Active Directory ao Asana | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Asana."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="bb353-103">Tutorial: Integração do Azure Active Directory ao Asana</span><span class="sxs-lookup"><span data-stu-id="bb353-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="bb353-104">Neste tutorial, você aprenderá como toointegrate Asana com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="bb353-104">In this tutorial, you learn how toointegrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb353-105">Integrando Asana com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb353-105">Integrating Asana with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bb353-106">Você pode controlar no AD do Azure que tenha acesso tooAsana</span><span class="sxs-lookup"><span data-stu-id="bb353-106">You can control in Azure AD who has access tooAsana</span></span>
- <span data-ttu-id="bb353-107">Você pode habilitar seu usuários tooautomatically get conectado tooAsana (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bb353-107">You can enable your users tooautomatically get signed-on tooAsana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bb353-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bb353-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bb353-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bb353-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb353-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bb353-110">Prerequisites</span></span>

<span data-ttu-id="bb353-111">tooconfigure integração do AD do Azure com Asana, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb353-111">tooconfigure Azure AD integration with Asana, you need hello following items:</span></span>

- <span data-ttu-id="bb353-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bb353-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bb353-113">Uma assinatura habilitada para logon único do Asana</span><span class="sxs-lookup"><span data-stu-id="bb353-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bb353-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="bb353-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bb353-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="bb353-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bb353-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="bb353-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bb353-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb353-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb353-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="bb353-118">Scenario description</span></span>
<span data-ttu-id="bb353-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="bb353-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bb353-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="bb353-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb353-121">Adicionando Asana da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="bb353-121">Adding Asana from hello gallery</span></span>
2. <span data-ttu-id="bb353-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bb353-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-hello-gallery"></a><span data-ttu-id="bb353-123">Adicionando Asana da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="bb353-123">Adding Asana from hello gallery</span></span>
<span data-ttu-id="bb353-124">integração de saudação tooconfigure de Asana no AD do Azure, você precisa tooadd Asana da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="bb353-124">tooconfigure hello integration of Asana into Azure AD, you need tooadd Asana from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bb353-125">**tooadd Asana da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bb353-125">**tooadd Asana from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb353-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="bb353-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="bb353-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="bb353-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bb353-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bb353-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="bb353-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bb353-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="bb353-133">Na caixa de pesquisa hello, digite **Asana**, selecione **Asana** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bb353-133">In hello search box, type **Asana**, select **Asana** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bb353-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb353-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bb353-136">Nesta seção, você configura e testa o logon único do Azure AD com o Asana, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="bb353-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bb353-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Asana é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb353-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Asana is tooa user in Azure AD.</span></span> <span data-ttu-id="bb353-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Asana precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="bb353-138">In other words, a link relationship between an Azure AD user and hello related user in Asana needs toobe established.</span></span>

<span data-ttu-id="bb353-139">Asana, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb353-139">In Asana, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bb353-140">tooconfigure e teste de logon único do AD do Azure com Asana, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb353-140">tooconfigure and test Azure AD single sign-on with Asana, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bb353-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="bb353-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bb353-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bb353-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bb353-143">**[Criar um usuário de teste Asana](#create-an-asana-test-user)**  -toohave um equivalente do Britta Simon em Asana é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="bb353-143">**[Create an Asana test user](#create-an-asana-test-user)** - toohave a counterpart of Britta Simon in Asana that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bb353-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="bb353-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bb353-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="bb353-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bb353-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb353-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bb353-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Asana.</span><span class="sxs-lookup"><span data-stu-id="bb353-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="bb353-148">**tooconfigure AD do Azure-logon único com Asana, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bb353-148">**tooconfigure Azure AD single sign-on with Asana, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb353-149">Em Olá portal do Azure, Olá **Asana** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="bb353-149">In hello Azure portal, on hello **Asana** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="bb353-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="bb353-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="bb353-153">Em Olá **Asana domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb353-153">On hello **Asana Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="bb353-155">a.</span><span class="sxs-lookup"><span data-stu-id="bb353-155">a.</span></span> <span data-ttu-id="bb353-156">Em Olá **URL de logon** caixa de texto, digite a URL:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="bb353-156">In hello **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="bb353-157">b.</span><span class="sxs-lookup"><span data-stu-id="bb353-157">b.</span></span> <span data-ttu-id="bb353-158">Em Olá **identificador** caixa de texto, o valor de tipo:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="bb353-158">In hello **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="bb353-159">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="bb353-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="bb353-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="bb353-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bb353-163">Em Olá **Asana configuração** seção, clique em **configurar Asana** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="bb353-163">On hello **Asana Configuration** section, click **Configure Asana** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bb353-164">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="bb353-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="bb353-166">Em uma janela de navegador diferente, logon tooyour Asana aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bb353-166">In a different browser window, sign-on tooyour Asana application.</span></span> <span data-ttu-id="bb353-167">tooconfigure SSO no Asana, configurações de espaço de trabalho do access Olá clicando no nome do espaço de trabalho Olá no canto superior direito de saudação da tela hello.</span><span class="sxs-lookup"><span data-stu-id="bb353-167">tooconfigure SSO in Asana, access hello workspace settings by clicking hello workspace name on hello top right corner of hello screen.</span></span> <span data-ttu-id="bb353-168">Em seguida, clique em **\<nome do espaço de trabalho\>Configurações**.</span><span class="sxs-lookup"><span data-stu-id="bb353-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![configurações de sso do Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="bb353-170">Em Olá **as configurações da organização** janela, clique em **administração**.</span><span class="sxs-lookup"><span data-stu-id="bb353-170">On hello **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="bb353-171">Em seguida, clique em **membros devem efetuar logon por meio de SAML** tooenable configuração de SSO de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb353-171">Then, click **Members must log in via SAML** tooenable hello SSO configuration.</span></span> <span data-ttu-id="bb353-172">Olá execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb353-172">hello perform hello following steps:</span></span>
   
    ![Definições de Configurar Organização de Logon Único](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="bb353-174">a.</span><span class="sxs-lookup"><span data-stu-id="bb353-174">a.</span></span> <span data-ttu-id="bb353-175">Em Olá **URL da página de entrada** caixa de texto, colar Olá **Single Sign-On URL do serviço SAML**.</span><span class="sxs-lookup"><span data-stu-id="bb353-175">In hello **Sign-in page URL** textbox, paste hello **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="bb353-176">b.</span><span class="sxs-lookup"><span data-stu-id="bb353-176">b.</span></span> <span data-ttu-id="bb353-177">Clique com botão direito certificado Olá baixado do portal do Azure e abrir o arquivo de certificado hello usando o bloco de notas ou seu editor de texto preferido.</span><span class="sxs-lookup"><span data-stu-id="bb353-177">Right click hello certificate downloaded from Azure portal, then open hello certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="bb353-178">Saudação de copiar conteúdo entre hello começar e Olá final certificado título e colá-lo em hello **certificado x. 509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="bb353-178">Copy hello content between hello begin and hello end certificate title and paste it in hello **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="bb353-179">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bb353-179">Click **Save**.</span></span> <span data-ttu-id="bb353-180">Vá muito[Asana guia para configurar SSO](https://asana.com/guide/help/premium/authentication#gl-saml) se precisar de assistência adicional.</span><span class="sxs-lookup"><span data-stu-id="bb353-180">Go too[Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="bb353-181">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="bb353-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bb353-182">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="bb353-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bb353-183">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bb353-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bb353-184">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb353-184">Create an Azure AD test user</span></span>

<span data-ttu-id="bb353-185">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb353-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="bb353-187">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bb353-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb353-188">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="bb353-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bb353-190">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="bb353-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bb353-192">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb353-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bb353-194">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb353-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![botão Adicionar de saudação](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bb353-196">a.</span><span class="sxs-lookup"><span data-stu-id="bb353-196">a.</span></span> <span data-ttu-id="bb353-197">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bb353-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bb353-198">b.</span><span class="sxs-lookup"><span data-stu-id="bb353-198">b.</span></span> <span data-ttu-id="bb353-199">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bb353-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bb353-200">c.</span><span class="sxs-lookup"><span data-stu-id="bb353-200">c.</span></span> <span data-ttu-id="bb353-201">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="bb353-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bb353-202">d.</span><span class="sxs-lookup"><span data-stu-id="bb353-202">d.</span></span> <span data-ttu-id="bb353-203">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="bb353-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="bb353-204">Criar um usuário de teste do Asana</span><span class="sxs-lookup"><span data-stu-id="bb353-204">Create an Asana test user</span></span>

<span data-ttu-id="bb353-205">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Asana.</span><span class="sxs-lookup"><span data-stu-id="bb353-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="bb353-206">Em **Asana**, vá toohello **equipes** seção no painel esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="bb353-206">On **Asana**, go toohello **Teams** section on hello left panel.</span></span> <span data-ttu-id="bb353-207">Clique em hello mais entrar botão.</span><span class="sxs-lookup"><span data-stu-id="bb353-207">Click hello plus sign button.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="bb353-209">Digite o email Olá britta.simon@contoso.com Olá caixa de texto e, em seguida, selecione **convidar**.</span><span class="sxs-lookup"><span data-stu-id="bb353-209">Type hello email britta.simon@contoso.com in hello text box and then select **Invite**.</span></span>

3. <span data-ttu-id="bb353-210">Clique em **Enviar Convite**.</span><span class="sxs-lookup"><span data-stu-id="bb353-210">Click **Send Invite**.</span></span> <span data-ttu-id="bb353-211">novo usuário de saudação receberá um email em sua conta de email.</span><span class="sxs-lookup"><span data-stu-id="bb353-211">hello new user will receive an email into her email account.</span></span> <span data-ttu-id="bb353-212">Ela será necessário toocreate e validar a conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb353-212">She will need toocreate and validate hello account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="bb353-213">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bb353-213">Assign hello Azure AD test user</span></span>

<span data-ttu-id="bb353-214">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAsana.</span><span class="sxs-lookup"><span data-stu-id="bb353-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAsana.</span></span>

![Atribuir função de usuário Olá][200]

<span data-ttu-id="bb353-216">**tooassign Britta Simon tooAsana, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="bb353-216">**tooassign Britta Simon tooAsana, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb353-217">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bb353-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="bb353-219">Na lista de aplicativos hello, selecione **Asana**.</span><span class="sxs-lookup"><span data-stu-id="bb353-219">In hello applications list, select **Asana**.</span></span>

    ![link de Asana Olá na lista de aplicativos Olá](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="bb353-221">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="bb353-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="bb353-223">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bb353-223">Click **Add** button.</span></span> <span data-ttu-id="bb353-224">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bb353-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="bb353-226">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="bb353-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bb353-227">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bb353-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bb353-228">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bb353-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bb353-229">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="bb353-229">Test single sign-on</span></span>

<span data-ttu-id="bb353-230">objetivo Olá desta seção é tootest seu AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="bb353-230">hello objective of this section is tootest your Azure AD single sign-on.</span></span>

<span data-ttu-id="bb353-231">Acesse a página de logon tooAsana.</span><span class="sxs-lookup"><span data-stu-id="bb353-231">Go tooAsana login page.</span></span> <span data-ttu-id="bb353-232">No texto de endereço de Email hello, inserir o endereço de email Olá britta.simon@contoso.com. Deixe Olá caixa de texto de senha em branco e, em seguida, clique em **logon**.</span><span class="sxs-lookup"><span data-stu-id="bb353-232">In hello Email address textbox, insert hello email address britta.simon@contoso.com. Leave hello password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="bb353-233">Você será redirecionado tooAzure AD página de logon.</span><span class="sxs-lookup"><span data-stu-id="bb353-233">You will be redirected tooAzure AD login page.</span></span> <span data-ttu-id="bb353-234">Preencha suas credenciais do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb353-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="bb353-235">Agora, você está conectado ao Asana.</span><span class="sxs-lookup"><span data-stu-id="bb353-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb353-236">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="bb353-236">Additional resources</span></span>

* [<span data-ttu-id="bb353-237">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="bb353-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb353-238">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bb353-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
