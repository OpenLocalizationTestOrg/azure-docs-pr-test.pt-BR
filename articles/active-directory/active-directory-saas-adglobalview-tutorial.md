---
title: "Tutorial: Integração do Azure Active Directory ao ADP Globalview | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ADP Globalview."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: aee2d56f05b486d12facbc41c9503455094604ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="367a7-103">Tutorial: Integração do Azure Active Directory ao ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="367a7-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="367a7-104">Neste tutorial, você aprenderá como toointegrate ADP Globalview com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="367a7-104">In this tutorial, you learn how toointegrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="367a7-105">Integrando ADP Globalview com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="367a7-105">Integrating ADP Globalview with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="367a7-106">Você pode controlar no AD do Azure que tenha acesso tooADP Globalview</span><span class="sxs-lookup"><span data-stu-id="367a7-106">You can control in Azure AD who has access tooADP Globalview</span></span>
- <span data-ttu-id="367a7-107">Você pode habilitar seu usuários tooautomatically get conectado tooADP Globalview (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="367a7-107">You can enable your users tooautomatically get signed-on tooADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="367a7-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="367a7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="367a7-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="367a7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="367a7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="367a7-110">Prerequisites</span></span>

<span data-ttu-id="367a7-111">tooconfigure integração do AD do Azure com ADP Globalview, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="367a7-111">tooconfigure Azure AD integration with ADP Globalview, you need hello following items:</span></span>

- <span data-ttu-id="367a7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="367a7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="367a7-113">Uma assinatura habilitada para logon único do ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="367a7-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="367a7-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="367a7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="367a7-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="367a7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="367a7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="367a7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="367a7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="367a7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="367a7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="367a7-118">Scenario description</span></span>
<span data-ttu-id="367a7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="367a7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="367a7-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="367a7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="367a7-121">Adicionando ADP Globalview da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="367a7-121">Adding ADP Globalview from hello gallery</span></span>
2. <span data-ttu-id="367a7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="367a7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-hello-gallery"></a><span data-ttu-id="367a7-123">Adicionando ADP Globalview da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="367a7-123">Adding ADP Globalview from hello gallery</span></span>
<span data-ttu-id="367a7-124">integração de saudação tooconfigure da ADP Globalview no AD do Azure, você precisa tooadd ADP Globalview da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="367a7-124">tooconfigure hello integration of ADP Globalview into Azure AD, you need tooadd ADP Globalview from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="367a7-125">**tooadd ADP Globalview da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="367a7-125">**tooadd ADP Globalview from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="367a7-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="367a7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="367a7-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="367a7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="367a7-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="367a7-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="367a7-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="367a7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="367a7-133">Na caixa de pesquisa hello, digite **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="367a7-133">In hello search box, type **ADP Globalview**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="367a7-135">No painel de resultados de saudação, selecione **ADP Globalview**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="367a7-135">In hello results panel, select **ADP Globalview**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="367a7-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="367a7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="367a7-138">Nesta seção, você configurará e testará o logon único do Azure AD com o ADP Globalview, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="367a7-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="367a7-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em ADP Globalview é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="367a7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP Globalview is tooa user in Azure AD.</span></span> <span data-ttu-id="367a7-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em ADP Globalview precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="367a7-140">In other words, a link relationship between an Azure AD user and hello related user in ADP Globalview needs toobe established.</span></span>

<span data-ttu-id="367a7-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="367a7-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP Globalview.</span></span>

<span data-ttu-id="367a7-142">tooconfigure e teste de logon único do AD do Azure com ADP Globalview, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="367a7-142">tooconfigure and test Azure AD single sign-on with ADP Globalview, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="367a7-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="367a7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="367a7-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="367a7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="367a7-145">**[Criar um usuário de teste ADP Globalview](#creating-an-adp-globalview-test-user)**  -toohave um equivalente do Britta Simon em ADP Globalview que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="367a7-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - toohave a counterpart of Britta Simon in ADP Globalview that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="367a7-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="367a7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="367a7-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="367a7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="367a7-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="367a7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="367a7-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="367a7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="367a7-150">**tooconfigure AD do Azure-logon único com ADP Globalview, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="367a7-150">**tooconfigure Azure AD single sign-on with ADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="367a7-151">Em Olá portal do Azure, Olá **ADP Globalview** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="367a7-151">In hello Azure portal, on hello **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="367a7-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="367a7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="367a7-155">Em Olá **ADP Globalview domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="367a7-155">On hello **ADP Globalview Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="367a7-157">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir: `https://<subdomain>.globalview.adp.com/federate` ou`https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="367a7-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="367a7-158">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="367a7-158">hello value is not real.</span></span> <span data-ttu-id="367a7-159">Atualize o valor de saudação com hello identificador real.</span><span class="sxs-lookup"><span data-stu-id="367a7-159">Update hello value with hello actual Identifier.</span></span> <span data-ttu-id="367a7-160">Entre em contato com [suporte ADP Globalview](https://www.adp.com/contact-us/overview.aspx) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="367a7-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooget hello value.</span></span>
 
4. <span data-ttu-id="367a7-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="367a7-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="367a7-163">Olá ADP GlobalView aplicativo espera as asserções de SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML.</span><span class="sxs-lookup"><span data-stu-id="367a7-163">hello ADP GlobalView application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="367a7-164">Olá captura de tela a seguir mostra um exemplo para ele.</span><span class="sxs-lookup"><span data-stu-id="367a7-164">hello following screenshot shows an example for it.</span></span> <span data-ttu-id="367a7-165">Olá nomes de declaração sempre ser **"PersonImmutableID"** e o valor de saudação do qual estamos mapeou tooExtensionAttribute2, que contém Olá EmployeeID do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="367a7-165">hello claim names always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2, which contains hello EmployeeID of hello user.</span></span> <span data-ttu-id="367a7-166">Aqui mapeamento de usuário de saudação do AD do Azure tooADP GlobalView é feito em Olá EmployeeID, mas você pode mapear valor diferente de tooa também com base nas suas configurações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="367a7-166">Here hello user mapping from Azure AD tooADP GlobalView is done on hello EmployeeID but you can map it tooa different value also based on your application settings.</span></span> <span data-ttu-id="367a7-167">Você pode trabalhar com hello ADP GlobalView equipe primeiro toouse Olá identificador correto de um usuário e mapear esse valor com hello **"PersonImmutableID"** de declaração.</span><span class="sxs-lookup"><span data-stu-id="367a7-167">You can work with hello ADP GlobalView team first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="367a7-168">Você também pode mapear Olá declaração de Email e UserID conforme mostrado na imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="367a7-168">You can also map hello Email and UserID claim as shown in hello picture.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="367a7-170">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="367a7-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="367a7-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="367a7-171">Attribute Name</span></span> | <span data-ttu-id="367a7-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="367a7-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="367a7-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="367a7-173">personalimmutableid</span></span> | <span data-ttu-id="367a7-174">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="367a7-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="367a7-175">email</span><span class="sxs-lookup"><span data-stu-id="367a7-175">email</span></span>               | <span data-ttu-id="367a7-176">user.mail</span><span class="sxs-lookup"><span data-stu-id="367a7-176">user.mail</span></span> |
    | <span data-ttu-id="367a7-177">userid</span><span class="sxs-lookup"><span data-stu-id="367a7-177">userid</span></span>              | <span data-ttu-id="367a7-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="367a7-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="367a7-179">a.</span><span class="sxs-lookup"><span data-stu-id="367a7-179">a.</span></span> <span data-ttu-id="367a7-180">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="367a7-180">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="367a7-183">b.</span><span class="sxs-lookup"><span data-stu-id="367a7-183">b.</span></span> <span data-ttu-id="367a7-184">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="367a7-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="367a7-185">c.</span><span class="sxs-lookup"><span data-stu-id="367a7-185">c.</span></span> <span data-ttu-id="367a7-186">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="367a7-186">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="367a7-187">d.</span><span class="sxs-lookup"><span data-stu-id="367a7-187">d.</span></span> <span data-ttu-id="367a7-188">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="367a7-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="367a7-189">Antes de configurar de asserção SAML hello, você precisa toocontact seu [suporte ADP Globalview](https://www.adp.com/contact-us/overview.aspx) e solicitar o valor de saudação do atributo de identificador exclusivo de saudação para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="367a7-189">Before you can configure hello SAML assertion, you need toocontact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="367a7-190">Você precisa esta declaração valor tooconfigure Olá personalizado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="367a7-190">You need this value tooconfigure hello custom claim for your application.</span></span> 

8. <span data-ttu-id="367a7-191">Em Olá **ADP Globalview configuração** seção, clique em **configurar ADP Globalview** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="367a7-191">On hello **ADP Globalview Configuration** section, click **Configure ADP Globalview** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="367a7-192">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="367a7-192">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="367a7-194">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="367a7-194">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="367a7-196">tooconfigure logon único no **ADP Globalview** lado, você precisa toosend Olá baixado **certificado (Base64)**, **URL de logout, ID de entidade de SAML e SAML Single Sign-On URL do serviço** muito[suporte ADP Globalview](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="367a7-196">tooconfigure single sign-on on **ADP Globalview** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="367a7-197">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="367a7-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="367a7-198">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="367a7-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="367a7-199">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="367a7-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="367a7-200">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="367a7-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="367a7-201">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="367a7-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="367a7-203">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="367a7-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="367a7-204">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="367a7-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="367a7-206">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="367a7-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="367a7-208">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="367a7-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="367a7-210">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="367a7-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="367a7-212">a.</span><span class="sxs-lookup"><span data-stu-id="367a7-212">a.</span></span> <span data-ttu-id="367a7-213">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="367a7-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="367a7-214">b.</span><span class="sxs-lookup"><span data-stu-id="367a7-214">b.</span></span> <span data-ttu-id="367a7-215">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="367a7-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="367a7-216">c.</span><span class="sxs-lookup"><span data-stu-id="367a7-216">c.</span></span> <span data-ttu-id="367a7-217">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="367a7-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="367a7-218">d.</span><span class="sxs-lookup"><span data-stu-id="367a7-218">d.</span></span> <span data-ttu-id="367a7-219">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="367a7-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="367a7-220">Criando um usuário de teste do ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="367a7-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="367a7-221">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="367a7-221">hello objective of this section is toocreate a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="367a7-222">Trabalhar com [suporte ADP Globalview](https://www.adp.com/contact-us/overview.aspx) tooadd usuários Olá Olá ADP GlobalView conta.</span><span class="sxs-lookup"><span data-stu-id="367a7-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP GlobalView account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="367a7-223">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="367a7-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="367a7-224">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="367a7-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP Globalview.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="367a7-226">**tooassign tooADP Britta Simon Globalview, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="367a7-226">**tooassign Britta Simon tooADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="367a7-227">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="367a7-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="367a7-229">Na lista de aplicativos hello, selecione **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="367a7-229">In hello applications list, select **ADP Globalview**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="367a7-231">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="367a7-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="367a7-233">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="367a7-233">Click **Add** button.</span></span> <span data-ttu-id="367a7-234">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="367a7-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="367a7-236">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="367a7-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="367a7-237">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="367a7-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="367a7-238">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="367a7-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="367a7-239">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="367a7-239">Testing single sign-on</span></span>

<span data-ttu-id="367a7-240">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="367a7-240">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="367a7-241">Quando você clica em Olá ADP GlobalView bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="367a7-241">When you click hello ADP GlobalView tile in hello Access Panel, you should get automatically signed-on tooyour ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="367a7-242">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="367a7-242">Additional resources</span></span>

* [<span data-ttu-id="367a7-243">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="367a7-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="367a7-244">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="367a7-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

