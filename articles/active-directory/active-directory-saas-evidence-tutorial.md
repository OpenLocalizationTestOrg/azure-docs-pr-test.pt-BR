---
title: "Tutorial: integração do Azure Active Directory ao Evidence.com | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Evidence.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: eed98c15dca8a6a77f0b5d407bb40ee0037fccad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="4fa9a-103">Tutorial: Integração do Active Directory do Azure ao Evidence.com</span><span class="sxs-lookup"><span data-stu-id="4fa9a-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="4fa9a-104">Neste tutorial, você aprenderá como toointegrate Evidence.com com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="4fa9a-104">In this tutorial, you learn how toointegrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4fa9a-105">Integrando Evidence.com com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fa9a-105">Integrating Evidence.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4fa9a-106">Você pode controlar no AD do Azure que tenha acesso tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-106">You can control in Azure AD who has access tooEvidence.com.</span></span>
- <span data-ttu-id="4fa9a-107">Você pode habilitar seus usuários tooautomatically get conectado tooEvidence.com (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-107">You can enable your users tooautomatically get signed-on tooEvidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4fa9a-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="4fa9a-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4fa9a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fa9a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4fa9a-110">Prerequisites</span></span>

<span data-ttu-id="4fa9a-111">tooconfigure integração do AD do Azure com Evidence.com, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fa9a-111">tooconfigure Azure AD integration with Evidence.com, you need hello following items:</span></span>

- <span data-ttu-id="4fa9a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa9a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4fa9a-113">Uma assinatura do Evidence.com habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="4fa9a-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4fa9a-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4fa9a-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4fa9a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4fa9a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4fa9a-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4fa9a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4fa9a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4fa9a-118">Scenario description</span></span>
<span data-ttu-id="4fa9a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4fa9a-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="4fa9a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4fa9a-121">Adicionando Evidence.com da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4fa9a-121">Adding Evidence.com from hello gallery</span></span>
2. <span data-ttu-id="4fa9a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa9a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-hello-gallery"></a><span data-ttu-id="4fa9a-123">Adicionando Evidence.com da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4fa9a-123">Adding Evidence.com from hello gallery</span></span>
<span data-ttu-id="4fa9a-124">integração de saudação tooconfigure de Evidence.com no AD do Azure, você precisa tooadd Evidence.com da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-124">tooconfigure hello integration of Evidence.com into Azure AD, you need tooadd Evidence.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4fa9a-125">**tooadd Evidence.com da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4fa9a-125">**tooadd Evidence.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fa9a-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="4fa9a-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4fa9a-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="4fa9a-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="4fa9a-133">Na caixa de pesquisa hello, digite **Evidence.com**, selecione **Evidence.com** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-133">In hello search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evidence.com na lista de resultados de saudação](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4fa9a-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fa9a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4fa9a-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Evidence.com, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4fa9a-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Evidence.com é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evidence.com is tooa user in Azure AD.</span></span> <span data-ttu-id="4fa9a-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Evidence.com precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-138">In other words, a link relationship between an Azure AD user and hello related user in Evidence.com needs toobe established.</span></span>

<span data-ttu-id="4fa9a-139">Evidence.com, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-139">In Evidence.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4fa9a-140">tooconfigure e teste de logon único do AD do Azure com Evidence.com, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fa9a-140">tooconfigure and test Azure AD single sign-on with Evidence.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4fa9a-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4fa9a-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4fa9a-143">**[Criar um usuário de teste Evidence.com](#create-a-evidencecom-test-user)**  -toohave um equivalente do Britta Simon em Evidence.com é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - toohave a counterpart of Britta Simon in Evidence.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4fa9a-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4fa9a-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4fa9a-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fa9a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4fa9a-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="4fa9a-148">**tooconfigure AD do Azure-logon único com Evidence.com, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4fa9a-148">**tooconfigure Azure AD single sign-on with Evidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fa9a-149">Em Olá portal do Azure, Olá **Evidence.com** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-149">In hello Azure portal, on hello **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="4fa9a-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="4fa9a-153">Em Olá **Evidence.com domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fa9a-153">On hello **Evidence.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="4fa9a-155">a.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-155">a.</span></span> <span data-ttu-id="4fa9a-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="4fa9a-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="4fa9a-157">b.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-157">b.</span></span> <span data-ttu-id="4fa9a-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="4fa9a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4fa9a-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-159">These values are not real.</span></span> <span data-ttu-id="4fa9a-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4fa9a-161">Entre em contato com [equipe de suporte do cliente Evidence.com](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget these values.</span></span> 

4. <span data-ttu-id="4fa9a-162">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="4fa9a-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4fa9a-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4fa9a-166">Em Olá **Evidence.com configuração** seção, clique em **configurar Evidence.com** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-166">On hello **Evidence.com Configuration** section, click **Configure Evidence.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4fa9a-167">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="4fa9a-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="4fa9a-169">Em uma janela de navegador da web separado, o logon tooyour Evidence.com locatário como um administrador e navegue muito**Admin** guia</span><span class="sxs-lookup"><span data-stu-id="4fa9a-169">In a separate web browser window, login tooyour Evidence.com tenant as an administrator and navigate too**Admin** Tab</span></span>

8. <span data-ttu-id="4fa9a-170">Clique em **Logon Único de Agência**</span><span class="sxs-lookup"><span data-stu-id="4fa9a-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="4fa9a-171">Escolha **Logon Único Baseado em SAML**</span><span class="sxs-lookup"><span data-stu-id="4fa9a-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="4fa9a-172">Saudação de cópia **ID da entidade SAML**, **Single Sign-On URL do serviço SAML** e **URL de logout** valores mostrados na hello portal do Azure e campos correspondentes de toohello no Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-172">Copy hello **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in hello Azure portal and toohello corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="4fa9a-173">Abra o arquivo Certificate(Base64) baixado no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado de segurança** caixa.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-173">Open your downloaded Certificate(Base64) file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Security Certificate** box.</span></span> 

12. <span data-ttu-id="4fa9a-174">Salve a configuração de saudação em Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-174">Save hello configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="4fa9a-175">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="4fa9a-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4fa9a-176">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4fa9a-177">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4fa9a-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4fa9a-178">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fa9a-178">Create an Azure AD test user</span></span>

<span data-ttu-id="4fa9a-179">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="4fa9a-181">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4fa9a-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fa9a-182">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-182">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4fa9a-184">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-184">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4fa9a-186">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-186">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4fa9a-188">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fa9a-188">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4fa9a-190">a.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-190">a.</span></span> <span data-ttu-id="4fa9a-191">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-191">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4fa9a-192">b.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-192">b.</span></span> <span data-ttu-id="4fa9a-193">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-193">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="4fa9a-194">c.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-194">c.</span></span> <span data-ttu-id="4fa9a-195">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-195">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="4fa9a-196">d.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-196">d.</span></span> <span data-ttu-id="4fa9a-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="4fa9a-198">Criar um usuário de teste de Evidence.com</span><span class="sxs-lookup"><span data-stu-id="4fa9a-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="4fa9a-199">Para o AD do Azure usuários toobe capaz de toosign no, eles devem ser provisionados acesso Olá Evidence.com aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-199">For Azure AD users toobe able toosign in, they must be provisioned for access inside hello Evidence.com application.</span></span> <span data-ttu-id="4fa9a-200">Esta seção descreve como contas de usuário de toocreate AD do Azure dentro de Evidence.com</span><span class="sxs-lookup"><span data-stu-id="4fa9a-200">This section describes how toocreate Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="4fa9a-201">**tooprovision uma conta de usuário no Evidence.com:**</span><span class="sxs-lookup"><span data-stu-id="4fa9a-201">**tooprovision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="4fa9a-202">Em uma janela do navegador da Web, faça logon no site de sua empresa do Evidence.com como administrador.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="4fa9a-203">Navegue muito**Admin** guia.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-203">Navigate too**Admin** tab.</span></span>

3. <span data-ttu-id="4fa9a-204">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="4fa9a-205">Clique em Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-205">Click hello **Add** button.</span></span>

5. <span data-ttu-id="4fa9a-206">Olá **endereço de Email** Olá adicionados usuário deve corresponder a saudação de nome de usuário de usuários Olá no AD do Azure que você deseja toogive acesso.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-206">hello **Email Address** of hello added user must match hello username of hello users in Azure AD who you wish toogive access.</span></span> <span data-ttu-id="4fa9a-207">Se Olá nome de usuário e endereço de email não são hello mesmo valor em sua organização, você pode usar o hello **Evidence.com > atributos > Single Sign-On** seção Olá toochange portal do Azure Olá nameidenitifer enviado endereço de email do tooEvidence.com toobe hello.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-207">If hello username and email address are not hello same value in your organization, you can use hello **Evidence.com > Attributes > Single Sign-On** section of hello Azure portal toochange hello nameidenitifer sent tooEvidence.com toobe hello email address.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4fa9a-208">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa9a-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4fa9a-209">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvidence.com.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="4fa9a-211">**tooassign Britta Simon tooEvidence.com, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4fa9a-211">**tooassign Britta Simon tooEvidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fa9a-212">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4fa9a-214">Na lista de aplicativos hello, selecione **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-214">In hello applications list, select **Evidence.com**.</span></span>

    ![link de Evidence.com Olá na lista de aplicativos Olá](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="4fa9a-216">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="4fa9a-218">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-218">Click **Add** button.</span></span> <span data-ttu-id="4fa9a-219">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="4fa9a-221">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4fa9a-222">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4fa9a-223">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4fa9a-224">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="4fa9a-224">Test single sign-on</span></span>

<span data-ttu-id="4fa9a-225">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4fa9a-226">Quando você clica em bloco Evidence.com Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Evidence.com aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-226">When you click hello Evidence.com tile in hello Access Panel, you should get automatically signed-on tooyour Evidence.com application.</span></span>
<span data-ttu-id="4fa9a-227">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4fa9a-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4fa9a-228">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4fa9a-228">Additional resources</span></span>

* [<span data-ttu-id="4fa9a-229">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa9a-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4fa9a-230">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4fa9a-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

