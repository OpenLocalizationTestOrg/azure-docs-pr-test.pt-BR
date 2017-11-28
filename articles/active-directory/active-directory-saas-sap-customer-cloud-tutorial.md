---
title: "Tutorial: integração do Azure Active Directory ao SAP Cloud for Customer | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e a nuvem do SAP para o cliente."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="39566-103">Tutorial: integração do Azure Active Directory ao SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="39566-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="39566-104">Neste tutorial, você aprenderá como toointegrate SAP nuvem para o cliente com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="39566-104">In this tutorial, you learn how toointegrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="39566-105">Integração de nuvem do SAP para o cliente com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="39566-105">Integrating SAP Cloud for Customer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="39566-106">Você pode controlar no AD do Azure que tenha acesso tooSAP nuvem para o cliente</span><span class="sxs-lookup"><span data-stu-id="39566-106">You can control in Azure AD who has access tooSAP Cloud for Customer</span></span>
- <span data-ttu-id="39566-107">Você pode habilitar seu usuários tooautomatically get conectado tooSAP nuvem para o cliente (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="39566-107">You can enable your users tooautomatically get signed-on tooSAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="39566-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="39566-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="39566-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="39566-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39566-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="39566-110">Prerequisites</span></span>

<span data-ttu-id="39566-111">tooconfigure integração do AD do Azure com a nuvem do SAP para o cliente, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="39566-111">tooconfigure Azure AD integration with SAP Cloud for Customer, you need hello following items:</span></span>

- <span data-ttu-id="39566-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="39566-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39566-113">Uma assinatura habilitada para logon único do SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="39566-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="39566-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="39566-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="39566-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="39566-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="39566-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="39566-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="39566-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39566-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39566-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="39566-118">Scenario description</span></span>
<span data-ttu-id="39566-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="39566-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="39566-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="39566-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39566-121">Adicionando nuvem SAP para o cliente da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="39566-121">Adding SAP Cloud for Customer from hello gallery</span></span>
2. <span data-ttu-id="39566-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="39566-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a><span data-ttu-id="39566-123">Adicionando nuvem SAP para o cliente da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="39566-123">Adding SAP Cloud for Customer from hello gallery</span></span>
<span data-ttu-id="39566-124">integração de saudação tooconfigure da nuvem do SAP para o cliente no AD do Azure, você precisa tooadd nuvem SAP para cliente da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="39566-124">tooconfigure hello integration of SAP Cloud for Customer into Azure AD, you need tooadd SAP Cloud for Customer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="39566-125">**tooadd nuvem SAP para o cliente da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="39566-125">**tooadd SAP Cloud for Customer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="39566-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="39566-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="39566-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="39566-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="39566-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="39566-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="39566-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="39566-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="39566-133">Na caixa de pesquisa hello, digite **nuvem SAP para o cliente**.</span><span class="sxs-lookup"><span data-stu-id="39566-133">In hello search box, type **SAP Cloud for Customer**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="39566-135">No painel de resultados de saudação, selecione **nuvem SAP para o cliente**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="39566-135">In hello results panel, select **SAP Cloud for Customer**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="39566-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="39566-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="39566-138">Nesta seção, você configurará e testará o logon único do Azure AD com o SAP Cloud for Customer, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="39566-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="39566-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na nuvem do SAP para o cliente é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="39566-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Cloud for Customer is tooa user in Azure AD.</span></span> <span data-ttu-id="39566-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na nuvem do SAP para o cliente precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="39566-140">In other words, a link relationship between an Azure AD user and hello related user in SAP Cloud for Customer needs toobe established.</span></span>

<span data-ttu-id="39566-141">Na nuvem do SAP para o cliente, atribua o valor de saudação de Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="39566-141">In SAP Cloud for Customer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="39566-142">tooconfigure e teste de logon único do AD do Azure com a nuvem do SAP para o cliente, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="39566-142">tooconfigure and test Azure AD single sign-on with SAP Cloud for Customer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="39566-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="39566-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="39566-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39566-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="39566-145">**[Criando uma nuvem do SAP para o usuário de teste do cliente](#creating-a-sap-cloud-for-customer-test-user)**  -toohave um equivalente do Britta Simon na nuvem do SAP para o cliente que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="39566-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - toohave a counterpart of Britta Simon in SAP Cloud for Customer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="39566-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="39566-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="39566-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="39566-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="39566-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="39566-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="39566-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em sua nuvem do SAP para o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="39566-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="39566-150">**tooconfigure logon único do AD do Azure com a nuvem do SAP para o cliente, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="39566-150">**tooconfigure Azure AD single sign-on with SAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="39566-151">Em Olá portal do Azure, Olá **nuvem SAP para o cliente** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="39566-151">In hello Azure portal, on hello **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="39566-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="39566-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="39566-155">Em Olá **nuvem SAP para o domínio de cliente e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="39566-155">On hello **SAP Cloud for Customer Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="39566-157">a.</span><span class="sxs-lookup"><span data-stu-id="39566-157">a.</span></span> <span data-ttu-id="39566-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="39566-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="39566-159">b.</span><span class="sxs-lookup"><span data-stu-id="39566-159">b.</span></span> <span data-ttu-id="39566-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="39566-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="39566-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="39566-161">These values are not real.</span></span> <span data-ttu-id="39566-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="39566-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="39566-163">Entre em contato com [SAP nuvem para a equipe de suporte do cliente do cliente](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="39566-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget these values.</span></span> 

4. <span data-ttu-id="39566-164">Em Olá **atributos de usuário** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="39566-164">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="39566-166">a.</span><span class="sxs-lookup"><span data-stu-id="39566-166">a.</span></span> <span data-ttu-id="39566-167">Em **identificador de usuário** lista, selecione Olá **ExtractMailPrefix()** função.</span><span class="sxs-lookup"><span data-stu-id="39566-167">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="39566-168">b.</span><span class="sxs-lookup"><span data-stu-id="39566-168">b.</span></span> <span data-ttu-id="39566-169">De saudação **Mail** lista, selecione Olá usuário atributo que toouse para sua implementação.</span><span class="sxs-lookup"><span data-stu-id="39566-169">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="39566-170">Por exemplo, se você quiser toouse Olá EmployeeID como identificador exclusivo do usuário e você armazenou o valor de atributo Olá Olá ExtensionAttribute2, selecione user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="39566-170">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="39566-171">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="39566-171">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="39566-173">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="39566-173">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="39566-175">Em Olá **nuvem SAP para configuração de cliente** seção, clique em **configurar nuvem do SAP para o cliente** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="39566-175">On hello **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="39566-176">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="39566-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="39566-178">tooget SSO configurado, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="39566-178">tooget SSO configured, perform hello following steps:</span></span>
   
    <span data-ttu-id="39566-179">a.</span><span class="sxs-lookup"><span data-stu-id="39566-179">a.</span></span> <span data-ttu-id="39566-180">Faça logon no portal do SAP Cloud for Customer com direitos de administrador.</span><span class="sxs-lookup"><span data-stu-id="39566-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="39566-181">b.</span><span class="sxs-lookup"><span data-stu-id="39566-181">b.</span></span> <span data-ttu-id="39566-182">Navegue toohello **aplicativo e tarefas comuns de gerenciamento de usuário** e clique em Olá **provedor de identidade** guia.</span><span class="sxs-lookup"><span data-stu-id="39566-182">Navigate toohello **Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="39566-183">c.</span><span class="sxs-lookup"><span data-stu-id="39566-183">c.</span></span> <span data-ttu-id="39566-184">Clique em **novo provedor de identidade** e um arquivo XML de metadados Olá select que baixou do portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="39566-184">Click **New Identity Provider** and select hello metadata XML file you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="39566-185">Importando metadados hello, sistema Olá carrega automaticamente certificados de assinatura necessária hello e certificado de criptografia.</span><span class="sxs-lookup"><span data-stu-id="39566-185">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="39566-187">d.</span><span class="sxs-lookup"><span data-stu-id="39566-187">d.</span></span> <span data-ttu-id="39566-188">Active Directory do Azure requer URL do serviço de consumidor de declaração de elemento de saudação na solicitação SAML hello, então selecione Olá **URL do serviço de consumidor asserção incluem** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="39566-188">Azure Active Directory requires hello element Assertion Consumer Service URL in hello SAML request, so select hello **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="39566-189">e.</span><span class="sxs-lookup"><span data-stu-id="39566-189">e.</span></span> <span data-ttu-id="39566-190">Clique em **Ativar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="39566-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="39566-191">f.</span><span class="sxs-lookup"><span data-stu-id="39566-191">f.</span></span> <span data-ttu-id="39566-192">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="39566-192">Save your changes.</span></span>
   
    <span data-ttu-id="39566-193">g.</span><span class="sxs-lookup"><span data-stu-id="39566-193">g.</span></span> <span data-ttu-id="39566-194">Clique em Olá **meu sistema** guia.</span><span class="sxs-lookup"><span data-stu-id="39566-194">Click hello **My System** tab.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="39566-196">h.</span><span class="sxs-lookup"><span data-stu-id="39566-196">h.</span></span> <span data-ttu-id="39566-197">Na caixa de texto **URL de Logon do Azure AD**, cole a **URL do Serviço de Logon Único SAML** copiada do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="39566-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="39566-199">i.</span><span class="sxs-lookup"><span data-stu-id="39566-199">i.</span></span> <span data-ttu-id="39566-200">Especificar se o funcionário Olá manualmente pode escolher entre fazer logon com a ID de usuário e senha ou SSO selecionando Olá **seleção de provedor de identidade Manual**.</span><span class="sxs-lookup"><span data-stu-id="39566-200">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting hello **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="39566-201">j.</span><span class="sxs-lookup"><span data-stu-id="39566-201">j.</span></span> <span data-ttu-id="39566-202">Em Olá **URL SSO** seção, especificar URL de saudação que deve ser usada por seu toosign funcionários no sistema toohello.</span><span class="sxs-lookup"><span data-stu-id="39566-202">In hello **SSO URL** section, specify hello URL that should be used by your employees toosign on toohello system.</span></span> 
    <span data-ttu-id="39566-203">Em Olá **tooEmployee URL enviado** lista, você pode escolher entre hello as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="39566-203">In hello **URL Sent tooEmployee** list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="39566-204">**URL não SSO**</span><span class="sxs-lookup"><span data-stu-id="39566-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="39566-205">sistema de saudação envia somente saudação normal do sistema URL toohello funcionário.</span><span class="sxs-lookup"><span data-stu-id="39566-205">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="39566-206">Olá funcionário não pode fazer logon usando o SSO e deve usar senha ou certificado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="39566-206">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="39566-207">**URL de SSO**</span><span class="sxs-lookup"><span data-stu-id="39566-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="39566-208">sistema de saudação envia somente Olá URL SSO toohello funcionário.</span><span class="sxs-lookup"><span data-stu-id="39566-208">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="39566-209">funcionário Olá pode fazer logon usando o SSO.</span><span class="sxs-lookup"><span data-stu-id="39566-209">hello employee can log on using SSO.</span></span> <span data-ttu-id="39566-210">Solicitação de autenticação é redirecionada por meio de saudação IdP.</span><span class="sxs-lookup"><span data-stu-id="39566-210">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="39566-211">**Seleção Automática**</span><span class="sxs-lookup"><span data-stu-id="39566-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="39566-212">Se SSO não estiver ativo, o sistema de saudação envia funcionário de toohello de URL saudação normal do sistema.</span><span class="sxs-lookup"><span data-stu-id="39566-212">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="39566-213">Se o SSO estiver ativo, o sistema de Olá verifica se o funcionário Olá tem uma senha.</span><span class="sxs-lookup"><span data-stu-id="39566-213">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="39566-214">Se uma senha estiver disponível, a URL do SSO e URL do SSO não são enviadas toohello funcionário.</span><span class="sxs-lookup"><span data-stu-id="39566-214">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="39566-215">No entanto, se funcionário Olá não tem senha, Olá URL SSO é enviada toohello funcionário.</span><span class="sxs-lookup"><span data-stu-id="39566-215">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="39566-216">k.</span><span class="sxs-lookup"><span data-stu-id="39566-216">k.</span></span> <span data-ttu-id="39566-217">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="39566-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="39566-218">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="39566-218">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="39566-219">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="39566-219">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="39566-220">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="39566-220">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="39566-221">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="39566-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="39566-222">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="39566-222">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="39566-224">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="39566-224">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="39566-225">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="39566-225">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="39566-227">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="39566-227">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="39566-229">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="39566-229">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="39566-231">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="39566-231">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="39566-233">a.</span><span class="sxs-lookup"><span data-stu-id="39566-233">a.</span></span> <span data-ttu-id="39566-234">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39566-234">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="39566-235">b.</span><span class="sxs-lookup"><span data-stu-id="39566-235">b.</span></span> <span data-ttu-id="39566-236">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="39566-236">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="39566-237">c.</span><span class="sxs-lookup"><span data-stu-id="39566-237">c.</span></span> <span data-ttu-id="39566-238">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="39566-238">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="39566-239">d.</span><span class="sxs-lookup"><span data-stu-id="39566-239">d.</span></span> <span data-ttu-id="39566-240">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="39566-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="39566-241">Criando um usuário de teste do SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="39566-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="39566-242">Nesta seção, você criará uma usuária chamada Brenda Fernandes no SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="39566-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="39566-243">Trabalhe com [SAP nuvem para a equipe de suporte do cliente](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd usuários Olá Olá SAP nuvem para a plataforma de cliente.</span><span class="sxs-lookup"><span data-stu-id="39566-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd hello users in hello SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="39566-244">Certifique-se de que o valor de NameID deve corresponder com campo de nome de usuário Olá Olá SAP nuvem para a plataforma de cliente.</span><span class="sxs-lookup"><span data-stu-id="39566-244">Please make sure that NameID value should match with hello username field in hello SAP Cloud for Customer platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="39566-245">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="39566-245">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="39566-246">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSAP nuvem para o cliente.</span><span class="sxs-lookup"><span data-stu-id="39566-246">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Cloud for Customer.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="39566-248">**tooassign Britta Simon tooSAP nuvem para o cliente, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="39566-248">**tooassign Britta Simon tooSAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="39566-249">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="39566-249">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="39566-251">Na lista de aplicativos hello, selecione **nuvem SAP para o cliente**.</span><span class="sxs-lookup"><span data-stu-id="39566-251">In hello applications list, select **SAP Cloud for Customer**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="39566-253">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="39566-253">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="39566-255">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="39566-255">Click **Add** button.</span></span> <span data-ttu-id="39566-256">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="39566-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="39566-258">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="39566-258">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="39566-259">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="39566-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="39566-260">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="39566-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="39566-261">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="39566-261">Testing single sign-on</span></span>

<span data-ttu-id="39566-262">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="39566-262">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="39566-263">Quando você clica em hello nuvem SAP para o bloco de cliente no painel de acesso de saudação, você deve obter tooyour automaticamente conectado em nuvem do SAP para o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="39566-263">When you click hello SAP Cloud for Customer tile in hello Access Panel, you should get automatically signed-on tooyour SAP Cloud for Customer application.</span></span>
<span data-ttu-id="39566-264">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="39566-264">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39566-265">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="39566-265">Additional resources</span></span>

* [<span data-ttu-id="39566-266">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="39566-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="39566-267">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="39566-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

