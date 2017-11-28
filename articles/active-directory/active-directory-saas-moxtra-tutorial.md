---
title: "Tutorial: Integração do Azure Active Directory com o Moxtra | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="ab1af-103">Tutorial: integração do Active Directory do Azure ao Moxtra</span><span class="sxs-lookup"><span data-stu-id="ab1af-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="ab1af-104">Neste tutorial, você aprenderá como toointegrate o Moxtra com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="ab1af-104">In this tutorial, you learn how toointegrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ab1af-105">Integrando o Moxtra com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab1af-105">Integrating Moxtra with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ab1af-106">Você pode controlar no AD do Azure que tenha acesso tooMoxtra</span><span class="sxs-lookup"><span data-stu-id="ab1af-106">You can control in Azure AD who has access tooMoxtra</span></span>
- <span data-ttu-id="ab1af-107">Você pode habilitar seu usuários tooautomatically get conectado tooMoxtra (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab1af-107">You can enable your users tooautomatically get signed-on tooMoxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ab1af-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ab1af-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ab1af-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ab1af-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab1af-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ab1af-110">Prerequisites</span></span>

<span data-ttu-id="ab1af-111">tooconfigure integração do AD do Azure com o Moxtra, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab1af-111">tooconfigure Azure AD integration with Moxtra, you need hello following items:</span></span>

- <span data-ttu-id="ab1af-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab1af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ab1af-113">Uma assinatura habilitada para logon único do Moxtra</span><span class="sxs-lookup"><span data-stu-id="ab1af-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ab1af-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ab1af-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ab1af-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ab1af-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ab1af-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ab1af-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ab1af-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab1af-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab1af-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ab1af-118">Scenario description</span></span>
<span data-ttu-id="ab1af-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ab1af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ab1af-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="ab1af-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab1af-121">Adicionando o Moxtra da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ab1af-121">Adding Moxtra from hello gallery</span></span>
2. <span data-ttu-id="ab1af-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab1af-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-hello-gallery"></a><span data-ttu-id="ab1af-123">Adicionando o Moxtra da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ab1af-123">Adding Moxtra from hello gallery</span></span>
<span data-ttu-id="ab1af-124">integração de saudação tooconfigure do Moxtra no AD do Azure, você precisa tooadd o Moxtra da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ab1af-124">tooconfigure hello integration of Moxtra into Azure AD, you need tooadd Moxtra from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ab1af-125">**tooadd o Moxtra da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ab1af-125">**tooadd Moxtra from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab1af-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ab1af-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ab1af-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ab1af-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ab1af-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab1af-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ab1af-133">Na caixa de pesquisa hello, digite **o Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-133">In hello search box, type **Moxtra**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="ab1af-135">No painel de resultados de saudação, selecione **o Moxtra**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ab1af-135">In hello results panel, select **Moxtra**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ab1af-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab1af-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ab1af-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Moxtra, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ab1af-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ab1af-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Moxtra é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab1af-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Moxtra is tooa user in Azure AD.</span></span> <span data-ttu-id="ab1af-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Moxtra precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ab1af-140">In other words, a link relationship between an Azure AD user and hello related user in Moxtra needs toobe established.</span></span>

<span data-ttu-id="ab1af-141">O Moxtra, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab1af-141">In Moxtra, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ab1af-142">tooconfigure e teste de logon único do AD do Azure com o Moxtra, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab1af-142">tooconfigure and test Azure AD single sign-on with Moxtra, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ab1af-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ab1af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ab1af-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ab1af-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ab1af-145">**[Criar um usuário de teste o Moxtra](#creating-a-moxtra-test-user)**  -toohave um equivalente do Britta Simon no Moxtra que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="ab1af-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - toohave a counterpart of Britta Simon in Moxtra that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ab1af-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="ab1af-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab1af-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="ab1af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ab1af-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab1af-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ab1af-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo o Moxtra.</span><span class="sxs-lookup"><span data-stu-id="ab1af-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="ab1af-150">**tooconfigure AD do Azure-logon único com o Moxtra, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ab1af-150">**tooconfigure Azure AD single sign-on with Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab1af-151">Em Olá portal do Azure, Olá **o Moxtra** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-151">In hello Azure portal, on hello **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ab1af-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="ab1af-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="ab1af-155">Em Olá **o Moxtra domínio e URLs** , execute Olá etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab1af-155">On hello **Moxtra Domain and URLs** section, perform hello following step:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="ab1af-157">Em Olá **URL de logon** caixa de texto, digite um URL como:`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="ab1af-157">In hello **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="ab1af-158">O Moxtra aplicativo espera as asserções de SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="ab1af-158">Moxtra application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="ab1af-159">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ab1af-159">Configure hello following claims for this application.</span></span> <span data-ttu-id="ab1af-160">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab1af-160">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ab1af-161">Olá captura de tela a seguir mostra um exemplo para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="ab1af-161">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="ab1af-163">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab1af-163">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="ab1af-164">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="ab1af-164">Attribute Name</span></span> | <span data-ttu-id="ab1af-165">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="ab1af-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ab1af-166">nome</span><span class="sxs-lookup"><span data-stu-id="ab1af-166">firstname</span></span> | <span data-ttu-id="ab1af-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ab1af-167">user.givenname</span></span> |
    | <span data-ttu-id="ab1af-168">sobrenome</span><span class="sxs-lookup"><span data-stu-id="ab1af-168">lastname</span></span> | <span data-ttu-id="ab1af-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="ab1af-169">user.surname</span></span> |
    | <span data-ttu-id="ab1af-170">idpid</span><span class="sxs-lookup"><span data-stu-id="ab1af-170">idpid</span></span>    | <span data-ttu-id="ab1af-171"><ID da Entidade SAML></span><span class="sxs-lookup"><span data-stu-id="ab1af-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="ab1af-172">Olá valor **idpid** atributo não é real.</span><span class="sxs-lookup"><span data-stu-id="ab1af-172">hello value of **idpid** attribute is not real.</span></span> <span data-ttu-id="ab1af-173">Você pode obter o valor real de saudação do **referência rápida** seção em **o Moxtra configuração**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-173">You can get hello actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="ab1af-174">a.</span><span class="sxs-lookup"><span data-stu-id="ab1af-174">a.</span></span> <span data-ttu-id="ab1af-175">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab1af-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="ab1af-177">b.</span><span class="sxs-lookup"><span data-stu-id="ab1af-177">b.</span></span> <span data-ttu-id="ab1af-178">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="ab1af-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ab1af-180">c.</span><span class="sxs-lookup"><span data-stu-id="ab1af-180">c.</span></span> <span data-ttu-id="ab1af-181">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="ab1af-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="ab1af-182">d.</span><span class="sxs-lookup"><span data-stu-id="ab1af-182">d.</span></span> <span data-ttu-id="ab1af-183">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="ab1af-184">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ab1af-184">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="ab1af-186">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ab1af-186">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ab1af-188">Em Olá **configuração o Moxtra** seção, clique em **o Moxtra configurar** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="ab1af-188">On hello **Moxtra Configuration** section, click **Configure Moxtra** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ab1af-189">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="ab1af-189">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="ab1af-191">Em outra janela do navegador, entre no site da empresa tooyour o Moxtra como um administrador.</span><span class="sxs-lookup"><span data-stu-id="ab1af-191">In another browser window, sign on tooyour Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="ab1af-192">Na barra de ferramentas Olá Olá esquerda, clique em **Console de Administração > logon único do SAML**e, em seguida, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-192">In hello toolbar on hello left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="ab1af-194">Em Olá **SAML** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab1af-194">On hello **SAML** page, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="ab1af-196">a.</span><span class="sxs-lookup"><span data-stu-id="ab1af-196">a.</span></span> <span data-ttu-id="ab1af-197">Em Olá **nome** caixa de texto, digite um nome para a sua configuração (por exemplo: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="ab1af-197">In hello **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="ab1af-198">b.</span><span class="sxs-lookup"><span data-stu-id="ab1af-198">b.</span></span> <span data-ttu-id="ab1af-199">Em hello **ID da entidade IdP** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab1af-199">In hello **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="ab1af-200">c.</span><span class="sxs-lookup"><span data-stu-id="ab1af-200">c.</span></span> <span data-ttu-id="ab1af-201">Em **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab1af-201">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="ab1af-202">d.</span><span class="sxs-lookup"><span data-stu-id="ab1af-202">d.</span></span> <span data-ttu-id="ab1af-203">Em Olá **AuthnContextClassRef** caixa de texto, tipo **urn: oasis: nomes: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-203">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="ab1af-204">e.</span><span class="sxs-lookup"><span data-stu-id="ab1af-204">e.</span></span> <span data-ttu-id="ab1af-205">Em Olá **formato NameID** caixa de texto, tipo **urn: oasis: nomes: tc: SAML: 1.1 nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-205">In hello **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="ab1af-206">f.</span><span class="sxs-lookup"><span data-stu-id="ab1af-206">f.</span></span> <span data-ttu-id="ab1af-207">Abra certificado que você baixou do portal do Azure no bloco de notas, copie o conteúdo de saudação e, em seguida, cole-o em Olá **certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="ab1af-207">Open certificate which you have downloaded from Azure portal in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="ab1af-208">g.</span><span class="sxs-lookup"><span data-stu-id="ab1af-208">g.</span></span> <span data-ttu-id="ab1af-209">No domínio de email SAML de saudação texto, digite seu domínio de email SAML.</span><span class="sxs-lookup"><span data-stu-id="ab1af-209">In hello SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="ab1af-210">domínio de saudação do tooverify toosee Olá etapas, clique em hello "****" abaixo.</span><span class="sxs-lookup"><span data-stu-id="ab1af-210">toosee hello steps tooverify hello domain, click hello "**i**" below.</span></span>

    <span data-ttu-id="ab1af-211">h.</span><span class="sxs-lookup"><span data-stu-id="ab1af-211">h.</span></span> <span data-ttu-id="ab1af-212">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="ab1af-213">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="ab1af-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ab1af-214">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ab1af-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ab1af-215">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ab1af-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ab1af-216">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab1af-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="ab1af-217">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab1af-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ab1af-219">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ab1af-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab1af-220">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ab1af-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ab1af-222">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ab1af-224">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab1af-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ab1af-226">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab1af-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ab1af-228">a.</span><span class="sxs-lookup"><span data-stu-id="ab1af-228">a.</span></span> <span data-ttu-id="ab1af-229">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ab1af-230">b.</span><span class="sxs-lookup"><span data-stu-id="ab1af-230">b.</span></span> <span data-ttu-id="ab1af-231">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ab1af-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ab1af-232">c.</span><span class="sxs-lookup"><span data-stu-id="ab1af-232">c.</span></span> <span data-ttu-id="ab1af-233">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ab1af-234">d.</span><span class="sxs-lookup"><span data-stu-id="ab1af-234">d.</span></span> <span data-ttu-id="ab1af-235">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="ab1af-236">Criar um usuário de teste Moxtra</span><span class="sxs-lookup"><span data-stu-id="ab1af-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="ab1af-237">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no Moxtra.</span><span class="sxs-lookup"><span data-stu-id="ab1af-237">hello objective of this section is toocreate a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="ab1af-238">**toocreate um usuário chamado Britta Simon no Moxtra, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ab1af-238">**toocreate a user called Britta Simon in Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab1af-239">Faça logon no tooyour o Moxtra site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="ab1af-239">Sign on tooyour Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="ab1af-240">Na barra de ferramentas Olá Olá esquerda, clique em **Console de Administração > Gerenciamento de usuário**e, em seguida, **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-240">In hello toolbar on hello left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="ab1af-242">Em Olá **adicionar usuário** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab1af-242">On hello **Add User** dialog, perform hello following steps:</span></span>
  
    <span data-ttu-id="ab1af-243">a.</span><span class="sxs-lookup"><span data-stu-id="ab1af-243">a.</span></span> <span data-ttu-id="ab1af-244">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-244">In hello **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="ab1af-245">b.</span><span class="sxs-lookup"><span data-stu-id="ab1af-245">b.</span></span> <span data-ttu-id="ab1af-246">Em Olá **Sobrenome** caixa de texto, tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-246">In hello **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="ab1af-247">c.</span><span class="sxs-lookup"><span data-stu-id="ab1af-247">c.</span></span> <span data-ttu-id="ab1af-248">Em Olá **Email** caixa de texto, tipo de endereço de email de Britta igual em portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab1af-248">In hello **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="ab1af-249">d.</span><span class="sxs-lookup"><span data-stu-id="ab1af-249">d.</span></span> <span data-ttu-id="ab1af-250">Em Olá **divisão** caixa de texto, tipo **desenvolvimento**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-250">In hello **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="ab1af-251">e.</span><span class="sxs-lookup"><span data-stu-id="ab1af-251">e.</span></span> <span data-ttu-id="ab1af-252">Em Olá **departamento** caixa de texto, tipo **IT**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-252">In hello **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="ab1af-253">f.</span><span class="sxs-lookup"><span data-stu-id="ab1af-253">f.</span></span> <span data-ttu-id="ab1af-254">Selecione **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="ab1af-255">g.</span><span class="sxs-lookup"><span data-stu-id="ab1af-255">g.</span></span> <span data-ttu-id="ab1af-256">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ab1af-257">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab1af-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ab1af-258">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMoxtra.</span><span class="sxs-lookup"><span data-stu-id="ab1af-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMoxtra.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ab1af-260">**tooassign Britta Simon tooMoxtra, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ab1af-260">**tooassign Britta Simon tooMoxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab1af-261">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ab1af-263">Na lista de aplicativos hello, selecione **o Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-263">In hello applications list, select **Moxtra**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="ab1af-265">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ab1af-267">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ab1af-267">Click **Add** button.</span></span> <span data-ttu-id="ab1af-268">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab1af-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ab1af-270">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab1af-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ab1af-271">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab1af-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ab1af-272">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab1af-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ab1af-273">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ab1af-273">Testing single sign-on</span></span>

<span data-ttu-id="ab1af-274">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab1af-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ab1af-275">Quando você clica em bloco o Moxtra Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour o Moxtra aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab1af-275">When you click hello Moxtra tile in hello Access Panel, you should get automatically signed-on tooyour Moxtra application.</span></span>
<span data-ttu-id="ab1af-276">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ab1af-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ab1af-277">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ab1af-277">Additional resources</span></span>

* [<span data-ttu-id="ab1af-278">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ab1af-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab1af-279">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ab1af-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

