---
title: "Tutorial: Integração do Azure Active Directory ao HR2day by Merces | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e HR2day por Merces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="f701a-103">Tutorial: Integração do Active Directory do Azure ao HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="f701a-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="f701a-104">Neste tutorial, você aprenderá como toointegrate HR2day por Merces com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f701a-104">In this tutorial, you learn how toointegrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f701a-105">Integrando HR2day por Merces com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="f701a-105">Integrating HR2day by Merces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f701a-106">Você pode controlar no AD do Azure que tenha acesso tooHR2day por Merces.</span><span class="sxs-lookup"><span data-stu-id="f701a-106">You can control in Azure AD who has access tooHR2day by Merces.</span></span>
- <span data-ttu-id="f701a-107">Você pode permitir que os usuários tooautomatically obter conectado tooHR2day por Merces com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f701a-107">You can enable your users tooautomatically get signed in tooHR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="f701a-108">Você pode gerenciar suas contas em um local central – Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f701a-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="f701a-109">Para obter mais informações sobre a integração de aplicativos SaaS ao Azure AD, consulte [O que é o acesso de aplicativos e o logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f701a-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f701a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f701a-110">Prerequisites</span></span>

<span data-ttu-id="f701a-111">tooconfigure integração do AD do Azure com HR2day por Merces, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f701a-111">tooconfigure Azure AD integration with HR2day by Merces, you need hello following items:</span></span>

- <span data-ttu-id="f701a-112">Uma assinatura do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f701a-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="f701a-113">Uma assinatura do HR2day by Merces habilitada para logon único.</span><span class="sxs-lookup"><span data-stu-id="f701a-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="f701a-114">Não é recomendável usar uma saudação de tootest do ambiente de produção as etapas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f701a-114">We don't recommend using a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="f701a-115">etapas de saudação tootest neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f701a-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="f701a-116">Não use o ambiente de produção a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f701a-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="f701a-117">Obtenha uma [avaliação gratuita de um mês do Azure AD](https://azure.microsoft.com/pricing/free-trial/) se você ainda não o fez.</span><span class="sxs-lookup"><span data-stu-id="f701a-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="f701a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f701a-118">Scenario description</span></span>
<span data-ttu-id="f701a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f701a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f701a-120">cenário de saudação que é descrito aqui consiste em duas principais blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="f701a-120">hello scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="f701a-121">Adicionando HR2day por Merces da Galeria de saudação.</span><span class="sxs-lookup"><span data-stu-id="f701a-121">Adding HR2day by Merces from hello gallery.</span></span>
2. <span data-ttu-id="f701a-122">Configurar e testar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f701a-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-hello-gallery"></a><span data-ttu-id="f701a-123">Adicionar HR2day por Merces da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f701a-123">Add HR2day by Merces from hello gallery</span></span>
<span data-ttu-id="f701a-124">integração de saudação do tooconfigure do HR2day por Merces no AD do Azure, adicionar HR2day por Merces na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f701a-124">tooconfigure hello integration of HR2day by Merces into Azure AD, add HR2day by Merces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f701a-125">**tooadd HR2day por Merces da Galeria hello, Olá execute as etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f701a-125">**tooadd HR2day by Merces from hello gallery, take hello following steps:**</span></span>

