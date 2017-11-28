---
title: "Tutorial: Integração do Azure Active Directory ao BenefitHub | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e BenefitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: c07d6e44e8cbc79afd79c900664011b059206b56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="554d7-103">Tutorial: Integração do Azure Active Directory ao BenefitHub</span><span class="sxs-lookup"><span data-stu-id="554d7-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="554d7-104">Neste tutorial, você aprenderá como toointegrate BenefitHub com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="554d7-104">In this tutorial, you learn how toointegrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="554d7-105">Integrando BenefitHub com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="554d7-105">Integrating BenefitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="554d7-106">Você pode controlar no AD do Azure que tenha acesso tooBenefitHub</span><span class="sxs-lookup"><span data-stu-id="554d7-106">You can control in Azure AD who has access tooBenefitHub</span></span>
- <span data-ttu-id="554d7-107">Você pode habilitar seu usuários tooautomatically get conectado tooBenefitHub (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="554d7-107">You can enable your users tooautomatically get signed-on tooBenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="554d7-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="554d7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="554d7-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="554d7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="554d7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="554d7-110">Prerequisites</span></span>

<span data-ttu-id="554d7-111">tooconfigure integração do AD do Azure com BenefitHub, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="554d7-111">tooconfigure Azure AD integration with BenefitHub, you need hello following items:</span></span>

- <span data-ttu-id="554d7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="554d7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="554d7-113">Uma assinatura habilitada para logon único do BenefitHub</span><span class="sxs-lookup"><span data-stu-id="554d7-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="554d7-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="554d7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="554d7-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="554d7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="554d7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="554d7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="554d7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="554d7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="554d7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="554d7-118">Scenario description</span></span>
<span data-ttu-id="554d7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="554d7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="554d7-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="554d7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="554d7-121">Adicionando BenefitHub da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="554d7-121">Adding BenefitHub from hello gallery</span></span>
2. <span data-ttu-id="554d7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="554d7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-hello-gallery"></a><span data-ttu-id="554d7-123">Adicionando BenefitHub da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="554d7-123">Adding BenefitHub from hello gallery</span></span>
<span data-ttu-id="554d7-124">integração de saudação tooconfigure de BenefitHub no AD do Azure, você precisa tooadd BenefitHub da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="554d7-124">tooconfigure hello integration of BenefitHub into Azure AD, you need tooadd BenefitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="554d7-125">**tooadd BenefitHub da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="554d7-125">**tooadd BenefitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="554d7-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="554d7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="554d7-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="554d7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="554d7-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="554d7-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="554d7-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="554d7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="554d7-133">Na caixa de pesquisa hello, digite **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="554d7-133">In hello search box, type **BenefitHub**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="554d7-135">No painel de resultados de saudação, selecione **BenefitHub**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="554d7-135">In hello results panel, select **BenefitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="554d7-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="554d7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="554d7-138">Nesta seção, você configura e testa o logon único do Azure AD com o BenefitHub, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="554d7-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="554d7-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em BenefitHub é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="554d7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenefitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="554d7-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em BenefitHub precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="554d7-140">In other words, a link relationship between an Azure AD user and hello related user in BenefitHub needs toobe established.</span></span>

<span data-ttu-id="554d7-141">BenefitHub, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="554d7-141">In BenefitHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="554d7-142">tooconfigure e teste de logon único do AD do Azure com BenefitHub, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="554d7-142">tooconfigure and test Azure AD single sign-on with BenefitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="554d7-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="554d7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="554d7-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="554d7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="554d7-145">**[Criar um usuário de teste BenefitHub](#creating-a-benefithub-test-user)**  -toohave um equivalente do Britta Simon em BenefitHub é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="554d7-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - toohave a counterpart of Britta Simon in BenefitHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="554d7-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="554d7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="554d7-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="554d7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="554d7-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="554d7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="554d7-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="554d7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="554d7-150">**tooconfigure AD do Azure-logon único com BenefitHub, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="554d7-150">**tooconfigure Azure AD single sign-on with BenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="554d7-151">Em Olá portal do Azure, Olá **BenefitHub** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="554d7-151">In hello Azure portal, on hello **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="554d7-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="554d7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="554d7-155">Em Olá **BenefitHub domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="554d7-155">On hello **BenefitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="554d7-157">a.</span><span class="sxs-lookup"><span data-stu-id="554d7-157">a.</span></span> <span data-ttu-id="554d7-158">Em Olá **identificador** caixa de texto, tipo:`urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="554d7-158">In hello **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="554d7-159">b.</span><span class="sxs-lookup"><span data-stu-id="554d7-159">b.</span></span> <span data-ttu-id="554d7-160">Em Olá **URL de resposta** caixa de texto, tipo:`https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="554d7-160">In hello **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="554d7-161">Olá BenefitHub aplicativo espera as asserções de SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML.</span><span class="sxs-lookup"><span data-stu-id="554d7-161">hello BenefitHub application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="554d7-162">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="554d7-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="554d7-163">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="554d7-163">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="554d7-165">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, como mostrado no hello anterior a imagem e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="554d7-165">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="554d7-166">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="554d7-166">Attribute Name</span></span> | <span data-ttu-id="554d7-167">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="554d7-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="554d7-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="554d7-168">organizationid</span></span> | <span data-ttu-id="554d7-169">< organizationid ></span><span class="sxs-lookup"><span data-stu-id="554d7-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="554d7-170">Esse valor de atributo não é real.</span><span class="sxs-lookup"><span data-stu-id="554d7-170">This attribute value is not real.</span></span> <span data-ttu-id="554d7-171">Atualize esse valor com a organizationid real.</span><span class="sxs-lookup"><span data-stu-id="554d7-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="554d7-172">Entre em contato com [BenefitHub a equipe de suporte](https://www.benefithub.com/Home/ContactUs) tooget Olá organizationid real.</span><span class="sxs-lookup"><span data-stu-id="554d7-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) tooget hello actual organizationid.</span></span>
    
    <span data-ttu-id="554d7-173">a.</span><span class="sxs-lookup"><span data-stu-id="554d7-173">a.</span></span> <span data-ttu-id="554d7-174">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="554d7-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="554d7-177">b.</span><span class="sxs-lookup"><span data-stu-id="554d7-177">b.</span></span> <span data-ttu-id="554d7-178">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="554d7-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="554d7-179">c.</span><span class="sxs-lookup"><span data-stu-id="554d7-179">c.</span></span> <span data-ttu-id="554d7-180">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="554d7-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="554d7-181">d.</span><span class="sxs-lookup"><span data-stu-id="554d7-181">d.</span></span> <span data-ttu-id="554d7-182">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="554d7-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="554d7-183">Antes de configurar de asserção SAML hello, você precisa toocontact seu [BenefitHub suporte](https://www.benefithub.com/Home/ContactUs) e solicitar o valor de saudação do atributo de identificador exclusivo de saudação para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="554d7-183">Before you can configure hello SAML assertion, you need toocontact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="554d7-184">Você precisa esta declaração valor tooconfigure Olá personalizado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="554d7-184">You need this value tooconfigure hello custom claim for your application.</span></span>

6. <span data-ttu-id="554d7-185">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="554d7-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="554d7-187">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="554d7-187">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="554d7-189">tooconfigure logon único no **BenefitHub** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte BenefitHub](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="554d7-189">tooconfigure single sign-on on **BenefitHub** side, you need toosend hello downloaded **Metadata XML** too[BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="554d7-190">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="554d7-190">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="554d7-191">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="554d7-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="554d7-192">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="554d7-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="554d7-193">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="554d7-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="554d7-194">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="554d7-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="554d7-195">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="554d7-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="554d7-197">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="554d7-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="554d7-198">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="554d7-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="554d7-200">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="554d7-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="554d7-202">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="554d7-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="554d7-204">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="554d7-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="554d7-206">a.</span><span class="sxs-lookup"><span data-stu-id="554d7-206">a.</span></span> <span data-ttu-id="554d7-207">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="554d7-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="554d7-208">b.</span><span class="sxs-lookup"><span data-stu-id="554d7-208">b.</span></span> <span data-ttu-id="554d7-209">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="554d7-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="554d7-210">c.</span><span class="sxs-lookup"><span data-stu-id="554d7-210">c.</span></span> <span data-ttu-id="554d7-211">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="554d7-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="554d7-212">d.</span><span class="sxs-lookup"><span data-stu-id="554d7-212">d.</span></span> <span data-ttu-id="554d7-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="554d7-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="554d7-214">Criando um usuário de teste do BenefitHub</span><span class="sxs-lookup"><span data-stu-id="554d7-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="554d7-215">Nesta seção, você cria um usuário chamado Brenda Fernandes no BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="554d7-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="554d7-216">Trabalhar com [BenefitHub a equipe de suporte](https://www.benefithub.com/Home/ContactUs) para adicionar usuários de saudação na plataforma de BenefitHub hello.</span><span class="sxs-lookup"><span data-stu-id="554d7-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add hello users in hello BenefitHub platform.</span></span> <span data-ttu-id="554d7-217">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="554d7-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="554d7-218">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="554d7-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="554d7-219">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBenefitHub.</span><span class="sxs-lookup"><span data-stu-id="554d7-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenefitHub.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="554d7-221">**tooassign Britta Simon tooBenefitHub, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="554d7-221">**tooassign Britta Simon tooBenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="554d7-222">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="554d7-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="554d7-224">Na lista de aplicativos hello, selecione **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="554d7-224">In hello applications list, select **BenefitHub**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="554d7-226">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="554d7-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="554d7-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="554d7-228">Click **Add** button.</span></span> <span data-ttu-id="554d7-229">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="554d7-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="554d7-231">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="554d7-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="554d7-232">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="554d7-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="554d7-233">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="554d7-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="554d7-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="554d7-234">Testing single sign-on</span></span>

<span data-ttu-id="554d7-235">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="554d7-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="554d7-236">Quando você clica em bloco BenefitHub Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour BenefitHub aplicativo.</span><span class="sxs-lookup"><span data-stu-id="554d7-236">When you click hello BenefitHub tile in hello Access Panel, you should get automatically signed-on tooyour BenefitHub application.</span></span>
<span data-ttu-id="554d7-237">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="554d7-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="554d7-238">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="554d7-238">Additional resources</span></span>

* [<span data-ttu-id="554d7-239">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="554d7-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="554d7-240">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="554d7-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

