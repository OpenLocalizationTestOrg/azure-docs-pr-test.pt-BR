---
title: "Tutorial: Integração do Azure Active Directory com o Qlik Sense Enterprise | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Qlik sentido Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="048b8-103">Tutorial: integração do Azure Active Directory ao Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="048b8-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="048b8-104">Neste tutorial, você aprenderá como toointegrate Qlik sentido Enterprise com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="048b8-104">In this tutorial, you learn how toointegrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="048b8-105">Integrando Qlik sentido Enterprise com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="048b8-105">Integrating Qlik Sense Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="048b8-106">Você pode controlar no AD do Azure que tenha acesso tooQlik sentido Enterprise.</span><span class="sxs-lookup"><span data-stu-id="048b8-106">You can control in Azure AD who has access tooQlik Sense Enterprise.</span></span>
- <span data-ttu-id="048b8-107">Você pode habilitar seu usuários tooautomatically get conectado tooQlik sentido Enterprise (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="048b8-107">You can enable your users tooautomatically get signed-on tooQlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="048b8-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="048b8-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="048b8-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="048b8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="048b8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="048b8-110">Prerequisites</span></span>

<span data-ttu-id="048b8-111">tooconfigure integração do AD do Azure com Qlik sentido Enterprise, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="048b8-111">tooconfigure Azure AD integration with Qlik Sense Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="048b8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="048b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="048b8-113">Uma assinatura do Qlik Sense Enterprise habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="048b8-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="048b8-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="048b8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="048b8-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="048b8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="048b8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="048b8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="048b8-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="048b8-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="048b8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="048b8-118">Scenario description</span></span>
<span data-ttu-id="048b8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="048b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="048b8-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="048b8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="048b8-121">Adicionando Qlik sentido Enterprise na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="048b8-121">Adding Qlik Sense Enterprise from hello gallery</span></span>
2. <span data-ttu-id="048b8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="048b8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a><span data-ttu-id="048b8-123">Adicionando Qlik sentido Enterprise na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="048b8-123">Adding Qlik Sense Enterprise from hello gallery</span></span>
<span data-ttu-id="048b8-124">integração de saudação tooconfigure do Qlik sentido corporativo no AD do Azure, você precisa tooadd Qlik sentido Enterprise na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="048b8-124">tooconfigure hello integration of Qlik Sense Enterprise into Azure AD, you need tooadd Qlik Sense Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="048b8-125">**tooadd Qlik sentido Enterprise na Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="048b8-125">**tooadd Qlik Sense Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="048b8-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="048b8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="048b8-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="048b8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="048b8-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="048b8-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="048b8-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="048b8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="048b8-133">Na caixa de pesquisa hello, digite **Qlik sentido Enterprise**, selecione **Qlik sentido Enterprise** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="048b8-133">In hello search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Qlik sentido Enterprise na lista de resultados de saudação](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="048b8-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="048b8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="048b8-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Qlik Sense Enterprise, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="048b8-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="048b8-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá Qlik sentido empresa é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="048b8-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Qlik Sense Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="048b8-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação Qlik sentido empresa precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="048b8-138">In other words, a link relationship between an Azure AD user and hello related user in Qlik Sense Enterprise needs toobe established.</span></span>

<span data-ttu-id="048b8-139">Qlik sentido Enterprise, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="048b8-139">In Qlik Sense Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="048b8-140">tooconfigure e teste de logon único do AD do Azure com Qlik sentido Enterprise, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="048b8-140">tooconfigure and test Azure AD single sign-on with Qlik Sense Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="048b8-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="048b8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="048b8-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="048b8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="048b8-143">**[Criar um usuário de teste Qlik sentido Enterprise](#create-a-qlik-sense-enterprise-test-user)**  -toohave um equivalente de Britta Simon Qlik sentido empresa que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="048b8-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - toohave a counterpart of Britta Simon in Qlik Sense Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="048b8-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="048b8-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="048b8-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="048b8-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="048b8-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="048b8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="048b8-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Qlik sentido Enterprise.</span><span class="sxs-lookup"><span data-stu-id="048b8-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="048b8-148">**tooconfigure logon único do AD do Azure com Qlik sentido Enterprise, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="048b8-148">**tooconfigure Azure AD single sign-on with Qlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="048b8-149">Em Olá portal do Azure, Olá **Qlik sentido Enterprise** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="048b8-149">In hello Azure portal, on hello **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="048b8-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="048b8-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="048b8-153">Em Olá **URLs e domínio da empresa sentido Qlik** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="048b8-153">On hello **Qlik Sense Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="048b8-155">a.</span><span class="sxs-lookup"><span data-stu-id="048b8-155">a.</span></span> <span data-ttu-id="048b8-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="048b8-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="048b8-157">Observe Olá barra no final da saudação desse URI à direita.</span><span class="sxs-lookup"><span data-stu-id="048b8-157">Note hello trailing slash at hello end of this URI.</span></span> <span data-ttu-id="048b8-158">Ela é necessária.</span><span class="sxs-lookup"><span data-stu-id="048b8-158">It is required.</span></span>
    
    <span data-ttu-id="048b8-159">b.</span><span class="sxs-lookup"><span data-stu-id="048b8-159">b.</span></span> <span data-ttu-id="048b8-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="048b8-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="048b8-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="048b8-161">These values are not real.</span></span> <span data-ttu-id="048b8-162">Atualizar esses valores com hello real URL de logon e o identificador que estão descritas mais adiante neste tutorial ou entre em contato com [a equipe de suporte Qlik sentido Enterprise Client](https://www.qlik.com/us/services/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="048b8-162">Update these values with hello actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="048b8-163">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="048b8-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="048b8-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="048b8-165">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="048b8-167">Prepare o arquivo de XML de metadados de federação de saudação para que você pode carregar servidor tooQlik sentido.</span><span class="sxs-lookup"><span data-stu-id="048b8-167">Prepare hello Federation Metadata XML file so that you can upload that tooQlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="048b8-168">Antes de carregar Olá IdP metadados toohello server Qlik sentido, o arquivo hello precisa toobe editado tooremove informações tooensure funcionamento entre o AD do Azure e o servidor Qlik sentido.</span><span class="sxs-lookup"><span data-stu-id="048b8-168">Before uploading hello IdP metadata toohello Qlik Sense server, hello file needs toobe edited tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="048b8-170">a.</span><span class="sxs-lookup"><span data-stu-id="048b8-170">a.</span></span> <span data-ttu-id="048b8-171">Abra o arquivo de FederationMetaData.xml de saudação, que você baixou do portal do Azure em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="048b8-171">Open hello FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="048b8-172">b.</span><span class="sxs-lookup"><span data-stu-id="048b8-172">b.</span></span> <span data-ttu-id="048b8-173">Procure o valor de saudação **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="048b8-173">Search for hello value **RoleDescriptor**.</span></span>  <span data-ttu-id="048b8-174">Há quatro entradas (dois pares de marcas de elemento de abertura e fechamento).</span><span class="sxs-lookup"><span data-stu-id="048b8-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="048b8-175">c.</span><span class="sxs-lookup"><span data-stu-id="048b8-175">c.</span></span> <span data-ttu-id="048b8-176">Exclua marcas de RoleDescriptor hello e todas as informações do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="048b8-176">Delete hello RoleDescriptor tags and all information in between from hello file.</span></span>
   
    <span data-ttu-id="048b8-177">d.</span><span class="sxs-lookup"><span data-stu-id="048b8-177">d.</span></span> <span data-ttu-id="048b8-178">Salve o arquivo hello e mantê-lo nas proximidades para uso neste documento.</span><span class="sxs-lookup"><span data-stu-id="048b8-178">Save hello file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="048b8-179">Navegue toohello Qlik sentido Qlik Management Console (QMC) como um usuário que pode criar configurações de proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="048b8-179">Navigate toohello Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="048b8-180">No hello QMC, clique em Olá **Virtual Proxies** item de menu.</span><span class="sxs-lookup"><span data-stu-id="048b8-180">In hello QMC, click on hello **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="048b8-182">Na parte inferior de saudação da tela hello, clique em Olá **criar novo** botão.</span><span class="sxs-lookup"><span data-stu-id="048b8-182">At hello bottom of hello screen, click hello **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="048b8-184">tela de edição de proxy Hello Virtual é exibida.</span><span class="sxs-lookup"><span data-stu-id="048b8-184">hello Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="048b8-185">Em Olá lado direito da tela hello é um menu para tornar visível a opções de configuração.</span><span class="sxs-lookup"><span data-stu-id="048b8-185">On hello right side of hello screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="048b8-187">Com a opção de menu de identificação Olá marcada, digite as informações de identificação de saudação hello Azure virtual configuração de proxy.</span><span class="sxs-lookup"><span data-stu-id="048b8-187">With hello Identification menu option checked, enter hello identifying information for hello Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="048b8-189">a.</span><span class="sxs-lookup"><span data-stu-id="048b8-189">a.</span></span> <span data-ttu-id="048b8-190">Olá **descrição** campo é um nome amigável para a configuração de proxy virtual hello.</span><span class="sxs-lookup"><span data-stu-id="048b8-190">hello **Description** field is a friendly name for hello virtual proxy configuration.</span></span>  <span data-ttu-id="048b8-191">Insira um valor para uma descrição.</span><span class="sxs-lookup"><span data-stu-id="048b8-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="048b8-192">b.</span><span class="sxs-lookup"><span data-stu-id="048b8-192">b.</span></span> <span data-ttu-id="048b8-193">Olá **prefixo** campo identifica Olá o ponto de extremidade de proxy virtual para conectar-se tooQlik sentido com Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="048b8-193">hello **Prefix** field identifies hello virtual proxy endpoint for connecting tooQlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="048b8-194">Insira um nome de prefixo exclusivo para esse proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="048b8-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="048b8-195">c.</span><span class="sxs-lookup"><span data-stu-id="048b8-195">c.</span></span> <span data-ttu-id="048b8-196">**Tempo limite de inatividade de sessão (minutos)** é o tempo limite de saudação para conexões através desse proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="048b8-196">**Session inactivity timeout (minutes)** is hello timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="048b8-197">d.</span><span class="sxs-lookup"><span data-stu-id="048b8-197">d.</span></span> <span data-ttu-id="048b8-198">Olá **nome de cabeçalho do cookie de sessão** é armazenar de nome de cookie Olá Olá identificador de sessão para Olá sessão Qlik sentido um usuário recebe após a autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="048b8-198">hello **Session cookie header name** is hello cookie name storing hello session identifier for hello Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="048b8-199">Esse nome deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="048b8-199">This name must be unique.</span></span>

12. <span data-ttu-id="048b8-200">Clique em toomake de opção de menu de autenticação Olá visível.</span><span class="sxs-lookup"><span data-stu-id="048b8-200">Click on hello Authentication menu option toomake it visible.</span></span>  <span data-ttu-id="048b8-201">tela de autenticação Hello aparece.</span><span class="sxs-lookup"><span data-stu-id="048b8-201">hello Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="048b8-203">a.</span><span class="sxs-lookup"><span data-stu-id="048b8-203">a.</span></span> <span data-ttu-id="048b8-204">Olá **modo de acesso anônimo** suspensa determina se os usuários anônimos podem acessar Qlik sentido por meio do proxy virtual hello.</span><span class="sxs-lookup"><span data-stu-id="048b8-204">hello **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through hello virtual proxy.</span></span>  <span data-ttu-id="048b8-205">opção de padrão de saudação não é nenhum usuário anônimo.</span><span class="sxs-lookup"><span data-stu-id="048b8-205">hello default option is No anonymous user.</span></span>
    
    <span data-ttu-id="048b8-206">b.</span><span class="sxs-lookup"><span data-stu-id="048b8-206">b.</span></span> <span data-ttu-id="048b8-207">Olá **método de autenticação** suspensa determina o esquema Olá Olá autenticação proxy virtual usará.</span><span class="sxs-lookup"><span data-stu-id="048b8-207">hello **Authentication method** drop-down determines hello authentication scheme hello virtual proxy will use.</span></span>  <span data-ttu-id="048b8-208">Selecione SAML na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="048b8-208">Select SAML from hello drop-down list.</span></span>  <span data-ttu-id="048b8-209">Mais opções são exibidas como resultado.</span><span class="sxs-lookup"><span data-stu-id="048b8-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="048b8-210">c.</span><span class="sxs-lookup"><span data-stu-id="048b8-210">c.</span></span> <span data-ttu-id="048b8-211">Em Olá **campo URI de host SAML**, os usuários de nome de host de entrada hello insiram tooaccess Qlik sentido através desse proxy virtual SAML.</span><span class="sxs-lookup"><span data-stu-id="048b8-211">In hello **SAML host URI field**, input hello hostname users enter tooaccess Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="048b8-212">Olá hostname é o uri de saudação de saudação server Qlik sentido.</span><span class="sxs-lookup"><span data-stu-id="048b8-212">hello hostname is hello uri of hello Qlik Sense server.</span></span>
    
    <span data-ttu-id="048b8-213">d.</span><span class="sxs-lookup"><span data-stu-id="048b8-213">d.</span></span> <span data-ttu-id="048b8-214">Em Olá **ID da entidade SAML**, digite Olá mesmo valor inserido para o campo URI de host Olá SAML.</span><span class="sxs-lookup"><span data-stu-id="048b8-214">In hello **SAML entity ID**, enter hello same value entered for hello SAML host URI field.</span></span>
    
    <span data-ttu-id="048b8-215">e.</span><span class="sxs-lookup"><span data-stu-id="048b8-215">e.</span></span> <span data-ttu-id="048b8-216">Olá **metadados IdP SAML** arquivo hello editado anteriormente no hello **editar metadados de federação de configuração do AD do Azure** seção.</span><span class="sxs-lookup"><span data-stu-id="048b8-216">hello **SAML IdP metadata** is hello file edited earlier in hello **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="048b8-217">**Antes de carregar os metadados de IdP hello, arquivo hello precisa toobe editado** tooremove informações tooensure funcionamento entre o AD do Azure e o servidor Qlik sentido.</span><span class="sxs-lookup"><span data-stu-id="048b8-217">**Before uploading hello IdP metadata, hello file needs toobe edited** tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="048b8-218">**Consulte toohello instruções acima se o arquivo hello tem ainda toobe editado.**</span><span class="sxs-lookup"><span data-stu-id="048b8-218">**Please refer toohello instructions above if hello file has yet toobe edited.**</span></span>  <span data-ttu-id="048b8-219">Se Olá arquivo foi editado clique no botão hello e tooupload de arquivo de metadados editado selecione Olá-configuração de proxy virtual toohello.</span><span class="sxs-lookup"><span data-stu-id="048b8-219">If hello file has been edited click on hello Browse button and select hello edited metadata file tooupload it toohello virtual proxy configuration.</span></span>
    
    <span data-ttu-id="048b8-220">f.</span><span class="sxs-lookup"><span data-stu-id="048b8-220">f.</span></span> <span data-ttu-id="048b8-221">Insira a referência de esquema ou nome de atributo Olá para atributo SAML de Olá representando Olá **UserID** AD do Azure envia toohello server Qlik sentido.</span><span class="sxs-lookup"><span data-stu-id="048b8-221">Enter hello attribute name or schema reference for hello SAML attribute representing hello **UserID** Azure AD sends toohello Qlik Sense server.</span></span>  <span data-ttu-id="048b8-222">Informações de referência de esquema estão disponíveis na configuração de postagem de telas Olá aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="048b8-222">Schema reference information is available in hello Azure app screens post configuration.</span></span>  <span data-ttu-id="048b8-223">atributo de nome de saudação toouse, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="048b8-223">toouse hello name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="048b8-224">g.</span><span class="sxs-lookup"><span data-stu-id="048b8-224">g.</span></span> <span data-ttu-id="048b8-225">Insira o valor de saudação para Olá **diretório de usuário** que será anexado toousers quando ele autenticar o servidor de sentido tooQlik por meio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="048b8-225">Enter hello value for hello **user directory** that will be attached toousers when they authenticate tooQlik Sense server through Azure AD.</span></span>  <span data-ttu-id="048b8-226">Valores embutidos em código devem estar entre **colchetes []**.</span><span class="sxs-lookup"><span data-stu-id="048b8-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="048b8-227">toouse um atributo enviado em Olá asserção SAML do AD do Azure, insira o nome de saudação do atributo Olá nessa caixa de texto **sem** colchetes.</span><span class="sxs-lookup"><span data-stu-id="048b8-227">toouse an attribute sent in hello Azure AD SAML assertion, enter hello name of hello attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="048b8-228">h.</span><span class="sxs-lookup"><span data-stu-id="048b8-228">h.</span></span> <span data-ttu-id="048b8-229">Olá **algoritmo de assinatura de SAML** conjuntos Olá Olá virtual configuração de proxy de assinatura de certificado do serviço provedor (deste servidor Qlik sentido maiusculas).</span><span class="sxs-lookup"><span data-stu-id="048b8-229">hello **SAML signing algorithm** sets hello service provider (in this case Qlik Sense server) certificate signing for hello virtual proxy configuration.</span></span>  <span data-ttu-id="048b8-230">Se o servidor de Qlik sentido usar um certificado confiável gerado usando o Microsoft Enhanced RSA e AES Cryptographic Provider, alterar algoritmo de assinatura de SAML Olá muito**SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="048b8-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change hello SAML signing algorithm too**SHA-256**.</span></span>
    
    <span data-ttu-id="048b8-231">i.</span><span class="sxs-lookup"><span data-stu-id="048b8-231">i.</span></span> <span data-ttu-id="048b8-232">Olá seção de mapeamento de atributo SAML permite atributos adicionais, como grupos toobe enviado tooQlik sentido para uso em regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="048b8-232">hello SAML attribute mapping section allows for additional attributes like groups toobe sent tooQlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="048b8-233">Clique em Olá **BALANCEAMENTO de carga** toomake da opção de menu-lo visível.</span><span class="sxs-lookup"><span data-stu-id="048b8-233">Click on hello **LOAD BALANCING** menu option toomake it visible.</span></span>  <span data-ttu-id="048b8-234">Olá balanceamento de carga de tela é exibida.</span><span class="sxs-lookup"><span data-stu-id="048b8-234">hello Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="048b8-236">Clique em Olá **adicionar novo nó de servidor** botão, o nó do mecanismo de select ou nós Qlik sentido serão enviar fins de balanceamento de carga de toofor de sessões e clique Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="048b8-236">Click on hello **Add new server node** button, select engine node or nodes Qlik Sense will send sessions toofor load balancing purposes, and click hello **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="048b8-238">Clique em toomake de opção de menu Avançado Olá visível.</span><span class="sxs-lookup"><span data-stu-id="048b8-238">Click on hello Advanced menu option toomake it visible.</span></span> <span data-ttu-id="048b8-239">tela de Hello avançadas é exibida.</span><span class="sxs-lookup"><span data-stu-id="048b8-239">hello Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="048b8-241">lista de permissões de Host Olá identifica os nomes de host são aceitas durante a conexão toohello server Qlik sentido.</span><span class="sxs-lookup"><span data-stu-id="048b8-241">hello Host white list identifies hostnames that are accepted when connecting toohello Qlik Sense server.</span></span>  <span data-ttu-id="048b8-242">**Insira o nome do host Olá os usuários especificarão ao se conectar a servidor de sentido tooQlik.**</span><span class="sxs-lookup"><span data-stu-id="048b8-242">**Enter hello hostname users will specify when connecting tooQlik Sense server.**</span></span> <span data-ttu-id="048b8-243">Olá hostname é hello mesmo valor como Olá SAML uri de host sem Olá https://.</span><span class="sxs-lookup"><span data-stu-id="048b8-243">hello hostname is hello same value as hello SAML host uri without hello https://.</span></span>

16. <span data-ttu-id="048b8-244">Clique em Olá **aplicar** botão.</span><span class="sxs-lookup"><span data-stu-id="048b8-244">Click hello **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="048b8-246">Clique em mensagem de aviso de saudação tooaccept Okey afirmando proxies proxy virtual toohello vinculado será reiniciado.</span><span class="sxs-lookup"><span data-stu-id="048b8-246">Click OK tooaccept hello warning message that states proxies linked toohello virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="048b8-248">Olá direita da tela hello, menu de itens associados Olá aparece.</span><span class="sxs-lookup"><span data-stu-id="048b8-248">On hello right side of hello screen, hello Associated items menu appears.</span></span>  <span data-ttu-id="048b8-249">Clique em Olá **Proxies** opção de menu.</span><span class="sxs-lookup"><span data-stu-id="048b8-249">Click on hello **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="048b8-251">Olá proxy tela é exibida.</span><span class="sxs-lookup"><span data-stu-id="048b8-251">hello proxy screen appears.</span></span>  <span data-ttu-id="048b8-252">Clique em Olá **Link** botão no hello inferior toolink um proxy do proxy toohello virtual.</span><span class="sxs-lookup"><span data-stu-id="048b8-252">Click hello **Link** button at hello bottom toolink a proxy toohello virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="048b8-254">Nó de proxy Olá Select que oferecem suporte a esta conexão de proxy virtual e clique Olá **Link** botão.</span><span class="sxs-lookup"><span data-stu-id="048b8-254">Select hello proxy node that will support this virtual proxy connection and click hello **Link** button.</span></span>  <span data-ttu-id="048b8-255">Depois de vincular, proxy hello será listado na proxies associados.</span><span class="sxs-lookup"><span data-stu-id="048b8-255">After linking, hello proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="048b8-258">Depois de cinco segundos de tooten, Olá mensagem QMC atualização serão exibida.</span><span class="sxs-lookup"><span data-stu-id="048b8-258">After about five tooten seconds, hello Refresh QMC message will appear.</span></span>  <span data-ttu-id="048b8-259">Clique em Olá **QMC atualização** botão.</span><span class="sxs-lookup"><span data-stu-id="048b8-259">Click hello **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="048b8-261">Quando Olá QMC for atualizado, clique em Olá **Virtual proxies** item de menu.</span><span class="sxs-lookup"><span data-stu-id="048b8-261">When hello QMC refreshes, click on hello **Virtual proxies** menu item.</span></span> <span data-ttu-id="048b8-262">nova entrada de proxy virtual SAML Hello está listada na tabela de saudação na tela hello.</span><span class="sxs-lookup"><span data-stu-id="048b8-262">hello new SAML virtual proxy entry is listed in hello table on hello screen.</span></span>  <span data-ttu-id="048b8-263">Clique na entrada de proxy virtual hello.</span><span class="sxs-lookup"><span data-stu-id="048b8-263">Single click on hello virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="048b8-265">Na parte inferior de saudação da tela hello, botão de metadados de SP baixar hello serão ativados.</span><span class="sxs-lookup"><span data-stu-id="048b8-265">At hello bottom of hello screen, hello Download SP metadata button will activate.</span></span>  <span data-ttu-id="048b8-266">Clique em Olá **SP baixar metadados** arquivo tooa do botão toosave Olá metadados.</span><span class="sxs-lookup"><span data-stu-id="048b8-266">Click hello **Download SP metadata** button toosave hello metadata tooa file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="048b8-268">Arquivo de metadados de sp Olá aberto.</span><span class="sxs-lookup"><span data-stu-id="048b8-268">Open hello sp metadata file.</span></span>  <span data-ttu-id="048b8-269">Observar Olá **entityID** entrada e hello **AssertionConsumerService** entrada.</span><span class="sxs-lookup"><span data-stu-id="048b8-269">Observe hello **entityID** entry and hello **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="048b8-270">Esses valores são equivalente toohello **identificador** e hello **URL de logon** na configuração de aplicativo de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="048b8-270">These values are equivalent toohello **Identifier** and hello **Sign on URL** in hello Azure AD application configuration.</span></span> <span data-ttu-id="048b8-271">Cole esses valores hello **URLs e domínio da empresa sentido Qlik** seção na configuração de aplicativo hello AD do Azure se eles não são correspondentes, em seguida, você deve substituí-las no Assistente de configuração de aplicativo do Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="048b8-271">Paste these values in hello **Qlik Sense Enterprise Domain and URLs** section in hello Azure AD application configuration if they are not matching, then you should replace them in hello Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="048b8-273">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="048b8-273">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="048b8-274">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="048b8-274">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="048b8-275">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="048b8-275">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="048b8-276">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="048b8-276">Create an Azure AD test user</span></span>
<span data-ttu-id="048b8-277">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="048b8-277">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="048b8-279">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="048b8-279">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="048b8-280">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="048b8-280">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

   ![botão de Active Directory do Azure Olá](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="048b8-282">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="048b8-282">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

   ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="048b8-284">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="048b8-284">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

   ![botão Adicionar de saudação](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="048b8-286">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="048b8-286">In hello **User** dialog box, perform hello following steps:</span></span>

   ![caixa de diálogo de usuário Olá](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="048b8-288">a.</span><span class="sxs-lookup"><span data-stu-id="048b8-288">a.</span></span> <span data-ttu-id="048b8-289">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="048b8-289">In hello **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="048b8-290">b.</span><span class="sxs-lookup"><span data-stu-id="048b8-290">b.</span></span> <span data-ttu-id="048b8-291">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="048b8-291">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

   <span data-ttu-id="048b8-292">c.</span><span class="sxs-lookup"><span data-stu-id="048b8-292">c.</span></span> <span data-ttu-id="048b8-293">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="048b8-293">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

   <span data-ttu-id="048b8-294">d.</span><span class="sxs-lookup"><span data-stu-id="048b8-294">d.</span></span> <span data-ttu-id="048b8-295">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="048b8-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="048b8-296">Criar um usuário de teste do Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="048b8-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="048b8-297">Nesta seção, você deve criar uma usuária chamada Brenda Fernandes no Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="048b8-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="048b8-298">Trabalhar com [a equipe de suporte Qlik sentido Enterprise Client](https://www.qlik.com/us/services/support) para adicionar usuários de saudação na plataforma do hello Qlik sentido Enterprise.</span><span class="sxs-lookup"><span data-stu-id="048b8-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add hello users in hello Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="048b8-299">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="048b8-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="048b8-300">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="048b8-300">Assign hello Azure AD test user</span></span>

<span data-ttu-id="048b8-301">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooQlik sentido Enterprise.</span><span class="sxs-lookup"><span data-stu-id="048b8-301">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQlik Sense Enterprise.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="048b8-303">**tooassign Britta Simon tooQlik sentido Enterprise, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="048b8-303">**tooassign Britta Simon tooQlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="048b8-304">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="048b8-304">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="048b8-306">Na lista de aplicativos hello, selecione **Qlik sentido Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="048b8-306">In hello applications list, select **Qlik Sense Enterprise**.</span></span>

    ![link de Qlik sentido Enterprise Olá na lista de aplicativos Olá](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="048b8-308">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="048b8-308">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="048b8-310">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="048b8-310">Click **Add** button.</span></span> <span data-ttu-id="048b8-311">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="048b8-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="048b8-313">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="048b8-313">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="048b8-314">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="048b8-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="048b8-315">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="048b8-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="048b8-316">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="048b8-316">Test single sign-on</span></span>

<span data-ttu-id="048b8-317">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="048b8-317">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="048b8-318">Quando você clica em bloco Qlik sentido Enterprise Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Qlik sentido Enterprise.</span><span class="sxs-lookup"><span data-stu-id="048b8-318">When you click hello Qlik Sense Enterprise tile in hello Access Panel, you should get automatically signed-on tooyour Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="048b8-319">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="048b8-319">Additional resources</span></span>

* [<span data-ttu-id="048b8-320">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="048b8-320">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="048b8-321">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="048b8-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