1. <span data-ttu-id="f701a-126">Em Olá [portal do Azure](https://portal.azure.com), em Olá painel de navegação esquerdo, selecione Olá **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f701a-126">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f701a-128">Vá muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f701a-128">Go too**Enterprise applications**.</span></span> <span data-ttu-id="f701a-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f701a-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f701a-131">tooadd um novo aplicativo, selecione Olá **novo aplicativo** botão na parte superior de Olá Olá da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f701a-131">tooadd a new application, select hello **New application** button on hello top of hello dialog box.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f701a-133">Na caixa de pesquisa hello, digite **HR2day por Merces**.</span><span class="sxs-lookup"><span data-stu-id="f701a-133">In hello search box, type **HR2day by Merces**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="f701a-135">No painel de resultados de saudação, selecione **HR2day por Merces**e, em seguida, selecione Olá **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f701a-135">In hello results panel, select **HR2day by Merces**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f701a-137">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f701a-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f701a-138">Nesta seção, você configurará e testará o logon único do Azure AD com o HR2day by Merces, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="f701a-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f701a-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário contraparte Olá HR2day por Merces tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f701a-139">For single sign-on toowork, Azure AD needs tooknow who hello counterpart user in HR2day by Merces is tooa user in Azure AD.</span></span> <span data-ttu-id="f701a-140">Em outras palavras, você precisa tooestablish um link entre um usuário do AD do Azure e o usuário relacionado de saudação em HR2day por Merces.</span><span class="sxs-lookup"><span data-stu-id="f701a-140">In other words, you need tooestablish a link between an Azure AD user and hello related user in HR2day by Merces.</span></span>

<span data-ttu-id="f701a-141">HR2day por Merces, atribuir Olá **nome de usuário** no AD do Azure muito **Username** tooestablish relação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f701a-141">In HR2day by Merces, assign hello **user name** in Azure AD too **Username** tooestablish hello relationship.</span></span>

<span data-ttu-id="f701a-142">tooconfigure e teste de logon único do AD do Azure com HR2day por Merces, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="f701a-142">tooconfigure and test Azure AD single sign-on with HR2day by Merces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f701a-143">[Configurar o logon único do AD do Azure](#configuring-azure-ad-single-sign-on): habilitar seu usuários toouse esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f701a-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users toouse this feature.</span></span>
2. <span data-ttu-id="f701a-144">[Criar um usuário de teste do Azure AD](#creating-an-azure-ad-test-user): para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f701a-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f701a-145">[Criar um HR2day pelo usuário de teste Merces](#creating-an-hr2day-by-merces-test-user): criar um equivalente de Britta Simon HR2day por Merces é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f701a-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f701a-146">[Atribuir um usuário de teste de saudação do AD do Azure](#assigning-the-azure-ad-test-user): habilitar Britta Simon toouse logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f701a-146">[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f701a-147">[Testar o logon único](#testing-single-sign-on): verificar se a configuração de saudação funciona.</span><span class="sxs-lookup"><span data-stu-id="f701a-147">[Test single sign-on](#testing-single-sign-on): Verify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f701a-148">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f701a-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f701a-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu HR2day pelo aplicativo Merces.</span><span class="sxs-lookup"><span data-stu-id="f701a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="f701a-150">**tooconfigure AD do Azure-logon único com HR2day por Merces, levar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f701a-150">**tooconfigure Azure AD single sign-on with HR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="f701a-151">Em Olá portal do Azure, Olá **HR2day por Merces** página de integração de aplicativos, selecione **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="f701a-151">In hello Azure portal, on hello **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Configurar o Logon Único][4]

2. <span data-ttu-id="f701a-153">tooenable logon único, em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon**.</span><span class="sxs-lookup"><span data-stu-id="f701a-153">tooenable single sign-on, in hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="f701a-155">Em Olá **HR2day Merces domínio e URLs** seção, levar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f701a-155">In hello **HR2day by Merces Domain and URLs** section, take hello following steps:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="f701a-157">a.</span><span class="sxs-lookup"><span data-stu-id="f701a-157">a.</span></span> <span data-ttu-id="f701a-158">Em Olá **URL de logon** caixa, digite uma URL usando o saudação padrão a seguir: `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="f701a-158">In hello **Sign-on URL** box, type a URL by using hello following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="f701a-159">b.</span><span class="sxs-lookup"><span data-stu-id="f701a-159">b.</span></span> <span data-ttu-id="f701a-160">Em Olá **identificador** caixa, digite uma URL usando o saudação padrão a seguir: `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="f701a-160">In hello **Identifier** box, type a URL by using hello following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f701a-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="f701a-161">These values are not real.</span></span> <span data-ttu-id="f701a-162">Atualize esses valores com URL de logon real hello e o identificador.</span><span class="sxs-lookup"><span data-stu-id="f701a-162">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="f701a-163">Olá contato [HR2day pela equipe de suporte de cliente Merces](mailto:servicedesk@merces.nl) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="f701a-163">Contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl) tooget these values.</span></span> 
 


4. <span data-ttu-id="f701a-164">Em Olá **o certificado de autenticação SAML** seção, selecione **Certificate(Base64)**e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f701a-164">On hello **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="f701a-166">Esta seção descreve como tooenable usuários tooauthenticate tooHR2day por Merces com suas contas no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f701a-166">This section describes how tooenable users tooauthenticate tooHR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="f701a-167">Eles fazem isso usando a federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="f701a-167">They do this by using federation that's based on hello SAML protocol.</span></span>

    <span data-ttu-id="f701a-168">O HR2day pelo aplicativo Merces espera asserções SAML de saudação em um formato específico, o que exige que o token SAML tooadd atributo personalizado mapeamentos tooyour.</span><span class="sxs-lookup"><span data-stu-id="f701a-168">Your HR2day by Merces application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token.</span></span> <span data-ttu-id="f701a-169">Olá captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="f701a-169">hello following screenshot shows an example of this.</span></span> 

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="f701a-171">Antes de configurar de asserção SAML hello, você deverá contatar Olá [HR2day pela equipe de suporte do cliente Merces](mailto:servicedesk@merces.nl) e solicitar o valor de saudação do atributo de identificador exclusivo de saudação para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="f701a-171">Before you can configure hello SAML assertion, you must contact hello [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="f701a-172">Você precisa de etapas de Olá de toocomplete esse valor na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="f701a-172">You need this value toocomplete hello steps in hello next section.</span></span> 

6. <span data-ttu-id="f701a-173">Em Olá **o logon único** caixa de diálogo Olá **atributos de usuário** seção, configure o atributo de token de SAML Olá conforme Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="f701a-173">In hello **Single sign-on** dialog box, in hello **User Attributes** section, configure hello SAML token attribute as shown in hello following image.</span></span> <span data-ttu-id="f701a-174">Depois, pegue Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f701a-174">Then take hello following steps.</span></span>
    
      | <span data-ttu-id="f701a-175">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="f701a-175">Attribute name</span></span>    |   <span data-ttu-id="f701a-176">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="f701a-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="f701a-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="f701a-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="f701a-178">join([mail],"102938475Z","@"</span><span class="sxs-lookup"><span data-stu-id="f701a-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="f701a-179">a.</span><span class="sxs-lookup"><span data-stu-id="f701a-179">a.</span></span> <span data-ttu-id="f701a-180">Olá tooopen **Adicionar atributo** caixa de diálogo, selecione **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="f701a-180">tooopen hello **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Configurar o Logon Único](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f701a-183">b.</span><span class="sxs-lookup"><span data-stu-id="f701a-183">b.</span></span> <span data-ttu-id="f701a-184">Em Olá **nome** , digite **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="f701a-184">In hello **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="f701a-185">c.</span><span class="sxs-lookup"><span data-stu-id="f701a-185">c.</span></span> <span data-ttu-id="f701a-186">De saudação **valor** lista, selecione **JOIN ()**.</span><span class="sxs-lookup"><span data-stu-id="f701a-186">From hello **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="f701a-187">d.</span><span class="sxs-lookup"><span data-stu-id="f701a-187">d.</span></span> <span data-ttu-id="f701a-188">De saudação **String1** lista, selecione **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="f701a-188">From hello **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="f701a-189">e.</span><span class="sxs-lookup"><span data-stu-id="f701a-189">e.</span></span> <span data-ttu-id="f701a-190">Para **String2**, digite Olá identificador exclusivo que é fornecido pela sua equipe HR2day.</span><span class="sxs-lookup"><span data-stu-id="f701a-190">For **String2**, type hello unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="f701a-191">f.</span><span class="sxs-lookup"><span data-stu-id="f701a-191">f.</span></span> <span data-ttu-id="f701a-192">Em Olá **separador** , digite  **@** .</span><span class="sxs-lookup"><span data-stu-id="f701a-192">In hello **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="f701a-193">g.</span><span class="sxs-lookup"><span data-stu-id="f701a-193">g.</span></span> <span data-ttu-id="f701a-194">Selecione **Ok**.</span><span class="sxs-lookup"><span data-stu-id="f701a-194">Select **Ok**.</span></span>

7. <span data-ttu-id="f701a-195">Selecione Olá **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="f701a-195">Select hello **Save** button.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f701a-197">Em Olá **HR2day pela configuração Merces** seção, selecione **HR2day configurar por Merces** tooopen Olá **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="f701a-197">In hello **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="f701a-198">Saudação de cópia **URL de logout**, **ID da entidade SAML**, e **Single Sign-On URL do serviço SAML** de saudação **referência rápida** seção.</span><span class="sxs-lookup"><span data-stu-id="f701a-198">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="f701a-200">tooconfigure SSO para seu aplicativo, entre em contato com hello [HR2day pela equipe de suporte de cliente Merces](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="f701a-200">tooconfigure SSO  for your application, contact hello [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="f701a-201">Anexar Olá baixado **Certificate(Base64)** tooyour email de arquivo.</span><span class="sxs-lookup"><span data-stu-id="f701a-201">Attach hello downloaded **Certificate(Base64)** file tooyour email.</span></span> <span data-ttu-id="f701a-202">Também fornecem Olá **URL de logout**, **ID da entidade SAML**, e **Single Sign-On URL do serviço SAML** para que eles podem ser configurados para integração com o SSO.</span><span class="sxs-lookup"><span data-stu-id="f701a-202">Also provide hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="f701a-203">Mencione toohello Merces equipe que essa integração precisa Olá toobe ID de entidade com um padrão de saudação **https://hr2day.force.com/INSTANCENAME**.</span><span class="sxs-lookup"><span data-stu-id="f701a-203">Mention toohello Merces team that this integration needs hello Entity ID toobe set with hello pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="f701a-204">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="f701a-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f701a-205">Depois de adicionar este aplicativo de saudação **do Active Directory** > **aplicativos empresariais** seção, selecione Olá **Single Sign-On** guia. Então Olá acesso incorporado documentação por meio de saudação **configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="f701a-205">After you add this app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab. Then access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f701a-206">Você pode ler mais sobre recurso de documentação embedded Olá no hello [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="f701a-206">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f701a-207">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f701a-207">Create an Azure AD test user</span></span>
<span data-ttu-id="f701a-208">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f701a-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f701a-210">**toocreate um usuário de teste no AD do Azure, Olá execute as etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f701a-210">**toocreate a test user in Azure AD, take hello following steps:**</span></span>

1. <span data-ttu-id="f701a-211">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, selecione Olá **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f701a-211">In hello **Azure portal**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f701a-213">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, selecione **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="f701a-213">toodisplay hello list of users, go too**Users and groups**, and then select **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f701a-215">Olá tooopen **usuário** caixa de diálogo, selecione **adicionar** na parte superior de Olá Olá da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f701a-215">tooopen hello **User** dialog box, select **Add** on hello top of hello dialog box.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f701a-217">Em Olá **usuário** caixa de diálogo, Olá execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f701a-217">In hello **User** dialog box, take hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f701a-219">a.</span><span class="sxs-lookup"><span data-stu-id="f701a-219">a.</span></span> <span data-ttu-id="f701a-220">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f701a-220">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f701a-221">b.</span><span class="sxs-lookup"><span data-stu-id="f701a-221">b.</span></span> <span data-ttu-id="f701a-222">Em Olá **nome de usuário** caixa, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f701a-222">In hello **User name** box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f701a-223">c.</span><span class="sxs-lookup"><span data-stu-id="f701a-223">c.</span></span> <span data-ttu-id="f701a-224">Selecione **Mostrar senha**e, em seguida, anote a senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="f701a-224">Select **Show Password**, and then write down hello password.</span></span>

    <span data-ttu-id="f701a-225">d.</span><span class="sxs-lookup"><span data-stu-id="f701a-225">d.</span></span> <span data-ttu-id="f701a-226">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f701a-226">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="f701a-227">Criar um usuário de teste do HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="f701a-227">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="f701a-228">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no HR2day por Merces.</span><span class="sxs-lookup"><span data-stu-id="f701a-228">hello objective of this section is toocreate a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="f701a-229">os usuários de saudação de tooadd na conta Olá HR2day, trabalhar com hello [HR2day pela equipe de suporte de cliente Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="f701a-229">tooadd hello users in hello HR2day account, work with hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="f701a-230">Se você precisar toocreate um usuário manualmente, entre em contato com o hello [HR2day pela equipe de suporte de cliente Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="f701a-230">If you need toocreate a user manually, contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f701a-231">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f701a-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f701a-232">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooHR2day seu acesso por Merces.</span><span class="sxs-lookup"><span data-stu-id="f701a-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHR2day by Merces.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f701a-234">**tooassign Britta Simon tooHR2day por Merces, Olá execute as etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f701a-234">**tooassign Britta Simon tooHR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="f701a-235">Em hello Azure aplicativos de portal, abra Olá exibir, vá toohello exibição de diretório e, em seguida, ir muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f701a-235">In hello Azure portal, open hello applications view, go toohello directory view, and then go too**Enterprise applications**.</span></span> <span data-ttu-id="f701a-236">Em seguida, selecione **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f701a-236">Next, select **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f701a-238">Na lista de aplicativos hello, selecione **HR2day por Merces**.</span><span class="sxs-lookup"><span data-stu-id="f701a-238">In hello applications list, select **HR2day by Merces**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="f701a-240">No menu Olá Olá esquerda, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f701a-240">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f701a-242">Selecione Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="f701a-242">Select hello **Add** button.</span></span> <span data-ttu-id="f701a-243">Em seguida, no hello **Adicionar atribuição** caixa de diálogo, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f701a-243">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f701a-245">Em Olá **usuários e grupos** caixa de diálogo Olá **usuários** lista, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f701a-245">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="f701a-246">Clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="f701a-246">Click hello **Select** button.</span></span>

7. <span data-ttu-id="f701a-247">Em Olá **Adicionar atribuição** caixa de diálogo, selecione **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="f701a-247">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f701a-248">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="f701a-248">Test single sign-on</span></span>

<span data-ttu-id="f701a-249">Olá, o objetivo desta seção é tootest Olá de seu AD do Azure única configuração de logon usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="f701a-249">hello objective of this section is tootest your Azure AD single sign-on configuration by using hello Access Panel.</span></span>  

<span data-ttu-id="f701a-250">Quando você seleciona Olá HR2day pelo bloco Merces Olá painel de acesso, você obter conectado automaticamente tooyour HR2day pelo aplicativo Merces.</span><span class="sxs-lookup"><span data-stu-id="f701a-250">When you select hello HR2day by Merces tile in hello Access Panel, you automatically get signed in  tooyour HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f701a-251">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f701a-251">Additional resources</span></span>

* [<span data-ttu-id="f701a-252">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f701a-252">List of tutorials about how tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f701a-253">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f701a-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

