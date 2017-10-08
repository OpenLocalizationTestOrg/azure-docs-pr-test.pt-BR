---
title: "Tutorial: Integração do Azure Active Directory ao SAP Business ByDesign | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="dff61-103">Tutorial: integração do Azure Active Directory ao SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="dff61-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="dff61-104">Neste tutorial, você aprenderá como toointegrate SAP Business ByDesign com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="dff61-104">In this tutorial, you learn how toointegrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dff61-105">Integração do SAP Business ByDesign com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="dff61-105">Integrating SAP Business ByDesign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dff61-106">Você pode controlar no AD do Azure que tenha acesso tooSAP ByDesign de negócios.</span><span class="sxs-lookup"><span data-stu-id="dff61-106">You can control in Azure AD who has access tooSAP Business ByDesign.</span></span>
- <span data-ttu-id="dff61-107">Você pode habilitar seu usuários tooautomatically get conectado tooSAP ByDesign de negócios (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dff61-107">You can enable your users tooautomatically get signed-on tooSAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="dff61-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dff61-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="dff61-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dff61-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dff61-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dff61-110">Prerequisites</span></span>

<span data-ttu-id="dff61-111">tooconfigure integração do AD do Azure com o SAP Business ByDesign, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="dff61-111">tooconfigure Azure AD integration with SAP Business ByDesign, you need hello following items:</span></span>

- <span data-ttu-id="dff61-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="dff61-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dff61-113">Uma assinatura do SAP Business ByDesign habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="dff61-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dff61-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="dff61-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dff61-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="dff61-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dff61-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="dff61-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dff61-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dff61-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dff61-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="dff61-118">Scenario description</span></span>
<span data-ttu-id="dff61-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="dff61-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dff61-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="dff61-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dff61-121">Adicionando SAP Business ByDesign da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="dff61-121">Adding SAP Business ByDesign from hello gallery</span></span>
2. <span data-ttu-id="dff61-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="dff61-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a><span data-ttu-id="dff61-123">Adicionando SAP Business ByDesign da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="dff61-123">Adding SAP Business ByDesign from hello gallery</span></span>
<span data-ttu-id="dff61-124">integração de saudação tooconfigure do SAP Business ByDesign no AD do Azure, você precisa tooadd SAP Business ByDesign da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="dff61-124">tooconfigure hello integration of SAP Business ByDesign into Azure AD, you need tooadd SAP Business ByDesign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dff61-125">**tooadd SAP Business ByDesign da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="dff61-125">**tooadd SAP Business ByDesign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dff61-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="dff61-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="dff61-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="dff61-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dff61-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="dff61-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="dff61-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dff61-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="dff61-133">Na caixa de pesquisa hello, digite **SAP Business ByDesign**, selecione **SAP Business ByDesign** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="dff61-133">In hello search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button tooadd hello application.</span></span>

    ![SAP Business ByDesign na lista de resultados de saudação](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dff61-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dff61-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="dff61-136">Nesta seção, você configurará e testará o logon único do Azure AD com o SAP Business ByDesign, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="dff61-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dff61-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SAP Business ByDesign é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dff61-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Business ByDesign is tooa user in Azure AD.</span></span> <span data-ttu-id="dff61-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no SAP Business ByDesign precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="dff61-138">In other words, a link relationship between an Azure AD user and hello related user in SAP Business ByDesign needs toobe established.</span></span>

<span data-ttu-id="dff61-139">No SAP Business ByDesign, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="dff61-139">In SAP Business ByDesign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dff61-140">tooconfigure e teste de logon único do AD do Azure com o SAP Business ByDesign, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="dff61-140">tooconfigure and test Azure AD single sign-on with SAP Business ByDesign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dff61-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="dff61-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dff61-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dff61-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dff61-143">**[Criar um usuário de teste do SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**  -toohave um equivalente do Britta Simon no SAP Business ByDesign que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="dff61-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - toohave a counterpart of Britta Simon in SAP Business ByDesign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dff61-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="dff61-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dff61-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="dff61-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="dff61-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dff61-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="dff61-147">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="dff61-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="dff61-148">**tooconfigure logon único do AD do Azure com o SAP Business ByDesign, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="dff61-148">**tooconfigure Azure AD single sign-on with SAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="dff61-149">Em Olá portal do Azure, Olá **SAP Business ByDesign** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="dff61-149">In hello Azure portal, on hello **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="dff61-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="dff61-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="dff61-153">Em Olá **URLs e domínio do SAP Business ByDesign** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="dff61-153">On hello **SAP Business ByDesign Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="dff61-155">a.</span><span class="sxs-lookup"><span data-stu-id="dff61-155">a.</span></span> <span data-ttu-id="dff61-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="dff61-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="dff61-157">b.</span><span class="sxs-lookup"><span data-stu-id="dff61-157">b.</span></span> <span data-ttu-id="dff61-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="dff61-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dff61-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="dff61-159">These values are not real.</span></span> <span data-ttu-id="dff61-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="dff61-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dff61-161">Entre em contato com [equipe de suporte do cliente do SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="dff61-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooget these values.</span></span>

4. <span data-ttu-id="dff61-162">Em Olá **atributos de usuário** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="dff61-162">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![Seção Atributo do SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="dff61-164">a.</span><span class="sxs-lookup"><span data-stu-id="dff61-164">a.</span></span> <span data-ttu-id="dff61-165">Em **identificador de usuário** lista, selecione Olá **ExtractMailPrefix()** função.</span><span class="sxs-lookup"><span data-stu-id="dff61-165">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="dff61-166">b.</span><span class="sxs-lookup"><span data-stu-id="dff61-166">b.</span></span> <span data-ttu-id="dff61-167">De saudação **Mail** lista, selecione Olá usuário atributo que toouse para sua implementação.</span><span class="sxs-lookup"><span data-stu-id="dff61-167">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span> <span data-ttu-id="dff61-168">Por exemplo, se você quiser toouse Olá EmployeeID como identificador exclusivo do usuário e você armazenou o valor de atributo Olá Olá ExtensionAttribute2, selecione user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="dff61-168">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>   

5. <span data-ttu-id="dff61-169">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="dff61-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="dff61-171">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="dff61-171">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="dff61-173">Em Olá **configuração do SAP Business ByDesign** seção, clique em **configurar o SAP Business ByDesign** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="dff61-173">On hello **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dff61-174">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="dff61-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="dff61-176">tooget SSO configurado para o seu aplicativo executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="dff61-176">tooget SSO configured for your application, perform hello following steps:</span></span>
   
    <span data-ttu-id="dff61-177">a.</span><span class="sxs-lookup"><span data-stu-id="dff61-177">a.</span></span> <span data-ttu-id="dff61-178">Faça logon no portal do SAP Business ByDesign tooyour com direitos de administrador.</span><span class="sxs-lookup"><span data-stu-id="dff61-178">Sign on tooyour SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="dff61-179">b.</span><span class="sxs-lookup"><span data-stu-id="dff61-179">b.</span></span> <span data-ttu-id="dff61-180">Navegue muito**aplicativo e tarefas comuns de gerenciamento de usuário** e clique em Olá **provedor de identidade** guia.</span><span class="sxs-lookup"><span data-stu-id="dff61-180">Navigate too**Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="dff61-181">c.</span><span class="sxs-lookup"><span data-stu-id="dff61-181">c.</span></span> <span data-ttu-id="dff61-182">Clique em **novo provedor de identidade** e selecione Olá metadados XML que você baixou do portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="dff61-182">Click **New Identity Provider** and select hello metadata XML file that you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="dff61-183">Importando metadados hello, sistema Olá carrega automaticamente certificados de assinatura necessária hello e certificado de criptografia.</span><span class="sxs-lookup"><span data-stu-id="dff61-183">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="dff61-185">d.</span><span class="sxs-lookup"><span data-stu-id="dff61-185">d.</span></span> <span data-ttu-id="dff61-186">Olá tooinclude **URL do serviço de consumidor de declaração** na solicitação SAML hello, selecione **incluem URL de serviço de consumidor de declaração**.</span><span class="sxs-lookup"><span data-stu-id="dff61-186">tooinclude hello **Assertion Consumer Service URL** into hello SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="dff61-187">e.</span><span class="sxs-lookup"><span data-stu-id="dff61-187">e.</span></span> <span data-ttu-id="dff61-188">Clique em **Ativar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="dff61-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="dff61-189">f.</span><span class="sxs-lookup"><span data-stu-id="dff61-189">f.</span></span> <span data-ttu-id="dff61-190">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="dff61-190">Save your changes.</span></span>
   
    <span data-ttu-id="dff61-191">g.</span><span class="sxs-lookup"><span data-stu-id="dff61-191">g.</span></span> <span data-ttu-id="dff61-192">Clique em Olá **meu sistema** guia.</span><span class="sxs-lookup"><span data-stu-id="dff61-192">Click hello **My System** tab.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="dff61-194">h.</span><span class="sxs-lookup"><span data-stu-id="dff61-194">h.</span></span> <span data-ttu-id="dff61-195">Colar **Single Sign-On URL do serviço SAML**, que você tiver copiado da saudação portal do Azure para Olá **na URL de logon do AD do Azure** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="dff61-195">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal it into hello **Azure AD Sign On URL** textbox.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="dff61-197">i.</span><span class="sxs-lookup"><span data-stu-id="dff61-197">i.</span></span> <span data-ttu-id="dff61-198">Especificar se o funcionário Olá manualmente pode escolher entre fazer logon com a ID de usuário e senha ou SSO selecionando **seleção de provedor de identidade Manual**.</span><span class="sxs-lookup"><span data-stu-id="dff61-198">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="dff61-199">j.</span><span class="sxs-lookup"><span data-stu-id="dff61-199">j.</span></span> <span data-ttu-id="dff61-200">Em Olá **URL SSO** seção, especificar URL Olá que deve ser usado pelo sistema do hello funcionário toologon toohello.</span><span class="sxs-lookup"><span data-stu-id="dff61-200">In hello **SSO URL** section, specify hello URL that should be used by hello employee toologon toohello system.</span></span> 
    <span data-ttu-id="dff61-201">Olá URL enviado tooEmployee lista suspensa, você pode escolher entre Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="dff61-201">In hello URL Sent tooEmployee dropdown list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="dff61-202">**URL não SSO**</span><span class="sxs-lookup"><span data-stu-id="dff61-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="dff61-203">sistema de saudação envia somente saudação normal do sistema URL toohello funcionário.</span><span class="sxs-lookup"><span data-stu-id="dff61-203">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="dff61-204">Olá funcionário não pode fazer logon usando o SSO e deve usar senha ou certificado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="dff61-204">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="dff61-205">**URL de SSO**</span><span class="sxs-lookup"><span data-stu-id="dff61-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="dff61-206">sistema de saudação envia somente Olá URL SSO toohello funcionário.</span><span class="sxs-lookup"><span data-stu-id="dff61-206">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="dff61-207">funcionário Olá pode fazer logon usando o SSO.</span><span class="sxs-lookup"><span data-stu-id="dff61-207">hello employee can log on using SSO.</span></span> <span data-ttu-id="dff61-208">Solicitação de autenticação é redirecionada por meio de saudação IdP.</span><span class="sxs-lookup"><span data-stu-id="dff61-208">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="dff61-209">**Seleção Automática**</span><span class="sxs-lookup"><span data-stu-id="dff61-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="dff61-210">Se SSO não estiver ativo, o sistema de saudação envia funcionário de toohello de URL saudação normal do sistema.</span><span class="sxs-lookup"><span data-stu-id="dff61-210">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="dff61-211">Se o SSO estiver ativo, o sistema de Olá verifica se o funcionário Olá tem uma senha.</span><span class="sxs-lookup"><span data-stu-id="dff61-211">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="dff61-212">Se uma senha estiver disponível, a URL do SSO e URL do SSO não são enviadas toohello funcionário.</span><span class="sxs-lookup"><span data-stu-id="dff61-212">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="dff61-213">No entanto, se funcionário Olá não tem senha, Olá URL SSO é enviada toohello funcionário.</span><span class="sxs-lookup"><span data-stu-id="dff61-213">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="dff61-214">k.</span><span class="sxs-lookup"><span data-stu-id="dff61-214">k.</span></span> <span data-ttu-id="dff61-215">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="dff61-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="dff61-216">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="dff61-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dff61-217">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="dff61-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dff61-218">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dff61-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dff61-219">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dff61-219">Create an Azure AD test user</span></span>

<span data-ttu-id="dff61-220">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dff61-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="dff61-222">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="dff61-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dff61-223">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="dff61-223">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="dff61-225">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="dff61-225">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="dff61-227">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dff61-227">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="dff61-229">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="dff61-229">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="dff61-231">a.</span><span class="sxs-lookup"><span data-stu-id="dff61-231">a.</span></span> <span data-ttu-id="dff61-232">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dff61-232">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dff61-233">b.</span><span class="sxs-lookup"><span data-stu-id="dff61-233">b.</span></span> <span data-ttu-id="dff61-234">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dff61-234">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="dff61-235">c.</span><span class="sxs-lookup"><span data-stu-id="dff61-235">c.</span></span> <span data-ttu-id="dff61-236">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="dff61-236">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="dff61-237">d.</span><span class="sxs-lookup"><span data-stu-id="dff61-237">d.</span></span> <span data-ttu-id="dff61-238">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="dff61-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="dff61-239">Criar um usuário de teste do SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="dff61-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="dff61-240">Nesta seção, você criará uma usuária chamada Brenda Fernandes no SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="dff61-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="dff61-241">Trabalhe com [equipe de suporte do cliente do SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html) tooadd usuários de saudação na plataforma do SAP Business ByDesign hello.</span><span class="sxs-lookup"><span data-stu-id="dff61-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello users in hello SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="dff61-242">Certifique-se de que o valor de NameID deve corresponder com o campo de nome de usuário de saudação na plataforma do SAP Business ByDesign hello.</span><span class="sxs-lookup"><span data-stu-id="dff61-242">Please make sure that NameID value should match with hello username field in hello SAP Business ByDesign platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="dff61-243">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="dff61-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="dff61-244">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSAP ByDesign de negócios.</span><span class="sxs-lookup"><span data-stu-id="dff61-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Business ByDesign.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="dff61-246">**tooassign Britta Simon tooSAP ByDesign Business, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="dff61-246">**tooassign Britta Simon tooSAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="dff61-247">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="dff61-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="dff61-249">Na lista de aplicativos hello, selecione **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="dff61-249">In hello applications list, select **SAP Business ByDesign**.</span></span>

    ![link do SAP Business ByDesign Olá na lista de aplicativos Olá](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="dff61-251">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="dff61-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="dff61-253">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dff61-253">Click **Add** button.</span></span> <span data-ttu-id="dff61-254">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dff61-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="dff61-256">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="dff61-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dff61-257">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dff61-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dff61-258">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dff61-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="dff61-259">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="dff61-259">Test single sign-on</span></span>

<span data-ttu-id="dff61-260">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="dff61-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dff61-261">Quando você clica em bloco SAP Business ByDesign Olá Olá painel de acesso, você deve obter aplicativos do SAP Business ByDesign automaticamente assinado em tooyour.</span><span class="sxs-lookup"><span data-stu-id="dff61-261">When you click hello SAP Business ByDesign tile in hello Access Panel, you should get automatically signed-on tooyour SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dff61-262">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="dff61-262">Additional resources</span></span>

* [<span data-ttu-id="dff61-263">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="dff61-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dff61-264">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dff61-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

