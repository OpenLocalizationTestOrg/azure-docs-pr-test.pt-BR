---
title: "Tutorial: Integração do Azure Active Directory ao DigiCert | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e DigiCert."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 861039d00533b3aeb361d04e45c4460c6fc8cef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="6dfd6-103">Tutorial: integração do Azure Active Directory com o DigiCert</span><span class="sxs-lookup"><span data-stu-id="6dfd6-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="6dfd6-104">Neste tutorial, você aprenderá como toointegrate DigiCert com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="6dfd6-104">In this tutorial, you learn how toointegrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6dfd6-105">Integrando DigiCert com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="6dfd6-105">Integrating DigiCert with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6dfd6-106">Você pode controlar no AD do Azure que tenha acesso tooDigiCert</span><span class="sxs-lookup"><span data-stu-id="6dfd6-106">You can control in Azure AD who has access tooDigiCert</span></span>
- <span data-ttu-id="6dfd6-107">Você pode habilitar seu usuários tooautomatically get conectado tooDigiCert (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6dfd6-107">You can enable your users tooautomatically get signed-on tooDigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6dfd6-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6dfd6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6dfd6-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6dfd6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6dfd6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6dfd6-110">Prerequisites</span></span>

<span data-ttu-id="6dfd6-111">tooconfigure integração do AD do Azure com DigiCert, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="6dfd6-111">tooconfigure Azure AD integration with DigiCert, you need hello following items:</span></span>

- <span data-ttu-id="6dfd6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6dfd6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6dfd6-113">Uma assinatura habilitada para logon único do DigiCert</span><span class="sxs-lookup"><span data-stu-id="6dfd6-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6dfd6-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6dfd6-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6dfd6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6dfd6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6dfd6-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6dfd6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6dfd6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6dfd6-118">Scenario description</span></span>
<span data-ttu-id="6dfd6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6dfd6-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="6dfd6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6dfd6-121">Adicionando DigiCert da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="6dfd6-121">Adding DigiCert from hello gallery</span></span>
2. <span data-ttu-id="6dfd6-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6dfd6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-hello-gallery"></a><span data-ttu-id="6dfd6-123">Adicionando DigiCert da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="6dfd6-123">Adding DigiCert from hello gallery</span></span>
<span data-ttu-id="6dfd6-124">integração de saudação tooconfigure de DigiCert no AD do Azure, você precisa tooadd DigiCert da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-124">tooconfigure hello integration of DigiCert into Azure AD, you need tooadd DigiCert from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6dfd6-125">**tooadd DigiCert da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6dfd6-125">**tooadd DigiCert from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6dfd6-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6dfd6-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6dfd6-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="6dfd6-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="6dfd6-133">Na caixa de pesquisa hello, digite **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-133">In hello search box, type **DigiCert**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="6dfd6-135">No painel de resultados de saudação, selecione **DigiCert**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-135">In hello results panel, select **DigiCert**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6dfd6-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6dfd6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6dfd6-138">Nesta seção, você configurará e testará o logon único do Azure AD com o DigiCert com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="6dfd6-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6dfd6-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em DigiCert é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DigiCert is tooa user in Azure AD.</span></span> <span data-ttu-id="6dfd6-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em DigiCert precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-140">In other words, a link relationship between an Azure AD user and hello related user in DigiCert needs toobe established.</span></span>

<span data-ttu-id="6dfd6-141">DigiCert, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-141">In DigiCert, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6dfd6-142">tooconfigure e teste de logon único do AD do Azure com DigiCert, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="6dfd6-142">tooconfigure and test Azure AD single sign-on with DigiCert, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6dfd6-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6dfd6-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6dfd6-145">**[Criar um usuário de teste DigiCert](#creating-a-digicert-test-user)**  -toohave um equivalente do Britta Simon em DigiCert é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - toohave a counterpart of Britta Simon in DigiCert that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6dfd6-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6dfd6-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6dfd6-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6dfd6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6dfd6-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo DigiCert.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="6dfd6-150">**tooconfigure AD do Azure-logon único com DigiCert, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6dfd6-150">**tooconfigure Azure AD single sign-on with DigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="6dfd6-151">Em Olá portal do Azure, Olá **DigiCert** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-151">In hello Azure portal, on hello **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="6dfd6-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="6dfd6-155">Em Olá **DigiCert domínio e URLs** seção, hello usuário não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-155">On hello **DigiCert Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="6dfd6-157">Aplicativo de DigiCert espera asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-157">DigiCert application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="6dfd6-158">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-158">Configure hello following claims for this application.</span></span> <span data-ttu-id="6dfd6-159">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-159">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="6dfd6-160">Olá captura de tela a seguir mostra um exemplo para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-160">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="6dfd6-162">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6dfd6-162">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="6dfd6-163">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="6dfd6-163">Attribute Name</span></span> | <span data-ttu-id="6dfd6-164">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="6dfd6-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="6dfd6-165">company</span><span class="sxs-lookup"><span data-stu-id="6dfd6-165">company</span></span> | <span data-ttu-id="6dfd6-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="6dfd6-166">< companycode ></span></span> |
    | <span data-ttu-id="6dfd6-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="6dfd6-167">digicertrole</span></span> | <span data-ttu-id="6dfd6-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="6dfd6-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="6dfd6-169">Olá valor **empresa** atributo não é real.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-169">hello value of **company** attribute is not real.</span></span> <span data-ttu-id="6dfd6-170">Atualize esse valor com o código da empresa real.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-170">Update this value with actual company code.</span></span> <span data-ttu-id="6dfd6-171">valor Olá tooget **empresa** atributo contato [a equipe de suporte DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="6dfd6-171">tooget hello value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="6dfd6-172">a.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-172">a.</span></span> <span data-ttu-id="6dfd6-173">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-173">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="6dfd6-176">b.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-176">b.</span></span> <span data-ttu-id="6dfd6-177">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-177">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="6dfd6-178">c.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-178">c.</span></span> <span data-ttu-id="6dfd6-179">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-179">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="6dfd6-180">d.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-180">d.</span></span> <span data-ttu-id="6dfd6-181">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="6dfd6-182">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-182">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="6dfd6-184">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="6dfd6-184">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="6dfd6-186">tooconfigure logon único no **DigiCert** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="6dfd6-186">tooconfigure single sign-on on **DigiCert** side, you need toosend hello downloaded **Metadata XML** too[DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="6dfd6-187">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-187">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6dfd6-188">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="6dfd6-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6dfd6-189">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6dfd6-190">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6dfd6-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6dfd6-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6dfd6-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="6dfd6-192">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="6dfd6-194">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6dfd6-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6dfd6-195">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6dfd6-197">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6dfd6-199">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6dfd6-201">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6dfd6-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6dfd6-203">a.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-203">a.</span></span> <span data-ttu-id="6dfd6-204">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6dfd6-205">b.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-205">b.</span></span> <span data-ttu-id="6dfd6-206">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6dfd6-207">c.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-207">c.</span></span> <span data-ttu-id="6dfd6-208">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6dfd6-209">d.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-209">d.</span></span> <span data-ttu-id="6dfd6-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="6dfd6-211">Como criar um usuário de teste DigiCert</span><span class="sxs-lookup"><span data-stu-id="6dfd6-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="6dfd6-212">Nesta seção, você criará um usuário chamado Brenda Fernandes no DigiCert.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="6dfd6-213">Trabalhe com [DigiCert a equipe de suporte](mailto:support@digicert.com) tooadd usuários Olá DigiCert.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-213">Please work with [DigiCert support team](mailto:support@digicert.com) tooadd hello users in DigiCert.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6dfd6-214">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6dfd6-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6dfd6-215">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooDigiCert.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDigiCert.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="6dfd6-217">**tooassign Britta Simon tooDigiCert, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6dfd6-217">**tooassign Britta Simon tooDigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="6dfd6-218">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="6dfd6-220">Na lista de aplicativos hello, selecione **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-220">In hello applications list, select **DigiCert**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="6dfd6-222">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="6dfd6-224">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-224">Click **Add** button.</span></span> <span data-ttu-id="6dfd6-225">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="6dfd6-227">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6dfd6-228">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6dfd6-229">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6dfd6-230">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="6dfd6-230">Testing single sign-on</span></span>

<span data-ttu-id="6dfd6-231">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6dfd6-232">Quando você clica em bloco DigiCert Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour DeigiCert aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6dfd6-232">When you click hello DigiCert tile in hello Access Panel, you should get automatically signed-on tooyour DeigiCert application.</span></span>
<span data-ttu-id="6dfd6-233">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6dfd6-233">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6dfd6-234">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6dfd6-234">Additional resources</span></span>

* [<span data-ttu-id="6dfd6-235">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6dfd6-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6dfd6-236">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6dfd6-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

