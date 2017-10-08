---
title: "Tutorial: integração do Azure Active Directory com o Workpath | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Workpath."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 69f443f314edb7c8c489a6c193e09b6f8fe6795a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="92c71-103">Tutorial: integração do Azure Active Directory com o Workpath</span><span class="sxs-lookup"><span data-stu-id="92c71-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="92c71-104">Neste tutorial, você aprenderá como toointegrate Workpath com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="92c71-104">In this tutorial, you learn how toointegrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92c71-105">Integrando Workpath com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="92c71-105">Integrating Workpath with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="92c71-106">Você pode controlar no AD do Azure que tenha acesso tooWorkpath</span><span class="sxs-lookup"><span data-stu-id="92c71-106">You can control in Azure AD who has access tooWorkpath</span></span>
- <span data-ttu-id="92c71-107">Você pode habilitar seu usuários tooautomatically get conectado tooWorkpath (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="92c71-107">You can enable your users tooautomatically get signed-on tooWorkpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92c71-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="92c71-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="92c71-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92c71-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92c71-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="92c71-110">Prerequisites</span></span>

<span data-ttu-id="92c71-111">tooconfigure integração do AD do Azure com Workpath, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="92c71-111">tooconfigure Azure AD integration with Workpath, you need hello following items:</span></span>

- <span data-ttu-id="92c71-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="92c71-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92c71-113">Uma assinatura do Workpath com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="92c71-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92c71-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="92c71-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92c71-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="92c71-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92c71-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="92c71-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92c71-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92c71-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92c71-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="92c71-118">Scenario description</span></span>
<span data-ttu-id="92c71-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="92c71-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92c71-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="92c71-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92c71-121">Adicionando Workpath da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="92c71-121">Adding Workpath from hello gallery</span></span>
2. <span data-ttu-id="92c71-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="92c71-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-hello-gallery"></a><span data-ttu-id="92c71-123">Adicionando Workpath da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="92c71-123">Adding Workpath from hello gallery</span></span>
<span data-ttu-id="92c71-124">integração de saudação tooconfigure de Workpath no AD do Azure, você precisa tooadd Workpath da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="92c71-124">tooconfigure hello integration of Workpath into Azure AD, you need tooadd Workpath from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="92c71-125">**tooadd Workpath da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="92c71-125">**tooadd Workpath from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="92c71-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="92c71-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92c71-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="92c71-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="92c71-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="92c71-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="92c71-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92c71-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="92c71-133">Na caixa de pesquisa hello, digite **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="92c71-133">In hello search box, type **Workpath**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="92c71-135">No painel de resultados de saudação, selecione **Workpath**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="92c71-135">In hello results panel, select **Workpath**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92c71-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="92c71-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92c71-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Workpath, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="92c71-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="92c71-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Workpath é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="92c71-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workpath is tooa user in Azure AD.</span></span> <span data-ttu-id="92c71-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Workpath precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="92c71-140">In other words, a link relationship between an Azure AD user and hello related user in Workpath needs toobe established.</span></span>

<span data-ttu-id="92c71-141">Workpath, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="92c71-141">In Workpath, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="92c71-142">tooconfigure e teste de logon único do AD do Azure com Workpath, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="92c71-142">tooconfigure and test Azure AD single sign-on with Workpath, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="92c71-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="92c71-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="92c71-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92c71-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92c71-145">**[Criar um usuário de teste Workpath](#creating-a-workpath-test-user)**  -toohave um equivalente do Britta Simon em Workpath é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="92c71-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - toohave a counterpart of Britta Simon in Workpath that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="92c71-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="92c71-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92c71-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="92c71-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92c71-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="92c71-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92c71-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Workpath.</span><span class="sxs-lookup"><span data-stu-id="92c71-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="92c71-150">**tooconfigure AD do Azure-logon único com Workpath, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="92c71-150">**tooconfigure Azure AD single sign-on with Workpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="92c71-151">Em Olá portal do Azure, Olá **Workpath** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="92c71-151">In hello Azure portal, on hello **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="92c71-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="92c71-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="92c71-155">Em Olá **Workpath domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="92c71-155">On hello **Workpath Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="92c71-157">a.</span><span class="sxs-lookup"><span data-stu-id="92c71-157">a.</span></span> <span data-ttu-id="92c71-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="92c71-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="92c71-159">b.</span><span class="sxs-lookup"><span data-stu-id="92c71-159">b.</span></span> <span data-ttu-id="92c71-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://api.workpath.com/v1/saml/assert/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="92c71-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="92c71-161">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="92c71-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="92c71-162">Se desejar que o aplicativo hello tooconfigure **SP** iniciada modo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="92c71-162">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="92c71-164">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="92c71-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92c71-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="92c71-165">These values are not real.</span></span> <span data-ttu-id="92c71-166">Atualize esses valores com URL de logon real hello, identificador e URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="92c71-166">Update these values with hello actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="92c71-167">Entre em contato com [Workpath a equipe de suporte](https://help.workpath.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="92c71-167">Contact [Workpath support team](https://help.workpath.com) tooget these values.</span></span>

5. <span data-ttu-id="92c71-168">Aplicativo de Workpath espera asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="92c71-168">Workpath application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="92c71-169">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="92c71-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="92c71-170">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92c71-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="92c71-171">Olá captura de tela a seguir mostra um exemplo para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="92c71-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="92c71-173">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="92c71-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="92c71-174">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="92c71-174">Attribute Name</span></span> | <span data-ttu-id="92c71-175">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="92c71-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="92c71-176">first_name</span><span class="sxs-lookup"><span data-stu-id="92c71-176">first_name</span></span> | <span data-ttu-id="92c71-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="92c71-177">user.givenname</span></span> |
    | <span data-ttu-id="92c71-178">last_name</span><span class="sxs-lookup"><span data-stu-id="92c71-178">last_name</span></span> | <span data-ttu-id="92c71-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="92c71-179">user.surname</span></span> |
    
    <span data-ttu-id="92c71-180">a.</span><span class="sxs-lookup"><span data-stu-id="92c71-180">a.</span></span> <span data-ttu-id="92c71-181">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92c71-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="92c71-183">b.</span><span class="sxs-lookup"><span data-stu-id="92c71-183">b.</span></span> <span data-ttu-id="92c71-184">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="92c71-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="92c71-186">c.</span><span class="sxs-lookup"><span data-stu-id="92c71-186">c.</span></span> <span data-ttu-id="92c71-187">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="92c71-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="92c71-188">d.</span><span class="sxs-lookup"><span data-stu-id="92c71-188">d.</span></span> <span data-ttu-id="92c71-189">Deixe Olá **Namespace** caixa de texto em branco.</span><span class="sxs-lookup"><span data-stu-id="92c71-189">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="92c71-190">e.</span><span class="sxs-lookup"><span data-stu-id="92c71-190">e.</span></span> <span data-ttu-id="92c71-191">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="92c71-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="92c71-192">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="92c71-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="92c71-194">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="92c71-194">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="92c71-196">Em Olá **Workpath configuração** seção, clique em **configurar Workpath** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="92c71-196">On hello **Workpath Configuration** section, click **Configure Workpath** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="92c71-197">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="92c71-197">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="92c71-199">tooconfigure logon único no **Workpath** lado, você precisa toosend Olá baixado **Metadata XML**, **URL de logout, ID de entidade de SAML e SAML Single Sign-On URL do serviço** muito[a equipe de suporte Workpath](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="92c71-199">tooconfigure single sign-on on **Workpath** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="92c71-200">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="92c71-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="92c71-201">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="92c71-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="92c71-202">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92c71-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92c71-203">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="92c71-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="92c71-204">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="92c71-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="92c71-206">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="92c71-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="92c71-207">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="92c71-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92c71-209">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="92c71-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92c71-211">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="92c71-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92c71-213">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="92c71-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92c71-215">a.</span><span class="sxs-lookup"><span data-stu-id="92c71-215">a.</span></span> <span data-ttu-id="92c71-216">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92c71-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92c71-217">b.</span><span class="sxs-lookup"><span data-stu-id="92c71-217">b.</span></span> <span data-ttu-id="92c71-218">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="92c71-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92c71-219">c.</span><span class="sxs-lookup"><span data-stu-id="92c71-219">c.</span></span> <span data-ttu-id="92c71-220">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="92c71-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="92c71-221">d.</span><span class="sxs-lookup"><span data-stu-id="92c71-221">d.</span></span> <span data-ttu-id="92c71-222">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="92c71-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="92c71-223">Criar um usuário de teste do Workpath</span><span class="sxs-lookup"><span data-stu-id="92c71-223">Creating a Workpath test user</span></span>

<span data-ttu-id="92c71-224">O Workpath dá suporte ao provisionamento de usuário just in time.</span><span class="sxs-lookup"><span data-stu-id="92c71-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="92c71-225">Após a autenticação de usuários são criados no aplicativo hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="92c71-225">After authentication users are created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="92c71-226">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="92c71-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="92c71-227">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWorkpath.</span><span class="sxs-lookup"><span data-stu-id="92c71-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkpath.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="92c71-229">**tooassign Britta Simon tooWorkpath, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="92c71-229">**tooassign Britta Simon tooWorkpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="92c71-230">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="92c71-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="92c71-232">Na lista de aplicativos hello, selecione **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="92c71-232">In hello applications list, select **Workpath**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="92c71-234">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="92c71-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="92c71-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="92c71-236">Click **Add** button.</span></span> <span data-ttu-id="92c71-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92c71-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="92c71-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="92c71-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="92c71-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92c71-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92c71-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92c71-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92c71-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="92c71-242">Testing single sign-on</span></span>

<span data-ttu-id="92c71-243">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="92c71-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="92c71-244">Quando você clica em bloco Workpath Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Workpath aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92c71-244">When you click hello Workpath tile in hello Access Panel, you should get automatically signed-on tooyour Workpath application.</span></span>
<span data-ttu-id="92c71-245">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92c71-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92c71-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="92c71-246">Additional resources</span></span>

* [<span data-ttu-id="92c71-247">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="92c71-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92c71-248">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92c71-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

