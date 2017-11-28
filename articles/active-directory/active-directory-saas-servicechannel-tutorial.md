---
title: "Tutorial: integração do Azure Active Directory com o ServiceChannel | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="8458a-103">Tutorial: integração do Azure Active Directory com o ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="8458a-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="8458a-104">Neste tutorial, você aprenderá como toointegrate ServiceChannel com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="8458a-104">In this tutorial, you learn how toointegrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8458a-105">Integrando ServiceChannel com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="8458a-105">Integrating ServiceChannel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8458a-106">Você pode controlar no AD do Azure que tenha acesso tooServiceChannel</span><span class="sxs-lookup"><span data-stu-id="8458a-106">You can control in Azure AD who has access tooServiceChannel</span></span>
- <span data-ttu-id="8458a-107">Você pode habilitar seu usuários tooautomatically get conectado tooServiceChannel (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8458a-107">You can enable your users tooautomatically get signed-on tooServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8458a-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="8458a-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="8458a-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8458a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8458a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8458a-110">Prerequisites</span></span>

<span data-ttu-id="8458a-111">tooconfigure integração do AD do Azure com ServiceChannel, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="8458a-111">tooconfigure Azure AD integration with ServiceChannel, you need hello following items:</span></span>

- <span data-ttu-id="8458a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8458a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8458a-113">Uma assinatura do ServiceChannel habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="8458a-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8458a-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8458a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8458a-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8458a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8458a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8458a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8458a-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8458a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8458a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8458a-118">Scenario description</span></span>
<span data-ttu-id="8458a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8458a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8458a-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="8458a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8458a-121">Adicionando ServiceChannel da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8458a-121">Adding ServiceChannel from hello gallery</span></span>
2. <span data-ttu-id="8458a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8458a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-hello-gallery"></a><span data-ttu-id="8458a-123">Adicionando ServiceChannel da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8458a-123">Adding ServiceChannel from hello gallery</span></span>
<span data-ttu-id="8458a-124">integração de saudação tooconfigure de ServiceChannel no AD do Azure, você precisa tooadd ServiceChannel da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8458a-124">tooconfigure hello integration of ServiceChannel into Azure AD, you need tooadd ServiceChannel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8458a-125">**tooadd ServiceChannel da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8458a-125">**tooadd ServiceChannel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8458a-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8458a-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8458a-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8458a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8458a-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8458a-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8458a-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8458a-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8458a-133">Na caixa de pesquisa hello, digite **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="8458a-133">In hello search box, type **ServiceChannel**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="8458a-135">No painel de resultados de saudação, selecione **ServiceChannel**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8458a-135">In hello results panel, select **ServiceChannel**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8458a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8458a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8458a-138">Nesta seção, você configurará e testará o logon único do Azure AD com o ServiceChannel, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="8458a-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8458a-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em ServiceChannel é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8458a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceChannel is tooa user in Azure AD.</span></span> <span data-ttu-id="8458a-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em ServiceChannel precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="8458a-140">In other words, a link relationship between an Azure AD user and hello related user in ServiceChannel needs toobe established.</span></span>

<span data-ttu-id="8458a-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="8458a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceChannel.</span></span>

<span data-ttu-id="8458a-142">tooconfigure e teste de logon único do AD do Azure com ServiceChannel, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="8458a-142">tooconfigure and test Azure AD single sign-on with ServiceChannel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8458a-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8458a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8458a-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8458a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8458a-145">**[Criar um usuário de teste de ServiceChannel](#creating-a-servicechannel-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8458a-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="8458a-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="8458a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8458a-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="8458a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8458a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8458a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8458a-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="8458a-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="8458a-150">**tooconfigure AD do Azure-logon único com ServiceChannel, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8458a-150">**tooconfigure Azure AD single sign-on with ServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="8458a-151">No portal de gerenciamento do Azure do hello, no hello **ServiceChannel** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="8458a-151">In hello Azure Management portal, on hello **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8458a-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="8458a-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="8458a-155">Em Olá **ServiceChannel domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8458a-155">On hello **ServiceChannel Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="8458a-157">a.</span><span class="sxs-lookup"><span data-stu-id="8458a-157">a.</span></span> <span data-ttu-id="8458a-158">Em Olá **identificador** texto, o valor do tipo hello como:`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="8458a-158">In hello **Identifier** textbox, type hello value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="8458a-159">b.</span><span class="sxs-lookup"><span data-stu-id="8458a-159">b.</span></span> <span data-ttu-id="8458a-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="8458a-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8458a-161">Observe que esses não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="8458a-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="8458a-162">Você tem tooupdate esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="8458a-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="8458a-163">Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação.</span><span class="sxs-lookup"><span data-stu-id="8458a-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="8458a-164">Entre em contato com [ServiceChannel a equipe de suporte](https://servicechannel.zendesk.com/hc/en-us) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="8458a-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) tooget these values.</span></span>

4. <span data-ttu-id="8458a-165">Seu aplicativo de ServiceChannel espera asserções SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML.</span><span class="sxs-lookup"><span data-stu-id="8458a-165">Your ServiceChannel application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="8458a-166">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="8458a-166">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="8458a-167">**Identificador de nome (identificador de usuário)** é Olá somente declaração obrigatória e o valor de padrão de saudação é **User** mas ServiceChannel espera este toobe mapeada com **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="8458a-167">**NameIdentifier(User Identifier)** is hello only mandatory claim and hello default value is **user.userprincipalname** but ServiceChannel expects this toobe mapped with **user.mail**.</span></span> <span data-ttu-id="8458a-168">Se você estiver planejando tooenable apenas no provisionamento do usuário, você deve adicionar Olá seguintes declarações conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="8458a-168">If you are planning tooenable Just In Time user provisioning, then you should add hello following claims as shown below.</span></span> <span data-ttu-id="8458a-169">**Função** declaração precisa toobe mapeado muito**user.assignedroles** que contém a função de saudação do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="8458a-169">**Role** claim needs toobe mapped too**user.assignedroles** which contains hello role of hello user.</span></span>  

    <span data-ttu-id="8458a-170">Você pode consultar o guia do ServiceChannel [aqui](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) para obter diretrizes sobre declarações.</span><span class="sxs-lookup"><span data-stu-id="8458a-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="8458a-172">Clique em [aqui](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow como tooconfigure **função** no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8458a-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow how tooconfigure **Role** in Azure AD</span></span>

5. <span data-ttu-id="8458a-173">Em **atributos de usuário** seção, clique em **exibir e editar todos os outros atributos de usuário** e definir atributos de saudação.</span><span class="sxs-lookup"><span data-stu-id="8458a-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span>

    | <span data-ttu-id="8458a-174">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="8458a-174">Attribute Name</span></span> | <span data-ttu-id="8458a-175">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="8458a-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="8458a-176">Função</span><span class="sxs-lookup"><span data-stu-id="8458a-176">Role</span></span>| <span data-ttu-id="8458a-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="8458a-177">user.assignedroles</span></span> |

    <span data-ttu-id="8458a-178">a.</span><span class="sxs-lookup"><span data-stu-id="8458a-178">a.</span></span> <span data-ttu-id="8458a-179">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8458a-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="8458a-182">b.</span><span class="sxs-lookup"><span data-stu-id="8458a-182">b.</span></span> <span data-ttu-id="8458a-183">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="8458a-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8458a-184">c.</span><span class="sxs-lookup"><span data-stu-id="8458a-184">c.</span></span> <span data-ttu-id="8458a-185">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="8458a-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8458a-186">d.</span><span class="sxs-lookup"><span data-stu-id="8458a-186">d.</span></span> <span data-ttu-id="8458a-187">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="8458a-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="8458a-188">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8458a-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="8458a-190">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8458a-190">Click **Save**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8458a-192">Em Olá **ServiceChannel configuração** seção, clique em **configurar ServiceChannel** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="8458a-192">On hello **ServiceChannel Configuration** section, click **Configure ServiceChannel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8458a-193">Observação Olá **SAML Enitity ID** de saudação **referência rápida** seção.</span><span class="sxs-lookup"><span data-stu-id="8458a-193">Please note hello **SAML Enitity ID** from hello **Quick Reference** section.</span></span>

9. <span data-ttu-id="8458a-194">tooconfigure logon único no **ServiceChannel** lado, você precisa toosend Olá baixado **certificado (Base64)** e **ID da entidade SAML** muito[ A equipe de suporte ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="8458a-194">tooconfigure single sign-on on **ServiceChannel** side, you need toosend hello downloaded **certificate (Base64)** and **SAML Entity ID** too[ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="8458a-195">Eles serão configurados isso no hello toohave de ordem conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="8458a-195">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8458a-196">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8458a-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="8458a-197">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8458a-197">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8458a-199">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8458a-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8458a-200">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8458a-200">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8458a-202">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="8458a-202">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8458a-204">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8458a-204">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8458a-206">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8458a-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8458a-208">a.</span><span class="sxs-lookup"><span data-stu-id="8458a-208">a.</span></span> <span data-ttu-id="8458a-209">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8458a-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8458a-210">b.</span><span class="sxs-lookup"><span data-stu-id="8458a-210">b.</span></span> <span data-ttu-id="8458a-211">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8458a-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8458a-212">c.</span><span class="sxs-lookup"><span data-stu-id="8458a-212">c.</span></span> <span data-ttu-id="8458a-213">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="8458a-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8458a-214">d.</span><span class="sxs-lookup"><span data-stu-id="8458a-214">d.</span></span> <span data-ttu-id="8458a-215">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8458a-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="8458a-216">Criar um usuário de teste do ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="8458a-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="8458a-217">Aplicativo dá suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação serão criados no aplicativo hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8458a-217">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="8458a-218">Para um provisionamento de usuário completo, entre em contato com [a equipe de suporte do ServiceChannel](https://servicechannel.zendesk.com/hc/en-us)</span><span class="sxs-lookup"><span data-stu-id="8458a-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8458a-219">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8458a-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8458a-220">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooServiceChannel seu acesso.</span><span class="sxs-lookup"><span data-stu-id="8458a-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceChannel.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8458a-222">**tooassign Britta Simon tooServiceChannel, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8458a-222">**tooassign Britta Simon tooServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="8458a-223">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8458a-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8458a-225">Na lista de aplicativos hello, selecione **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="8458a-225">In hello applications list, select **ServiceChannel**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="8458a-227">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8458a-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8458a-229">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8458a-229">Click **Add** button.</span></span> <span data-ttu-id="8458a-230">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8458a-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8458a-232">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="8458a-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8458a-233">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8458a-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8458a-234">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8458a-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8458a-235">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8458a-235">Testing single sign-on</span></span>

<span data-ttu-id="8458a-236">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="8458a-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8458a-237">Quando você clica em bloco ServiceChannel Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour ServiceChannel aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8458a-237">When you click hello ServiceChannel tile in hello Access Panel, you should get automatically signed-on tooyour ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8458a-238">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8458a-238">Additional resources</span></span>

* [<span data-ttu-id="8458a-239">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8458a-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8458a-240">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8458a-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png