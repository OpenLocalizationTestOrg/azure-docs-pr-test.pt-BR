---
title: "Tutorial: Integração do Azure Active Directory com o NetSuite | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="5ecee-103">Tutorial: Integração do Azure Active Directory com o Netsuite</span><span class="sxs-lookup"><span data-stu-id="5ecee-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="5ecee-104">Neste tutorial, você aprenderá como toointegrate Netsuite com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="5ecee-104">In this tutorial, you learn how toointegrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ecee-105">Integrando o Netsuite com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ecee-105">Integrating Netsuite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5ecee-106">Você pode controlar no AD do Azure que tenha acesso tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="5ecee-106">You can control in Azure AD who has access tooNetsuite</span></span>
- <span data-ttu-id="5ecee-107">Você pode habilitar seu usuários tooautomatically get conectado tooNetsuite (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ecee-107">You can enable your users tooautomatically get signed-on tooNetsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ecee-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5ecee-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5ecee-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5ecee-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ecee-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5ecee-110">Prerequisites</span></span>

<span data-ttu-id="5ecee-111">tooconfigure integração do AD do Azure com o Netsuite, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ecee-111">tooconfigure Azure AD integration with Netsuite, you need hello following items:</span></span>

- <span data-ttu-id="5ecee-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ecee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ecee-113">Uma assinatura habilitada para logon único do Netsuite</span><span class="sxs-lookup"><span data-stu-id="5ecee-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ecee-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5ecee-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ecee-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5ecee-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ecee-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5ecee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5ecee-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ecee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ecee-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5ecee-118">Scenario description</span></span>
<span data-ttu-id="5ecee-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5ecee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ecee-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="5ecee-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ecee-121">Adicionando Netsuite da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5ecee-121">Adding Netsuite from hello gallery</span></span>
2. <span data-ttu-id="5ecee-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ecee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-hello-gallery"></a><span data-ttu-id="5ecee-123">Adicionando Netsuite da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5ecee-123">Adding Netsuite from hello gallery</span></span>
<span data-ttu-id="5ecee-124">integração de saudação tooconfigure do Netsuite no AD do Azure, você precisa tooadd Netsuite da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5ecee-124">tooconfigure hello integration of Netsuite into Azure AD, you need tooadd Netsuite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5ecee-125">**tooadd Netsuite da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5ecee-125">**tooadd Netsuite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ecee-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5ecee-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ecee-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5ecee-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="5ecee-131">Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ecee-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="5ecee-133">Na caixa de pesquisa hello, digite **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-133">In hello search box, type **Netsuite**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="5ecee-135">No painel de resultados de saudação, selecione **Netsuite**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5ecee-135">In hello results panel, select **Netsuite**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5ecee-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ecee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5ecee-138">Nesta seção, você configura e testa o logon único do Azure AD com o Netsuite, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="5ecee-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5ecee-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Netsuite é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ecee-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Netsuite is tooa user in Azure AD.</span></span> <span data-ttu-id="5ecee-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Netsuite precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="5ecee-140">In other words, a link relationship between an Azure AD user and hello related user in Netsuite needs toobe established.</span></span>

<span data-ttu-id="5ecee-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Netsuite.</span><span class="sxs-lookup"><span data-stu-id="5ecee-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Netsuite.</span></span>

<span data-ttu-id="5ecee-142">tooconfigure e teste de logon único do AD do Azure com o Netsuite, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ecee-142">tooconfigure and test Azure AD single sign-on with Netsuite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5ecee-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5ecee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5ecee-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ecee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ecee-145">**[Criar um usuário de teste do Netsuite](#creating-a-netsuite-test-user)**  -toohave um equivalente do Britta Simon no Netsuite é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="5ecee-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - toohave a counterpart of Britta Simon in Netsuite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5ecee-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="5ecee-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ecee-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="5ecee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5ecee-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ecee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5ecee-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo Netsuite.</span><span class="sxs-lookup"><span data-stu-id="5ecee-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="5ecee-150">**tooconfigure AD do Azure-logon único com o Netsuite, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5ecee-150">**tooconfigure Azure AD single sign-on with Netsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ecee-151">Em Olá portal do Azure, Olá **Netsuite** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-151">In hello Azure portal, on hello **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="5ecee-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="5ecee-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="5ecee-155">Em Olá **Netsuite domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ecee-155">On hello **Netsuite Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="5ecee-157">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="5ecee-157">In hello **Reply URL** textbox, type a URL using hello following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5ecee-158">Esse valor não é o valor real.</span><span class="sxs-lookup"><span data-stu-id="5ecee-158">This value is not real value.</span></span> <span data-ttu-id="5ecee-159">Valor de saudação de atualização com hello URL de resposta real.</span><span class="sxs-lookup"><span data-stu-id="5ecee-159">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="5ecee-160">Entre em contato com [equipe de suporte do Netsuite](http://www.netsuite.com/portal/services/support.shtml) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="5ecee-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) tooget this value.</span></span>
 
4. <span data-ttu-id="5ecee-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5ecee-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="5ecee-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5ecee-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5ecee-165">Em Olá **Netsuite configuração** seção, clique em **configurar Netsuite** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="5ecee-165">On hello **Netsuite Configuration** section, click **Configure Netsuite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5ecee-166">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="5ecee-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="5ecee-168">Abra uma nova guia no navegador e entre no site Netsuite de sua empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="5ecee-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="5ecee-169">Na barra de ferramentas de saudação na parte superior de saudação da página de saudação, clique em **instalação**, em seguida, clique em **Gerenciador de instalação**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-169">In hello toolbar at hello top of hello page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="5ecee-171">De saudação **tarefas de configuração** lista, selecione **integração**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-171">From hello **Setup Tasks** list, select **Integration**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="5ecee-173">Em Olá **gerenciar autenticação** seção, clique em **o logon único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-173">In hello **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="5ecee-175">Em Olá **instalação do SAML** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ecee-175">On hello **SAML Setup** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="5ecee-176">a.</span><span class="sxs-lookup"><span data-stu-id="5ecee-176">a.</span></span> <span data-ttu-id="5ecee-177">Saudação de cópia **Single Sign-On URL do serviço SAML** o valor da **referência rápida** seção **configurar o logon** e cole-a saudação **provedor de identidade Página de logon** campo Netsuite.</span><span class="sxs-lookup"><span data-stu-id="5ecee-177">Copy hello **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into hello **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="5ecee-179">b.</span><span class="sxs-lookup"><span data-stu-id="5ecee-179">b.</span></span> <span data-ttu-id="5ecee-180">No NetSuite, selecione **Método de Autenticação Primária**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="5ecee-181">c.</span><span class="sxs-lookup"><span data-stu-id="5ecee-181">c.</span></span> <span data-ttu-id="5ecee-182">Para o campo de saudação rotulado **metadados do provedor de identidade SAMLV2**, selecione **carregar arquivo de metadados IDP**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-182">For hello field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="5ecee-183">Em seguida, clique em **procurar** arquivo de metadados de saudação tooupload que baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ecee-183">Then click **Browse** tooupload hello metadata file that you downloaded from Azure portal.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="5ecee-185">d.</span><span class="sxs-lookup"><span data-stu-id="5ecee-185">d.</span></span> <span data-ttu-id="5ecee-186">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-186">Click **Submit**.</span></span>

12. <span data-ttu-id="5ecee-187">No Azure AD, clique na caixa de seleção **Exibir e editar todos os outros atributos de usuário** e adicione um atributo.</span><span class="sxs-lookup"><span data-stu-id="5ecee-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="5ecee-189">Para Olá **nome do atributo** , digite em `account`.</span><span class="sxs-lookup"><span data-stu-id="5ecee-189">For hello **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="5ecee-190">Para Olá **o valor do atributo** , digite sua ID de conta do Netsuite Esse valor é constante e alteração de conta.</span><span class="sxs-lookup"><span data-stu-id="5ecee-190">For hello **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="5ecee-191">Instruções sobre como toofind sua ID da conta estão incluídas abaixo:</span><span class="sxs-lookup"><span data-stu-id="5ecee-191">Instructions on how toofind your account ID are included below:</span></span>

      ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="5ecee-193">a.</span><span class="sxs-lookup"><span data-stu-id="5ecee-193">a.</span></span> <span data-ttu-id="5ecee-194">No Netsuite, clique em **instalação** no menu de navegação superior hello.</span><span class="sxs-lookup"><span data-stu-id="5ecee-194">In Netsuite, click **Setup** from hello top navigation menu.</span></span>

    <span data-ttu-id="5ecee-195">b.</span><span class="sxs-lookup"><span data-stu-id="5ecee-195">b.</span></span> <span data-ttu-id="5ecee-196">Em seguida, clique em Olá **tarefas de configuração** seção do menu de navegação à esquerda hello, selecione Olá **integração** seção e, em seguida, clique em **preferências de serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-196">Then click under hello **Setup Tasks** section of hello left navigation menu, select hello **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="5ecee-197">c.</span><span class="sxs-lookup"><span data-stu-id="5ecee-197">c.</span></span> <span data-ttu-id="5ecee-198">Copie a ID da conta Netsuite e cole-a saudação **o valor do atributo** campo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ecee-198">Copy your Netsuite Account ID and paste it into hello **Attribute Value** field in Azure AD.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="5ecee-200">Antes dos usuários podem executar logon único no Netsuite, eles devem primeiro atribua Olá permissões apropriadas no Netsuite.</span><span class="sxs-lookup"><span data-stu-id="5ecee-200">Before users can perform single sign-on into Netsuite, they must first be assigned hello appropriate permissions in Netsuite.</span></span> <span data-ttu-id="5ecee-201">Siga as instruções de saudação abaixo tooassign essas permissões.</span><span class="sxs-lookup"><span data-stu-id="5ecee-201">Follow hello instructions below tooassign these permissions.</span></span>

    <span data-ttu-id="5ecee-202">a.</span><span class="sxs-lookup"><span data-stu-id="5ecee-202">a.</span></span> <span data-ttu-id="5ecee-203">No menu de navegação superior hello, clique em **instalação**, em seguida, clique em **Gerenciador de instalação**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-203">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="5ecee-205">b.</span><span class="sxs-lookup"><span data-stu-id="5ecee-205">b.</span></span> <span data-ttu-id="5ecee-206">No menu de navegação à esquerda do hello, selecione **usuários/funções**, em seguida, clique em **gerenciar funções**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-206">On hello left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="5ecee-208">c.</span><span class="sxs-lookup"><span data-stu-id="5ecee-208">c.</span></span> <span data-ttu-id="5ecee-209">Clique em **Nova Função**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-209">Click **New Role**.</span></span>

    <span data-ttu-id="5ecee-210">d.</span><span class="sxs-lookup"><span data-stu-id="5ecee-210">d.</span></span> <span data-ttu-id="5ecee-211">Digite um **nome** de nova função e selecione Olá **Single Sign-On somente** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="5ecee-211">Type in a **Name** for your new role, and select hello **Single Sign-On Only** checkbox.</span></span>
      
      ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="5ecee-213">e.</span><span class="sxs-lookup"><span data-stu-id="5ecee-213">e.</span></span> <span data-ttu-id="5ecee-214">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-214">Click **Save**.</span></span>

    <span data-ttu-id="5ecee-215">f.</span><span class="sxs-lookup"><span data-stu-id="5ecee-215">f.</span></span> <span data-ttu-id="5ecee-216">No menu de saudação na parte superior de saudação, clique em **permissões**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-216">In hello menu on hello top, click **Permissions**.</span></span> <span data-ttu-id="5ecee-217">Em seguida, clique em **Instalação**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-217">Then click **Setup**.</span></span>
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="5ecee-219">g.</span><span class="sxs-lookup"><span data-stu-id="5ecee-219">g.</span></span> <span data-ttu-id="5ecee-220">Selecione **Instalar o Logon Único do SAM** e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="5ecee-221">h.</span><span class="sxs-lookup"><span data-stu-id="5ecee-221">h.</span></span> <span data-ttu-id="5ecee-222">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-222">Click **Save**.</span></span>

    <span data-ttu-id="5ecee-223">i.</span><span class="sxs-lookup"><span data-stu-id="5ecee-223">i.</span></span> <span data-ttu-id="5ecee-224">No menu de navegação superior hello, clique em **instalação**, em seguida, clique em **Gerenciador de instalação**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-224">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="5ecee-226">j.</span><span class="sxs-lookup"><span data-stu-id="5ecee-226">j.</span></span> <span data-ttu-id="5ecee-227">No menu de navegação à esquerda do hello, selecione **usuários/funções**, em seguida, clique em **gerenciar usuários**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-227">On hello left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="5ecee-229">k.</span><span class="sxs-lookup"><span data-stu-id="5ecee-229">k.</span></span> <span data-ttu-id="5ecee-230">Selecione um usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="5ecee-230">Select a test user.</span></span> <span data-ttu-id="5ecee-231">Em seguida, clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-231">Then click **Edit**.</span></span>
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="5ecee-233">l.</span><span class="sxs-lookup"><span data-stu-id="5ecee-233">l.</span></span> <span data-ttu-id="5ecee-234">Na caixa de diálogo de funções hello, selecione função hello que você criou e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-234">On hello Roles dialog, select hello role that you have created and click **Add**.</span></span>
      
       ![Configurar Logon Único](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="5ecee-236">m.</span><span class="sxs-lookup"><span data-stu-id="5ecee-236">m.</span></span> <span data-ttu-id="5ecee-237">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="5ecee-238">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="5ecee-238">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5ecee-239">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="5ecee-239">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5ecee-240">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5ecee-240">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5ecee-241">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ecee-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="5ecee-242">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ecee-242">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="5ecee-244">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5ecee-244">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ecee-245">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5ecee-245">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="5ecee-247">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-247">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ecee-249">Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5ecee-249">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ecee-251">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ecee-251">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ecee-253">a.</span><span class="sxs-lookup"><span data-stu-id="5ecee-253">a.</span></span> <span data-ttu-id="5ecee-254">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-254">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ecee-255">b.</span><span class="sxs-lookup"><span data-stu-id="5ecee-255">b.</span></span> <span data-ttu-id="5ecee-256">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5ecee-256">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ecee-257">c.</span><span class="sxs-lookup"><span data-stu-id="5ecee-257">c.</span></span> <span data-ttu-id="5ecee-258">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-258">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5ecee-259">d.</span><span class="sxs-lookup"><span data-stu-id="5ecee-259">d.</span></span> <span data-ttu-id="5ecee-260">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="5ecee-261">Criando um usuário de teste do Netsuite</span><span class="sxs-lookup"><span data-stu-id="5ecee-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="5ecee-262">Nesta seção, um usuário chamado Brenda Fernandes é criado no Netsuite.</span><span class="sxs-lookup"><span data-stu-id="5ecee-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="5ecee-263">O Netsuite dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="5ecee-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="5ecee-264">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="5ecee-264">There is no action item for you in this section.</span></span> <span data-ttu-id="5ecee-265">Se um usuário não existir no Netsuite, um novo é criado quando você tenta tooaccess Netsuite.</span><span class="sxs-lookup"><span data-stu-id="5ecee-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt tooaccess Netsuite.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5ecee-266">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ecee-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5ecee-267">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="5ecee-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetsuite.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="5ecee-269">**tooassign Britta Simon tooNetsuite, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5ecee-269">**tooassign Britta Simon tooNetsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="5ecee-270">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5ecee-272">Na lista de aplicativos hello, selecione **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-272">In hello applications list, select **Netsuite**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="5ecee-274">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="5ecee-276">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-276">Click **Add** button.</span></span> <span data-ttu-id="5ecee-277">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5ecee-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="5ecee-279">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ecee-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5ecee-280">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5ecee-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ecee-281">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5ecee-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5ecee-282">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="5ecee-282">Testing single sign-on</span></span>

<span data-ttu-id="5ecee-283">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ecee-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5ecee-284">tootest seu único-configurações de logon, abra Olá painel de acesso em [https://myapps.microsoft.com](https://myapps.microsoft.com/), entre na conta de teste hello e clique em **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="5ecee-284">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into hello test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ecee-285">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5ecee-285">Additional resources</span></span>

* [<span data-ttu-id="5ecee-286">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5ecee-286">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ecee-287">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5ecee-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="5ecee-288">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="5ecee-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

