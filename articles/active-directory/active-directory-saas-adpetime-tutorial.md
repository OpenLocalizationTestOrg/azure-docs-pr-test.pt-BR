---
title: "Tutorial: integração do Azure Active Directory com o ADP eTime | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e eTime ADP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="43274-103">Tutorial: integração do Azure Active Directory ao ADP eTime</span><span class="sxs-lookup"><span data-stu-id="43274-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="43274-104">Neste tutorial, você aprenderá como eTime toointegrate ADP com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="43274-104">In this tutorial, you learn how toointegrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="43274-105">Integrando ADP eTime com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="43274-105">Integrating ADP eTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="43274-106">Você pode controlar no AD do Azure que tenha acesso tooADP eTime</span><span class="sxs-lookup"><span data-stu-id="43274-106">You can control in Azure AD who has access tooADP eTime</span></span>
- <span data-ttu-id="43274-107">Você pode habilitar seu usuários tooautomatically get conectado tooADP eTime (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="43274-107">You can enable your users tooautomatically get signed-on tooADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="43274-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="43274-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="43274-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="43274-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43274-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="43274-110">Prerequisites</span></span>

<span data-ttu-id="43274-111">tooconfigure integração do AD do Azure com ADP eTime, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="43274-111">tooconfigure Azure AD integration with ADP eTime, you need hello following items:</span></span>

- <span data-ttu-id="43274-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="43274-112">An Azure AD subscription</span></span>
- <span data-ttu-id="43274-113">Uma assinatura habilitada para logon único do ADP eTime</span><span class="sxs-lookup"><span data-stu-id="43274-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="43274-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="43274-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="43274-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="43274-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="43274-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="43274-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="43274-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43274-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="43274-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="43274-118">Scenario description</span></span>
<span data-ttu-id="43274-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="43274-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="43274-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="43274-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="43274-121">Adicionando ADP eTime da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="43274-121">Adding ADP eTime from hello gallery</span></span>
2. <span data-ttu-id="43274-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="43274-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-hello-gallery"></a><span data-ttu-id="43274-123">Adicionando ADP eTime da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="43274-123">Adding ADP eTime from hello gallery</span></span>
<span data-ttu-id="43274-124">integração de saudação tooconfigure da ADP eTime no AD do Azure, você precisa tooadd ADP eTime da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="43274-124">tooconfigure hello integration of ADP eTime into Azure AD, you need tooadd ADP eTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="43274-125">**eTime tooadd ADP da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="43274-125">**tooadd ADP eTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="43274-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="43274-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="43274-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="43274-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="43274-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="43274-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="43274-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="43274-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="43274-133">Na caixa de pesquisa hello, digite **eTime ADP**.</span><span class="sxs-lookup"><span data-stu-id="43274-133">In hello search box, type **ADP eTime**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="43274-135">No painel de resultados de saudação, selecione **ADP eTime**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="43274-135">In hello results panel, select **ADP eTime**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="43274-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="43274-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="43274-138">Nesta seção, você configura e testa o logon único do Azure AD com o ADP eTime, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="43274-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="43274-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em ADP eTime é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="43274-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP eTime is tooa user in Azure AD.</span></span> <span data-ttu-id="43274-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em ADP eTime precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="43274-140">In other words, a link relationship between an Azure AD user and hello related user in ADP eTime needs toobe established.</span></span>

<span data-ttu-id="43274-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="43274-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP eTime.</span></span>

<span data-ttu-id="43274-142">tooconfigure e teste de logon único do AD do Azure com ADP eTime, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="43274-142">tooconfigure and test Azure AD single sign-on with ADP eTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="43274-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="43274-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="43274-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43274-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="43274-145">**[Criar um usuário de teste ADP eTime](#creating-an-adp-etime-test-user)**  -toohave uma duplicata de Britta Simon em ADP eTime que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="43274-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - toohave a counterpart of Britta Simon in ADP eTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="43274-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="43274-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="43274-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="43274-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="43274-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="43274-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="43274-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="43274-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="43274-150">**tooconfigure AD do Azure-logon único com ADP eTime, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="43274-150">**tooconfigure Azure AD single sign-on with ADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="43274-151">Em Olá portal do Azure, Olá **ADP eTime** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="43274-151">In hello Azure portal, on hello **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="43274-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="43274-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="43274-155">Em Olá **eTime ADP domínio e URLs** , execute Olá etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="43274-155">On hello **ADP eTime Domain and URLs** section, perform hello following step:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="43274-157">a.</span><span class="sxs-lookup"><span data-stu-id="43274-157">a.</span></span> <span data-ttu-id="43274-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="43274-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="43274-159">b.</span><span class="sxs-lookup"><span data-stu-id="43274-159">b.</span></span> <span data-ttu-id="43274-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="43274-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="43274-161">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="43274-161">These values are not hello real.</span></span> <span data-ttu-id="43274-162">Atualize esses valores com URL de resposta real hello e o identificador.</span><span class="sxs-lookup"><span data-stu-id="43274-162">Update these values with hello actual Reply URL and Identifier.</span></span> <span data-ttu-id="43274-163">Entre em contato com [a equipe de suporte ADP eTime](https://www.adp.com/contact-us/overview.aspx) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="43274-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooget these values.</span></span>

4. <span data-ttu-id="43274-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="43274-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="43274-166">Olá aplicativo de eTime ADP espera as asserções de SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML.</span><span class="sxs-lookup"><span data-stu-id="43274-166">hello ADP eTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="43274-167">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="43274-167">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="43274-168">Olá nome de declaração sempre será **"PersonImmutableID"** e o valor de saudação do qual estamos mapeou tooExtensionAttribute2 que contém Olá EmployeeID do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="43274-168">hello claim name will always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2 which contains hello EmployeeID of hello user.</span></span> 

    <span data-ttu-id="43274-169">Aqui será feito mapeamento de usuário de saudação do AD do Azure tooADP eTime Olá EmployeeID, mas você pode mapear esse valor diferente de tooa também com base nas suas configurações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43274-169">Here hello user mapping from Azure AD tooADP eTime will be done on hello EmployeeID but you can map this tooa different value also based on your application settings.</span></span> <span data-ttu-id="43274-170">Portanto, o trabalho com [a equipe de suporte ADP eTime](https://www.adp.com/contact-us/overview.aspx) toouse primeiro Olá identificador correto de um usuário e mapear esse valor com hello **"PersonImmutableID"** de declaração.</span><span class="sxs-lookup"><span data-stu-id="43274-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="43274-172">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="43274-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="43274-173">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="43274-173">Attribute Name</span></span> | <span data-ttu-id="43274-174">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="43274-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="43274-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="43274-175">PersonImmutableID</span></span> | <span data-ttu-id="43274-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="43274-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="43274-177">a.</span><span class="sxs-lookup"><span data-stu-id="43274-177">a.</span></span> <span data-ttu-id="43274-178">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="43274-178">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="43274-181">b.</span><span class="sxs-lookup"><span data-stu-id="43274-181">b.</span></span> <span data-ttu-id="43274-182">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="43274-182">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="43274-183">c.</span><span class="sxs-lookup"><span data-stu-id="43274-183">c.</span></span> <span data-ttu-id="43274-184">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="43274-184">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="43274-185">d.</span><span class="sxs-lookup"><span data-stu-id="43274-185">d.</span></span> <span data-ttu-id="43274-186">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="43274-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="43274-187">Antes de configurar de asserção SAML hello, você precisa toocontact seu [a equipe de suporte eTime ADP](https://www.adp.com/contact-us/overview.aspx) e solicitar o valor de saudação do atributo de identificador exclusivo de saudação para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="43274-187">Before you can configure hello SAML assertion, you need toocontact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="43274-188">Você precisa esta declaração valor tooconfigure Olá personalizado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43274-188">You need this value tooconfigure hello custom claim for your application.</span></span> 

7. <span data-ttu-id="43274-189">Em Olá **eTime ADP configuração** seção, clique em **configurar ADP eTime** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="43274-189">On hello **ADP eTime Configuration** section, click **Configure ADP eTime** tooopen **Configure sign-on** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="43274-191">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="43274-191">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="43274-193">tooconfigure logon único no **ADP eTime** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte ADP eTime](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="43274-193">tooconfigure single sign-on on **ADP eTime** side, you need toosend hello downloaded **Metadata XML** too[ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="43274-194">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="43274-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="43274-195">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="43274-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="43274-196">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="43274-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="43274-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="43274-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="43274-198">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="43274-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="43274-200">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="43274-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="43274-201">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="43274-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="43274-203">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="43274-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="43274-205">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="43274-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="43274-207">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="43274-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="43274-209">a.</span><span class="sxs-lookup"><span data-stu-id="43274-209">a.</span></span> <span data-ttu-id="43274-210">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="43274-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="43274-211">b.</span><span class="sxs-lookup"><span data-stu-id="43274-211">b.</span></span> <span data-ttu-id="43274-212">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="43274-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="43274-213">c.</span><span class="sxs-lookup"><span data-stu-id="43274-213">c.</span></span> <span data-ttu-id="43274-214">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="43274-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="43274-215">d.</span><span class="sxs-lookup"><span data-stu-id="43274-215">d.</span></span> <span data-ttu-id="43274-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="43274-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="43274-217">Criando um usuário de teste do ADP eTime</span><span class="sxs-lookup"><span data-stu-id="43274-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="43274-218">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="43274-218">hello objective of this section is toocreate a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="43274-219">Trabalhar com [a equipe de suporte ADP eTime](https://www.adp.com/contact-us/overview.aspx) tooadd usuários de saudação na conta de eTime Olá ADP.</span><span class="sxs-lookup"><span data-stu-id="43274-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP eTime account.</span></span> 
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="43274-220">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="43274-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="43274-221">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooADP eTime.</span><span class="sxs-lookup"><span data-stu-id="43274-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP eTime.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="43274-223">**tooassign Britta Simon tooADP eTime, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="43274-223">**tooassign Britta Simon tooADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="43274-224">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="43274-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="43274-226">Na lista de aplicativos hello, selecione **eTime ADP**.</span><span class="sxs-lookup"><span data-stu-id="43274-226">In hello applications list, select **ADP eTime**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="43274-228">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="43274-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="43274-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="43274-230">Click **Add** button.</span></span> <span data-ttu-id="43274-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="43274-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="43274-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="43274-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="43274-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="43274-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="43274-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="43274-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="43274-236">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="43274-236">Testing single sign-on</span></span>

<span data-ttu-id="43274-237">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="43274-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="43274-238">Quando você clica em eTime bloco ADP Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour ADP eTime aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43274-238">When you click hello ADP eTime tile in hello Access Panel, you should get automatically signed-on tooyour ADP eTime application.</span></span>
<span data-ttu-id="43274-239">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="43274-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="43274-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="43274-240">Additional resources</span></span>

* [<span data-ttu-id="43274-241">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="43274-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="43274-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="43274-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

