---
title: "Tutorial: Integração do Azure Active Directory com o eKincare | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e eKincare."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 16129e3384132bb34744aadf088bb65f07ed7a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="df1d2-103">Tutorial: Integração do Azure Active Directory com o eKincare</span><span class="sxs-lookup"><span data-stu-id="df1d2-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="df1d2-104">Neste tutorial, você aprenderá como eKincare toointegrate com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="df1d2-104">In this tutorial, you learn how toointegrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df1d2-105">Integrando eKincare com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="df1d2-105">Integrating eKincare with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="df1d2-106">Você pode controlar no AD do Azure que tenha acesso tooeKincare</span><span class="sxs-lookup"><span data-stu-id="df1d2-106">You can control in Azure AD who has access tooeKincare</span></span>
- <span data-ttu-id="df1d2-107">Você pode habilitar seu usuários tooautomatically get conectado tooeKincare (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df1d2-107">You can enable your users tooautomatically get signed-on tooeKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="df1d2-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="df1d2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="df1d2-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df1d2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df1d2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="df1d2-110">Prerequisites</span></span>

<span data-ttu-id="df1d2-111">tooconfigure integração do AD do Azure com eKincare, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="df1d2-111">tooconfigure Azure AD integration with eKincare, you need hello following items:</span></span>

- <span data-ttu-id="df1d2-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df1d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df1d2-113">Uma assinatura do eKincare com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="df1d2-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="df1d2-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="df1d2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="df1d2-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="df1d2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df1d2-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="df1d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="df1d2-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df1d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="df1d2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="df1d2-118">Scenario description</span></span>
<span data-ttu-id="df1d2-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="df1d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="df1d2-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="df1d2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df1d2-121">Adicionando eKincare da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="df1d2-121">Adding eKincare from hello gallery</span></span>
2. <span data-ttu-id="df1d2-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df1d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-hello-gallery"></a><span data-ttu-id="df1d2-123">Adicionando eKincare da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="df1d2-123">Adding eKincare from hello gallery</span></span>
<span data-ttu-id="df1d2-124">integração de saudação tooconfigure de eKincare no AD do Azure, você precisa eKincare tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="df1d2-124">tooconfigure hello integration of eKincare into Azure AD, you need tooadd eKincare from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="df1d2-125">**eKincare tooadd da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="df1d2-125">**tooadd eKincare from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="df1d2-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="df1d2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="df1d2-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="df1d2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="df1d2-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="df1d2-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="df1d2-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df1d2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="df1d2-133">Na caixa de pesquisa hello, digite **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="df1d2-133">In hello search box, type **eKincare**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="df1d2-135">No painel de resultados de saudação, selecione **eKincare**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="df1d2-135">In hello results panel, select **eKincare**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="df1d2-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df1d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="df1d2-138">Nesta seção, você configurará e testará o logon único do Azure AD com o eKincare, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="df1d2-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="df1d2-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em eKincare é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="df1d2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eKincare is tooa user in Azure AD.</span></span> <span data-ttu-id="df1d2-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em eKincare precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="df1d2-140">In other words, a link relationship between an Azure AD user and hello related user in eKincare needs toobe established.</span></span>

<span data-ttu-id="df1d2-141">EKincare, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="df1d2-141">In eKincare, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="df1d2-142">tooconfigure e teste de logon único do AD do Azure com eKincare, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="df1d2-142">tooconfigure and test Azure AD single sign-on with eKincare, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="df1d2-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="df1d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="df1d2-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df1d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df1d2-145">**[Criar um usuário de teste eKincare](#creating-a-ekincare-test-user)**  -toohave um equivalente do Britta Simon em eKincare é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="df1d2-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - toohave a counterpart of Britta Simon in eKincare that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="df1d2-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="df1d2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df1d2-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="df1d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="df1d2-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="df1d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="df1d2-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo eKincare.</span><span class="sxs-lookup"><span data-stu-id="df1d2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="df1d2-150">**tooconfigure AD do Azure-logon único com eKincare, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="df1d2-150">**tooconfigure Azure AD single sign-on with eKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="df1d2-151">Em Olá portal do Azure, Olá **eKincare** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="df1d2-151">In hello Azure portal, on hello **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="df1d2-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="df1d2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="df1d2-155">Em Olá **eKincare domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="df1d2-155">On hello **eKincare Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="df1d2-157">a.</span><span class="sxs-lookup"><span data-stu-id="df1d2-157">a.</span></span> <span data-ttu-id="df1d2-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="df1d2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="df1d2-159">b.</span><span class="sxs-lookup"><span data-stu-id="df1d2-159">b.</span></span> <span data-ttu-id="df1d2-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="df1d2-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="df1d2-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="df1d2-161">These values are not real.</span></span> <span data-ttu-id="df1d2-162">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="df1d2-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="df1d2-163">Entre em contato com [eKincare a equipe de suporte](mailto:tech@ekincare.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="df1d2-163">Contact [eKincare support team](mailto:tech@ekincare.com) tooget these values.</span></span>
 
4. <span data-ttu-id="df1d2-164">aplicativo de eKincare espera asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="df1d2-164">eKincare application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="df1d2-165">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="df1d2-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="df1d2-166">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="df1d2-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="df1d2-167">Olá captura de tela a seguir mostra um exemplo para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="df1d2-167">hello following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="df1d2-168">Olá nome de declaração sempre será **"employeeid"** e o valor de saudação que podemos mapeou toouser.extensionattribute1, que contém employeeid saudação do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="df1d2-168">hello claim name will always be **"employeeid"** and hello value of which we have mapped toouser.extensionattribute1, that contains hello employeeid of hello user.</span></span> <span data-ttu-id="df1d2-169">outras duas declarações Hello nome ou seja</span><span class="sxs-lookup"><span data-stu-id="df1d2-169">hello other two claims' name i.e</span></span> <span data-ttu-id="df1d2-170">**"organizationid"** e **"Nome_da_Organização"** sempre será o mesmo e seus valores contêm detalhes de saudação da organização de saudação do usuário Olá respectivamente.</span><span class="sxs-lookup"><span data-stu-id="df1d2-170">**"organizationid"** and **"organizationname"** will always be same and their values contain hello details of hello organization of hello user respectively.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="df1d2-172">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="df1d2-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="df1d2-173">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="df1d2-173">Attribute Name</span></span> | <span data-ttu-id="df1d2-174">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="df1d2-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="df1d2-175">employeeid</span><span class="sxs-lookup"><span data-stu-id="df1d2-175">employeeid</span></span> | <span data-ttu-id="df1d2-176">*user.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="df1d2-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="df1d2-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="df1d2-177">organizationid</span></span> | <span data-ttu-id="df1d2-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="df1d2-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="df1d2-179">organizationname</span><span class="sxs-lookup"><span data-stu-id="df1d2-179">organizationname</span></span> | <span data-ttu-id="df1d2-180">*user.companyname*</span><span class="sxs-lookup"><span data-stu-id="df1d2-180">*user.companyname*</span></span> |

    <span data-ttu-id="df1d2-181">a.</span><span class="sxs-lookup"><span data-stu-id="df1d2-181">a.</span></span> <span data-ttu-id="df1d2-182">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df1d2-182">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="df1d2-185">b.</span><span class="sxs-lookup"><span data-stu-id="df1d2-185">b.</span></span> <span data-ttu-id="df1d2-186">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="df1d2-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="df1d2-187">c.</span><span class="sxs-lookup"><span data-stu-id="df1d2-187">c.</span></span> <span data-ttu-id="df1d2-188">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="df1d2-188">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="df1d2-189">d.</span><span class="sxs-lookup"><span data-stu-id="df1d2-189">d.</span></span> <span data-ttu-id="df1d2-190">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="df1d2-190">Click **Ok**</span></span>

6. <span data-ttu-id="df1d2-191">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="df1d2-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="df1d2-193">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="df1d2-193">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="df1d2-195">tooconfigure logon único no **eKincare** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte eKincare](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="df1d2-195">tooconfigure single sign-on on **eKincare** side, you need toosend hello downloaded **Metadata XML** too[eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="df1d2-196">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="df1d2-196">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="df1d2-197">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="df1d2-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="df1d2-198">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="df1d2-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="df1d2-199">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="df1d2-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="df1d2-200">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df1d2-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="df1d2-201">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="df1d2-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="df1d2-203">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="df1d2-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="df1d2-204">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="df1d2-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="df1d2-206">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="df1d2-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="df1d2-208">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="df1d2-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="df1d2-210">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="df1d2-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="df1d2-212">a.</span><span class="sxs-lookup"><span data-stu-id="df1d2-212">a.</span></span> <span data-ttu-id="df1d2-213">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df1d2-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="df1d2-214">b.</span><span class="sxs-lookup"><span data-stu-id="df1d2-214">b.</span></span> <span data-ttu-id="df1d2-215">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="df1d2-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="df1d2-216">c.</span><span class="sxs-lookup"><span data-stu-id="df1d2-216">c.</span></span> <span data-ttu-id="df1d2-217">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="df1d2-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="df1d2-218">d.</span><span class="sxs-lookup"><span data-stu-id="df1d2-218">d.</span></span> <span data-ttu-id="df1d2-219">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="df1d2-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="df1d2-220">Criar um usuário de teste do eKincare</span><span class="sxs-lookup"><span data-stu-id="df1d2-220">Creating a eKincare test user</span></span>

<span data-ttu-id="df1d2-221">Aplicativo dá suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação são criados automaticamente no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="df1d2-221">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="df1d2-222">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="df1d2-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="df1d2-223">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooeKincare.</span><span class="sxs-lookup"><span data-stu-id="df1d2-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeKincare.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="df1d2-225">**tooassign Britta Simon tooeKincare, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="df1d2-225">**tooassign Britta Simon tooeKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="df1d2-226">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="df1d2-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="df1d2-228">Na lista de aplicativos hello, selecione **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="df1d2-228">In hello applications list, select **eKincare**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="df1d2-230">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="df1d2-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="df1d2-232">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="df1d2-232">Click **Add** button.</span></span> <span data-ttu-id="df1d2-233">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df1d2-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="df1d2-235">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="df1d2-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="df1d2-236">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df1d2-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="df1d2-237">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df1d2-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="df1d2-238">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="df1d2-238">Testing single sign-on</span></span>

<span data-ttu-id="df1d2-239">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="df1d2-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="df1d2-240">Quando você clica em bloco eKincare Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour eKincare aplicativo.</span><span class="sxs-lookup"><span data-stu-id="df1d2-240">When you click hello eKincare tile in hello Access Panel, you should get automatically signed-on tooyour eKincare application.</span></span>
<span data-ttu-id="df1d2-241">Para obter mais informações sobre o painel de acesso, consulte [Introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="df1d2-241">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="df1d2-242">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="df1d2-242">Additional resources</span></span>

* [<span data-ttu-id="df1d2-243">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="df1d2-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df1d2-244">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="df1d2-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

