---
title: "Tutorial: integração do Azure Active Directory ao Front | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e frontal."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="7440d-103">Tutorial: integração do Azure Active Directory ao Front</span><span class="sxs-lookup"><span data-stu-id="7440d-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="7440d-104">Neste tutorial, você aprenderá como toointegrate frente com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="7440d-104">In this tutorial, you learn how toointegrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7440d-105">Integrando frente com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="7440d-105">Integrating Front with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7440d-106">Você pode controlar no AD do Azure que tenha acesso tooFront.</span><span class="sxs-lookup"><span data-stu-id="7440d-106">You can control in Azure AD who has access tooFront.</span></span>
- <span data-ttu-id="7440d-107">Você pode habilitar seu usuários tooautomatically get conectado tooFront (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7440d-107">You can enable your users tooautomatically get signed-on tooFront (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7440d-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7440d-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="7440d-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7440d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7440d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7440d-110">Prerequisites</span></span>

<span data-ttu-id="7440d-111">integração de tooconfigure AD do Azure com início, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="7440d-111">tooconfigure Azure AD integration with Front, you need hello following items:</span></span>

- <span data-ttu-id="7440d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7440d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7440d-113">Uma assinatura de Front habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="7440d-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7440d-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7440d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7440d-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7440d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7440d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7440d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7440d-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7440d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7440d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7440d-118">Scenario description</span></span>
<span data-ttu-id="7440d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7440d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7440d-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="7440d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7440d-121">Adicionando a frente da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7440d-121">Adding Front from hello gallery</span></span>
2. <span data-ttu-id="7440d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7440d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-hello-gallery"></a><span data-ttu-id="7440d-123">Adicionando a frente da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7440d-123">Adding Front from hello gallery</span></span>
<span data-ttu-id="7440d-124">integração de Olá tooconfigure da frente no AD do Azure, você precisa tooadd frente da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7440d-124">tooconfigure hello integration of Front into Azure AD, you need tooadd Front from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7440d-125">**tooadd frente da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7440d-125">**tooadd Front from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7440d-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7440d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="7440d-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7440d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7440d-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7440d-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="7440d-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7440d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="7440d-133">Na caixa de pesquisa hello, digite **Front**, selecione **Front** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7440d-133">In hello search box, type **Front**, select **Front** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Início da lista de resultados de saudação](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7440d-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7440d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7440d-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Front, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7440d-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7440d-137">Para toowork de logon único, o AD do Azure precisa tooknow que o usuário de contraparte Olá na frente é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7440d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Front is tooa user in Azure AD.</span></span> <span data-ttu-id="7440d-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado Olá na frente precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7440d-138">In other words, a link relationship between an Azure AD user and hello related user in Front needs toobe established.</span></span>

<span data-ttu-id="7440d-139">No futuro, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="7440d-139">In Front, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7440d-140">tooconfigure e teste de logon único do AD do Azure com início, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="7440d-140">tooconfigure and test Azure AD single sign-on with Front, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7440d-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7440d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7440d-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7440d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7440d-143">**[Criar um usuário de teste de frente](#create-a-front-test-user)**  -toohave um equivalente de Britta Simon na frente, o que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="7440d-143">**[Create a Front test user](#create-a-front-test-user)** - toohave a counterpart of Britta Simon in Front that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7440d-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="7440d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7440d-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="7440d-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7440d-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7440d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7440d-147">Nesta seção, habilitar o AD do Azure-logon único no portal do Azure de saudação e configurar o logon único em seu aplicativo de início.</span><span class="sxs-lookup"><span data-stu-id="7440d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="7440d-148">**tooconfigure logon único do AD do Azure com início, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7440d-148">**tooconfigure Azure AD single sign-on with Front, perform hello following steps:**</span></span>

1. <span data-ttu-id="7440d-149">Em Olá portal do Azure, Olá **Front** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="7440d-149">In hello Azure portal, on hello **Front** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="7440d-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="7440d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="7440d-153">Em Olá **domínio Front e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="7440d-153">On hello **Front Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="7440d-155">a.</span><span class="sxs-lookup"><span data-stu-id="7440d-155">a.</span></span> <span data-ttu-id="7440d-156">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="7440d-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="7440d-157">b.</span><span class="sxs-lookup"><span data-stu-id="7440d-157">b.</span></span> <span data-ttu-id="7440d-158">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="7440d-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="7440d-159">Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="7440d-159">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="7440d-161">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="7440d-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7440d-162">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="7440d-162">These values are not real.</span></span> <span data-ttu-id="7440d-163">Atualizar esses valores com hello real identificador, URL de resposta e URL de entrada que são explicadas posteriormente no tutorial ou entre em contato com [equipe de suporte de cliente Front](mailto:support@frontapp.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="7440d-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) tooget these values.</span></span> 

5. <span data-ttu-id="7440d-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7440d-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="7440d-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7440d-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="7440d-168">Em Olá **configuração Front** seção, clique em **configurar Front** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="7440d-168">On hello **Front Configuration** section, click **Configure Front** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7440d-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="7440d-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="7440d-171">Locatário de frente tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="7440d-171">Sign-on tooyour Front tenant as an administrator.</span></span>

9. <span data-ttu-id="7440d-172">Vá muito**configurações (ícone de engrenagem na parte inferior de saudação do lateral esquerda Olá) > Preferências**.</span><span class="sxs-lookup"><span data-stu-id="7440d-172">Go too**Settings (cog icon at hello bottom of hello left sidebar) > Preferences**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="7440d-174">Clique no link **Logon Único** .</span><span class="sxs-lookup"><span data-stu-id="7440d-174">Click **Single Sign On** link.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="7440d-176">Selecione **SAML** na lista suspensa de saudação do **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="7440d-176">Select **SAML** in hello drop-down list of **Single Sign On**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="7440d-178">Em Olá **ponto de entrada** caixa de texto colocar o valor de saudação de **o URL de serviço de logon único** do Assistente de configuração de aplicativo do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7440d-178">In hello **Entry Point** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="7440d-180">Abra seu baixado **Certificate(Base64)** no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado de autenticação** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="7440d-180">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Signing certificate** textbox.</span></span>
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="7440d-182">Em Olá **as configurações do provedor de serviço** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7440d-182">On hello **Service provider settings** section, perform hello following steps:</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="7440d-184">a.</span><span class="sxs-lookup"><span data-stu-id="7440d-184">a.</span></span> <span data-ttu-id="7440d-185">Copie o valor de saudação do **ID da entidade** e cole-a saudação **identificador** textbox em **domínio Front e URLs** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7440d-185">Copy hello value of **Entity ID** and paste it into hello **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="7440d-186">b.</span><span class="sxs-lookup"><span data-stu-id="7440d-186">b.</span></span> <span data-ttu-id="7440d-187">Copie o valor de saudação do **URL do ACS** e cole-a saudação **URL de logon** textbox em **domínio Front e URLs** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7440d-187">Copy hello value of **ACS URL** and paste it into hello **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="7440d-188">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7440d-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="7440d-189">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="7440d-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7440d-190">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="7440d-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7440d-191">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7440d-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7440d-192">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7440d-192">Create an Azure AD test user</span></span>

<span data-ttu-id="7440d-193">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7440d-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="7440d-195">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7440d-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7440d-196">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="7440d-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7440d-198">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="7440d-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7440d-200">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7440d-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7440d-202">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7440d-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7440d-204">a.</span><span class="sxs-lookup"><span data-stu-id="7440d-204">a.</span></span> <span data-ttu-id="7440d-205">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7440d-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7440d-206">b.</span><span class="sxs-lookup"><span data-stu-id="7440d-206">b.</span></span> <span data-ttu-id="7440d-207">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7440d-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7440d-208">c.</span><span class="sxs-lookup"><span data-stu-id="7440d-208">c.</span></span> <span data-ttu-id="7440d-209">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="7440d-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7440d-210">d.</span><span class="sxs-lookup"><span data-stu-id="7440d-210">d.</span></span> <span data-ttu-id="7440d-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7440d-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="7440d-212">Criar um usuário de teste do Front</span><span class="sxs-lookup"><span data-stu-id="7440d-212">Create a Front test user</span></span>

<span data-ttu-id="7440d-213">Nesta seção, você criará uma usuária chamada Britta Simon no Front.</span><span class="sxs-lookup"><span data-stu-id="7440d-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="7440d-214">Trabalhar com [equipe de suporte de cliente Front](mailto:support@frontapp.com) para adicionar usuários de saudação na plataforma de frente hello.</span><span class="sxs-lookup"><span data-stu-id="7440d-214">Work with [Front Client support team](mailto:support@frontapp.com) to add hello users in hello Front platform.</span></span> <span data-ttu-id="7440d-215">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="7440d-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7440d-216">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7440d-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7440d-217">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooFront.</span><span class="sxs-lookup"><span data-stu-id="7440d-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFront.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="7440d-219">**tooassign Britta Simon tooFront, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7440d-219">**tooassign Britta Simon tooFront, perform hello following steps:**</span></span>

1. <span data-ttu-id="7440d-220">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7440d-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7440d-222">Na lista de aplicativos hello, selecione **Front**.</span><span class="sxs-lookup"><span data-stu-id="7440d-222">In hello applications list, select **Front**.</span></span>

    ![link de início Olá na lista de aplicativos Olá](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="7440d-224">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7440d-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="7440d-226">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7440d-226">Click **Add** button.</span></span> <span data-ttu-id="7440d-227">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7440d-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="7440d-229">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="7440d-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7440d-230">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7440d-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7440d-231">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7440d-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7440d-232">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="7440d-232">Test single sign-on</span></span>

<span data-ttu-id="7440d-233">Olá o objetivo desta seção é tootest usando o Azure AD SSOconfiguration Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="7440d-233">hello objective of this section is tootest your Azure AD SSOconfiguration using hello Access Panel.</span></span>

<span data-ttu-id="7440d-234">Quando você clica em um bloco de frente Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado em aplicativo de início.</span><span class="sxs-lookup"><span data-stu-id="7440d-234">When you click hello Front tile in hello Access Panel, you should get automatically signed-on tooyour Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7440d-235">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7440d-235">Additional resources</span></span>

* [<span data-ttu-id="7440d-236">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7440d-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7440d-237">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7440d-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

