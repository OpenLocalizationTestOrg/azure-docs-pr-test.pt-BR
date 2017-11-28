---
title: "Tutorial: Integração do Azure Active Directory ao RFPIO | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="05a6d-103">Tutorial: Integração do Azure Active Directory ao RFPIO</span><span class="sxs-lookup"><span data-stu-id="05a6d-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="05a6d-104">Neste tutorial, você aprenderá como toointegrate RFPIO com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="05a6d-104">In this tutorial, you learn how toointegrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05a6d-105">Integrando RFPIO com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="05a6d-105">Integrating RFPIO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="05a6d-106">Você pode controlar quem no AD do Azure que tenha acesso tooRFPIO.</span><span class="sxs-lookup"><span data-stu-id="05a6d-106">You can control who in Azure AD who has access tooRFPIO.</span></span>
- <span data-ttu-id="05a6d-107">Você pode habilitar seu usuários tooautomatically get conectado tooRFPIO (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="05a6d-107">You can enable your users tooautomatically get signed-on tooRFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="05a6d-108">Você pode gerenciar suas contas em um local central – Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="05a6d-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="05a6d-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05a6d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05a6d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="05a6d-110">Prerequisites</span></span>

<span data-ttu-id="05a6d-111">tooconfigure integração do AD do Azure com RFPIO, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="05a6d-111">tooconfigure Azure AD integration with RFPIO, you need hello following items:</span></span>

- <span data-ttu-id="05a6d-112">Uma assinatura do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05a6d-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="05a6d-113">Uma assinatura habilitada para logon único do RFPIO.</span><span class="sxs-lookup"><span data-stu-id="05a6d-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="05a6d-114">Não é recomendável que você use um etapas Olá tootest do ambiente de produção neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="05a6d-114">We don't recommend that you use a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="05a6d-115">etapas de saudação tootest neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="05a6d-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="05a6d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="05a6d-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="05a6d-117">Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05a6d-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05a6d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="05a6d-118">Scenario description</span></span>
<span data-ttu-id="05a6d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="05a6d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05a6d-120">cenário de saudação que é descrito neste tutorial consiste em duas principais blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="05a6d-120">hello scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05a6d-121">Adicionando RFPIO da Galeria de saudação.</span><span class="sxs-lookup"><span data-stu-id="05a6d-121">Adding RFPIO from hello gallery.</span></span>
2. <span data-ttu-id="05a6d-122">Configurar e testar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05a6d-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-hello-gallery"></a><span data-ttu-id="05a6d-123">Adicionar RFPIO da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="05a6d-123">Add RFPIO from hello gallery</span></span>
<span data-ttu-id="05a6d-124">integração de saudação tooconfigure de RFPIO no AD do Azure, você precisa tooadd RFPIO da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="05a6d-124">tooconfigure hello integration of RFPIO into Azure AD, you need tooadd RFPIO from hello gallery tooyour list of managed SaaS apps.</span></span>

### <a name="tooadd-rfpio-from-hello-gallery"></a><span data-ttu-id="05a6d-125">tooadd RFPIO da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="05a6d-125">tooadd RFPIO from hello gallery</span></span>

1. <span data-ttu-id="05a6d-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, selecione Olá **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="05a6d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="05a6d-128">Selecione **Aplicativos da empresa**, em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="05a6d-130">tooadd um novo aplicativo, selecione Olá **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="05a6d-130">tooadd a new application, select hello **New application** button on hello top of dialog box.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="05a6d-132">Na caixa de pesquisa hello, digite **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-132">In hello search box, type **RFPIO**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="05a6d-134">No painel de resultados de saudação, selecione **RFPIO**e, em seguida, selecione Olá **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="05a6d-134">In hello results panel, select **RFPIO**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="05a6d-136">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a6d-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="05a6d-137">Nesta seção, você configurará e testará o logon único do Azure AD com o RFPIO, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="05a6d-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="05a6d-138">Para toowork de logon único, o AD do Azure precisa tooknow qual relação hello está entre o usuário correspondente em RFPIO e um usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="05a6d-138">For single sign-on toowork, Azure AD needs tooknow what hello relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="05a6d-139">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em RFPIO precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="05a6d-139">In other words, a link relationship between an Azure AD user and hello related user in RFPIO needs toobe established.</span></span>

<span data-ttu-id="05a6d-140">Em RFPIO, atribuir o valor de saudação do **nome de usuário** no AD do Azure como valor de saudação do **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="05a6d-140">In RFPIO, assign hello value of **user name** in Azure AD as hello value of  **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="05a6d-141">tooconfigure e teste de logon único do AD do Azure com RFPIO, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="05a6d-141">tooconfigure and test Azure AD single sign-on with RFPIO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="05a6d-142">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**– tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="05a6d-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="05a6d-143">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**– tootest logon único do AD do Azure com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05a6d-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05a6d-144">**[Criar um usuário de teste RFPIO](#creating-a-rfpio-test-user)**  - toohave um equivalente do Britta Simon em RFPIO é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="05a6d-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --toohave a counterpart of Britta Simon in RFPIO that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="05a6d-145">**[Atribuir um usuário de teste de saudação do AD do Azure](#assigning-the-azure-ad-test-user)**– tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="05a6d-145">**[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05a6d-146">**[Testar o logon único](#testing-single-sign-on)**  – tooverify se Olá configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="05a6d-146">**[Test Single Sign-On](#testing-single-sign-on)** --tooverify if hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="05a6d-147">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a6d-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="05a6d-148">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo RFPIO.</span><span class="sxs-lookup"><span data-stu-id="05a6d-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="05a6d-149">**tooconfigure AD do Azure-logon único com RFPIO, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="05a6d-149">**tooconfigure Azure AD single sign-on with RFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="05a6d-150">Em Olá portal do Azure, Olá **RFPIO** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-150">In hello Azure portal, on hello **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="05a6d-152">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="05a6d-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="05a6d-154">Em Olá **RFPIO domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="05a6d-154">On hello **RFPIO Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="05a6d-156">a.</span><span class="sxs-lookup"><span data-stu-id="05a6d-156">a.</span></span> <span data-ttu-id="05a6d-157">Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="05a6d-157">In hello **Identifier** textbox, type hello URL: `https://www.rfpio.com`</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="05a6d-159">b.</span><span class="sxs-lookup"><span data-stu-id="05a6d-159">b.</span></span> <span data-ttu-id="05a6d-160">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="05a6d-161">c.</span><span class="sxs-lookup"><span data-stu-id="05a6d-161">c.</span></span> <span data-ttu-id="05a6d-162">Em Olá **estado de retransmissão** caixa de texto Digite um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="05a6d-162">In hello **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="05a6d-163">Entre em contato com [RFPIO equipe de suporte](https://www.rfpio.com/contact/) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="05a6d-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) tooget this value.</span></span> 

4. <span data-ttu-id="05a6d-164">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="05a6d-165">Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="05a6d-165">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>   

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="05a6d-167">Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="05a6d-167">In hello **Sign on URL** textbox, type hello URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="05a6d-168">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="05a6d-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="05a6d-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="05a6d-170">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="05a6d-172">Em uma janela de navegador web diferente, o logon toohello **RFPIO** site como um administrador.</span><span class="sxs-lookup"><span data-stu-id="05a6d-172">In a different web browser window, login toohello **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="05a6d-173">Clique em Olá inferior esquerda suspenso.</span><span class="sxs-lookup"><span data-stu-id="05a6d-173">Click on hello bottom left corner dropdown.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="05a6d-175">Clique em Olá **as configurações da organização**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-175">Click on hello **Organization Settings**.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="05a6d-177">Clique em Olá **recursos e integração**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-177">Click on hello **FEATURES & INTEGRATION**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="05a6d-179">Em Olá **configuração de SSO de SAML** clique **editar**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-179">In hello **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="05a6d-181">Nesta seção, execute as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="05a6d-181">In this Section perform following actions:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="05a6d-183">a.</span><span class="sxs-lookup"><span data-stu-id="05a6d-183">a.</span></span> <span data-ttu-id="05a6d-184">Copiar o conteúdo de saudação do hello **XML de metadados baixado** e cole-a saudação **configuração de identidade** campo.</span><span class="sxs-lookup"><span data-stu-id="05a6d-184">Copy hello content of hello **Downloaded Metadata XML** and paste it into hello **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="05a6d-185">baixado toocopy Olá conteúdo de **Metadata XML** Use **o bloco de notas + +** ou adequada **Editor XML**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-185">toocopy hello content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="05a6d-186">b.</span><span class="sxs-lookup"><span data-stu-id="05a6d-186">b.</span></span> <span data-ttu-id="05a6d-187">Clique em **Validar**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-187">Click **Validate**.</span></span>

    <span data-ttu-id="05a6d-188">c.</span><span class="sxs-lookup"><span data-stu-id="05a6d-188">c.</span></span> <span data-ttu-id="05a6d-189">Depois de clicar em **validar**, inverter **SAML(Enabled)** tooon.</span><span class="sxs-lookup"><span data-stu-id="05a6d-189">After Clicking **Validate**, Flip **SAML(Enabled)** tooon.</span></span>

    <span data-ttu-id="05a6d-190">d.</span><span class="sxs-lookup"><span data-stu-id="05a6d-190">d.</span></span> <span data-ttu-id="05a6d-191">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="05a6d-192">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="05a6d-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="05a6d-193">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="05a6d-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="05a6d-194">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="05a6d-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="05a6d-195">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a6d-195">Create an Azure AD test user</span></span>
<span data-ttu-id="05a6d-196">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="05a6d-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="05a6d-198">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="05a6d-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="05a6d-199">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="05a6d-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="05a6d-201">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="05a6d-203">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="05a6d-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="05a6d-205">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="05a6d-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="05a6d-207">a.</span><span class="sxs-lookup"><span data-stu-id="05a6d-207">a.</span></span> <span data-ttu-id="05a6d-208">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05a6d-209">b.</span><span class="sxs-lookup"><span data-stu-id="05a6d-209">b.</span></span> <span data-ttu-id="05a6d-210">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="05a6d-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="05a6d-211">c.</span><span class="sxs-lookup"><span data-stu-id="05a6d-211">c.</span></span> <span data-ttu-id="05a6d-212">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="05a6d-213">d.</span><span class="sxs-lookup"><span data-stu-id="05a6d-213">d.</span></span> <span data-ttu-id="05a6d-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="05a6d-215">Criar um usuário de teste do RFPIO</span><span class="sxs-lookup"><span data-stu-id="05a6d-215">Create a RFPIO test user</span></span>

<span data-ttu-id="05a6d-216">tooenable AD do Azure usuários toolog em tooRFPIO, eles devem ser provisionados no RFPIO.</span><span class="sxs-lookup"><span data-stu-id="05a6d-216">tooenable Azure AD users toolog in tooRFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="05a6d-217">No caso de saudação de RFPIO, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="05a6d-217">In hello case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="05a6d-218">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="05a6d-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="05a6d-219">Faça logon em tooyour site da empresa RFPIO como um administrador.</span><span class="sxs-lookup"><span data-stu-id="05a6d-219">Log in tooyour RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="05a6d-220">Clique em Olá inferior esquerda suspenso.</span><span class="sxs-lookup"><span data-stu-id="05a6d-220">Click on hello bottom left corner dropdown.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="05a6d-222">Clique em Olá **as configurações da organização**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-222">Click on hello **Organization Settings**.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="05a6d-224">Clique em **MEMBROS DA EQUIPE**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-224">Click **TEAM MEMBERS**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="05a6d-226">Clique em **ADICIONAR MEMBROS**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-226">Click on **ADD MEMBERS**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="05a6d-228">Em Olá **adicionar novos membros** seção.</span><span class="sxs-lookup"><span data-stu-id="05a6d-228">In hello **Add New Members** section.</span></span> <span data-ttu-id="05a6d-229">Execute as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="05a6d-229">Perform following actions:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="05a6d-231">a.</span><span class="sxs-lookup"><span data-stu-id="05a6d-231">a.</span></span> <span data-ttu-id="05a6d-232">Insira **endereço de Email** em Olá **Insira um email por linha** campo.</span><span class="sxs-lookup"><span data-stu-id="05a6d-232">Enter **Email address** in hello **Enter one email per line** field.</span></span>

    <span data-ttu-id="05a6d-233">b.</span><span class="sxs-lookup"><span data-stu-id="05a6d-233">b.</span></span> <span data-ttu-id="05a6d-234">Selecione **Função** de acordo com seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="05a6d-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="05a6d-235">c.</span><span class="sxs-lookup"><span data-stu-id="05a6d-235">c.</span></span> <span data-ttu-id="05a6d-236">Clique em **ADICIONAR MEMBROS**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="05a6d-237">proprietário de conta do Active Directory do Azure Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="05a6d-237">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="05a6d-238">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="05a6d-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="05a6d-239">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooRFPIO.</span><span class="sxs-lookup"><span data-stu-id="05a6d-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRFPIO.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="05a6d-241">**tooassign Britta Simon tooRFPIO, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="05a6d-241">**tooassign Britta Simon tooRFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="05a6d-242">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="05a6d-244">Na lista de aplicativos hello, selecione **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-244">In hello applications list, select **RFPIO**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="05a6d-246">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="05a6d-248">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="05a6d-248">Click **Add** button.</span></span> <span data-ttu-id="05a6d-249">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="05a6d-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="05a6d-251">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="05a6d-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="05a6d-252">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="05a6d-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="05a6d-253">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="05a6d-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="05a6d-254">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="05a6d-254">Test single sign-on</span></span>

<span data-ttu-id="05a6d-255">Nesta seção, você pode testar a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="05a6d-255">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="05a6d-256">Quando você clica em Olá RFPIO bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de RFPIO.</span><span class="sxs-lookup"><span data-stu-id="05a6d-256">When you click hello RFPIO tile in hello Access Panel, you should get automatically signed-on tooyour RFPIO application.</span></span>
<span data-ttu-id="05a6d-257">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05a6d-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="05a6d-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="05a6d-258">Additional resources</span></span>

* [<span data-ttu-id="05a6d-259">Lista de tutoriais sobre como toointegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="05a6d-259">List of tutorials about how toointegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05a6d-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="05a6d-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

