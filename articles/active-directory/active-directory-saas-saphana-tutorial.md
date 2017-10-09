---
title: "Tutorial: integração do Azure Active Directory com o SAP HANA | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="a88d0-103">Tutorial: integração do Azure Active Directory com o SAP HANA</span><span class="sxs-lookup"><span data-stu-id="a88d0-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="a88d0-104">Neste tutorial, você aprenderá como toointegrate SAP HANA com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="a88d0-104">In this tutorial, you learn how toointegrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a88d0-105">Integração do SAP HANA com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="a88d0-105">Integrating SAP HANA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a88d0-106">Você pode controlar no AD do Azure que tenha acesso tooSAP HANA</span><span class="sxs-lookup"><span data-stu-id="a88d0-106">You can control in Azure AD who has access tooSAP HANA</span></span>
- <span data-ttu-id="a88d0-107">Você pode habilitar seu usuários tooautomatically get conectado tooSAP HANA (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a88d0-107">You can enable your users tooautomatically get signed-on tooSAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a88d0-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a88d0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a88d0-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a88d0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a88d0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a88d0-110">Prerequisites</span></span>

<span data-ttu-id="a88d0-111">tooconfigure integração do AD do Azure com o SAP HANA, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="a88d0-111">tooconfigure Azure AD integration with SAP HANA, you need hello following items:</span></span>

- <span data-ttu-id="a88d0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a88d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a88d0-113">Uma assinatura do SAP HANA habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="a88d0-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="a88d0-114">Uma instância do HANA em execução, seja em qualquer IaaS público, local, em VMs do Azure ou em grandes instâncias SAP no Azure</span><span class="sxs-lookup"><span data-stu-id="a88d0-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="a88d0-115">Olá XSA administração da Web Interface, bem como HANA Studio instalado na instância do HANA hello.</span><span class="sxs-lookup"><span data-stu-id="a88d0-115">hello XSA Administration Web Interface as well as HANA Studio installed on hello HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="a88d0-116">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="a88d0-116">tootest hello steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="a88d0-117">Teste a integração de saudação primeiro em desenvolvimento ou ambiente de aplicativo hello e, em seguida, ambiente de produção de hello do uso de preparo.</span><span class="sxs-lookup"><span data-stu-id="a88d0-117">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="a88d0-118">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a88d0-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a88d0-119">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a88d0-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a88d0-120">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a88d0-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a88d0-121">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a88d0-121">Scenario description</span></span>
<span data-ttu-id="a88d0-122">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a88d0-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a88d0-123">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="a88d0-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a88d0-124">Adicionando SAP HANA da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a88d0-124">Adding SAP HANA from hello gallery</span></span>
2. <span data-ttu-id="a88d0-125">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a88d0-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-hello-gallery"></a><span data-ttu-id="a88d0-126">Adicionando SAP HANA da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a88d0-126">Adding SAP HANA from hello gallery</span></span>
<span data-ttu-id="a88d0-127">integração de saudação tooconfigure do SAP HANA no AD do Azure, você precisa tooadd SAP HANA na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a88d0-127">tooconfigure hello integration of SAP HANA into Azure AD, you need tooadd SAP HANA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a88d0-128">**tooadd SAP HANA na Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a88d0-128">**tooadd SAP HANA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a88d0-129">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a88d0-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="a88d0-131">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a88d0-132">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-132">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="a88d0-134">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a88d0-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="a88d0-136">Na caixa de pesquisa hello, digite **SAP HANA**, selecione **SAP HANA** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a88d0-136">In hello search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button tooadd hello application.</span></span> 

    ![Olá novo aplicativo](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a88d0-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a88d0-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a88d0-139">Nesta seção, você configurará e testará o logon único do Azure AD com o SAP HANA, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a88d0-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a88d0-140">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SAP HANA é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a88d0-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA is tooa user in Azure AD.</span></span> <span data-ttu-id="a88d0-141">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no SAP HANA deve toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a88d0-141">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA needs toobe established.</span></span>

<span data-ttu-id="a88d0-142">SAP HANA, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="a88d0-142">In SAP HANA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a88d0-143">tooconfigure e teste de logon único do AD do Azure com o SAP HANA, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="a88d0-143">tooconfigure and test Azure AD single sign-on with SAP HANA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a88d0-144">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a88d0-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a88d0-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a88d0-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a88d0-146">**[Criar um usuário de teste do SAP HANA](#creating-a-sap-hana-test-user)**  -toohave um equivalente do Britta Simon no SAP HANA é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="a88d0-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - toohave a counterpart of Britta Simon in SAP HANA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a88d0-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="a88d0-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a88d0-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="a88d0-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a88d0-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a88d0-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a88d0-150">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="a88d0-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="a88d0-151">**tooconfigure AD do Azure-logon único com o SAP HANA, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a88d0-151">**tooconfigure Azure AD single sign-on with SAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="a88d0-152">Em Olá portal do Azure, Olá **SAP HANA** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-152">In hello Azure portal, on hello **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a88d0-154">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="a88d0-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="a88d0-156">Em Olá **URLs e SAP HANA domínio** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a88d0-156">On hello **SAP HANA Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="a88d0-158">a.</span><span class="sxs-lookup"><span data-stu-id="a88d0-158">a.</span></span> <span data-ttu-id="a88d0-159">Em Olá **identificador** caixa de texto, tipo:`HA100`</span><span class="sxs-lookup"><span data-stu-id="a88d0-159">In hello **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="a88d0-160">b.</span><span class="sxs-lookup"><span data-stu-id="a88d0-160">b.</span></span> <span data-ttu-id="a88d0-161">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="a88d0-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a88d0-162">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="a88d0-162">These values are not real.</span></span> <span data-ttu-id="a88d0-163">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="a88d0-163">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="a88d0-164">Entre em contato com [equipe de suporte do cliente do SAP HANA](https://cloudplatform.sap.com/contact.html) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="a88d0-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="a88d0-165">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a88d0-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="a88d0-167">Se o certificado não está ativo, em seguida, ativá-lo clicando Olá caixa de seleção "Criar novo certificado active" na saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a88d0-167">If certificate is not active then make it active by clicking hello “Make new certificate active” checkbox in hello Azure AD.</span></span> 

5. <span data-ttu-id="a88d0-168">Aplicativos do SAP HANA espera as asserções de SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="a88d0-168">SAP HANA application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="a88d0-169">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="a88d0-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="a88d0-170">Aqui nós mapeou hello **identificador de usuário** com **ExtractMailPrefix()** função de **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-170">Here we have mapped hello **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="a88d0-171">Isso retorna o valor de prefixo de saudação de email do usuário de saudação que é Olá ID exclusivo do usuário.</span><span class="sxs-lookup"><span data-stu-id="a88d0-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="a88d0-172">Isto é enviado toohello aplicativo SAP HANA em cada resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="a88d0-172">This is sent toohello SAP HANA application in every successful response.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="a88d0-174">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="a88d0-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="a88d0-175">a.</span><span class="sxs-lookup"><span data-stu-id="a88d0-175">a.</span></span> <span data-ttu-id="a88d0-176">Em Olá **identificador de usuário** lista suspensa, selecione **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-176">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="a88d0-177">b.</span><span class="sxs-lookup"><span data-stu-id="a88d0-177">b.</span></span> <span data-ttu-id="a88d0-178">Em Olá **Mail** lista suspensa, selecione **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-178">In hello **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="a88d0-179">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a88d0-179">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="a88d0-181">tooconfigure logon único no **SAP HANA** lado, o logon tooyour **HANA XSA Web Console** navegando toohello respectivo HTTPS-ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="a88d0-181">tooconfigure single sign-on on **SAP HANA** side, login tooyour **HANA XSA Web Console**  by browsing toohello respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="a88d0-182">Na configuração padrão de saudação, Olá URL redireciona Olá solicitação tooa tela de logon, que exige credenciais de saudação de um autenticado SAP HANA banco de dados toocomplete saudação do processo de logon.</span><span class="sxs-lookup"><span data-stu-id="a88d0-182">In hello default configuration, hello URL redirects hello request tooa logon screen, which requires hello credentials of an authenticated SAP HANA database user toocomplete hello logon process.</span></span> <span data-ttu-id="a88d0-183">usuário Olá que fizer logon deve ter tarefas de administração do hello privilégios necessários tooperform SAML.</span><span class="sxs-lookup"><span data-stu-id="a88d0-183">hello user who logs on must have hello privileges required tooperform SAML administration tasks.</span></span>

9. <span data-ttu-id="a88d0-184">Olá XSA a Interface da Web, navegar muito**provedor de identidade SAML** e clique Olá **"+"** -botão na parte inferior de saudação do painel de adicionar informações de provedor de identidade do hello tela toodisplay hello e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a88d0-184">In hello XSA Web Interface, navigate too**SAML Identity Provider** and from there, click hello **“+”** -button on hello bottom of hello screen toodisplay hello Add Identity Provider Info pane and perform hello following steps:</span></span>

    ![Adicionar Provedor de Identidade](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="a88d0-186">a.</span><span class="sxs-lookup"><span data-stu-id="a88d0-186">a.</span></span> <span data-ttu-id="a88d0-187">Em Olá **adicionar informações do provedor de identidade** painel, colar conteúdo Olá Olá Metadata XML, que você baixou do portal do Azure em Olá **metadados** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a88d0-187">In hello **Add Identity Provider Info** pane, paste hello contents of hello Metadata XML, which you have downloaded from Azure portal into hello **Metadata** textbox.</span></span>

    ![Configurações para Adicionar Provedor de Identidade](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="a88d0-189">b.</span><span class="sxs-lookup"><span data-stu-id="a88d0-189">b.</span></span> <span data-ttu-id="a88d0-190">Se o conteúdo de saudação do documento XML de saudação for válido, Olá análise processo extrai Olá informações necessárias tooinsert Olá **assunto, ID de entidade e emissor** campos Olá geral dados área da tela e Olá campos URL Olá Área de tela de destino, por exemplo,  **URL Base e a URL de logon único (*)**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-190">If hello contents of hello XML document are valid, hello parsing process extracts hello information required tooinsert into hello **Subject, Entity ID, and Issuer** fields in hello General Data screen area, and hello URL fields in hello Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Configurações para Adicionar Provedor de Identidade](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="a88d0-192">c.</span><span class="sxs-lookup"><span data-stu-id="a88d0-192">c.</span></span> <span data-ttu-id="a88d0-193">Na caixa de nome de saudação da saudação geral dados área da tela, insira um nome para o novo provedor de identidade SAML SSO hello.</span><span class="sxs-lookup"><span data-stu-id="a88d0-193">In hello Name box of hello General Data screen area, enter a name for hello new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="a88d0-194">nome de saudação do hello IDP SAML é obrigatório e deve ser exclusiva. ele aparece na lista de saudação do IDPs SAML disponível que é exibida, se selecionar o SAML como método de autenticação de saudação do SAP HANA XS aplicativos toouse, por exemplo, na área de tela de autenticação Olá Olá XS artefato da ferramenta de administração.</span><span class="sxs-lookup"><span data-stu-id="a88d0-194">hello name of hello SAML IDP is mandatory and must be unique; it appears in hello list of available SAML IDPs that is displayed, if you select SAML as hello authentication method for SAP HANA XS applications toouse, for example, in hello Authentication screen area of hello XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="a88d0-195">Salve os detalhes de saudação do novo provedor de identidade SAML hello.</span><span class="sxs-lookup"><span data-stu-id="a88d0-195">Save hello details of hello new SAML identity provider.</span></span> <span data-ttu-id="a88d0-196">Escolha **salvar** toosave Olá detalhes do provedor de identidade SAML hello e adicionar Olá nova lista de IDP SAML toohello de IDPs de SAML conhecidos.</span><span class="sxs-lookup"><span data-stu-id="a88d0-196">Choose **Save** toosave hello details of hello SAML identity provider and add hello new SAML IDP toohello list of known SAML IDPs.</span></span>

    ![botão salvar](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="a88d0-198">No Studio HANA em Propriedades do sistema de saudação do hello **configuração** guia, apenas as configurações de filtro **saml** e ajuste Olá **assertion_timeout** de **10 segundos** muito**120 s**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-198">In HANA Studio within hello system properties of hello **Configuration** tab, just filter settings by **saml** and adjust hello **assertion_timeout** from **10 sec** too**120 sec**.</span></span>

    ![configuração assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="a88d0-200">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="a88d0-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a88d0-201">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="a88d0-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a88d0-202">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a88d0-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a88d0-203">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a88d0-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="a88d0-204">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a88d0-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a88d0-206">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a88d0-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a88d0-207">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a88d0-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a88d0-209">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a88d0-211">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a88d0-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botão Adicionar de saudação](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a88d0-213">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a88d0-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a88d0-215">a.</span><span class="sxs-lookup"><span data-stu-id="a88d0-215">a.</span></span> <span data-ttu-id="a88d0-216">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a88d0-217">b.</span><span class="sxs-lookup"><span data-stu-id="a88d0-217">b.</span></span> <span data-ttu-id="a88d0-218">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a88d0-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a88d0-219">c.</span><span class="sxs-lookup"><span data-stu-id="a88d0-219">c.</span></span> <span data-ttu-id="a88d0-220">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a88d0-221">d.</span><span class="sxs-lookup"><span data-stu-id="a88d0-221">d.</span></span> <span data-ttu-id="a88d0-222">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="a88d0-223">Criação de um usuário de teste SAP HANA</span><span class="sxs-lookup"><span data-stu-id="a88d0-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="a88d0-224">tooenable AD do Azure usuários toolog em tooSAP HANA, eles devem ser provisionados no SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="a88d0-224">tooenable Azure AD users toolog in tooSAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="a88d0-225">O SAP HANA dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="a88d0-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a88d0-226">Se você precisar toocreate um usuário manualmente, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a88d0-226">If you need toocreate a user manually, perform hello following steps:</span></span>

>[!Note]
><span data-ttu-id="a88d0-227">Você pode alterar autenticação externa de saudação usada pelo usuário hello.</span><span class="sxs-lookup"><span data-stu-id="a88d0-227">You can change hello external authentication used by hello user.</span></span>
<span data-ttu-id="a88d0-228">Os usuários externos são autenticados usando um sistema externo, por exemplo, um sistema Kerberos.</span><span class="sxs-lookup"><span data-stu-id="a88d0-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="a88d0-229">Para obter informações detalhadas sobre identidades externas, contate seu [administrador de domínio](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="a88d0-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="a88d0-230">Olá abrir [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) como um administrador e habilitar hello usuário de banco de dados para o SSO do SAML.</span><span class="sxs-lookup"><span data-stu-id="a88d0-230">Open hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable hello DB-User for SAML SSO.</span></span>

    ![criar usuário](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="a88d0-232">Escala Olá invisível da caixa de seleção toohello à esquerda do **SAML** e siga o link de configurar hello.</span><span class="sxs-lookup"><span data-stu-id="a88d0-232">Tick hello invisible checkbox toohello left of **SAML** and follow hello Configure link.</span></span>

3. <span data-ttu-id="a88d0-233">Clique em **adicionar** tooadd Olá IDP SAML e clique em **Okey** selecionando Olá SAML IDP apropriado.</span><span class="sxs-lookup"><span data-stu-id="a88d0-233">Click **Add** tooadd hello SAML IDP and click **OK** selecting hello appropriate SAML IDP.</span></span>

4. <span data-ttu-id="a88d0-234">Adicionar Olá **identidade externa** (ex.</span><span class="sxs-lookup"><span data-stu-id="a88d0-234">Add hello **External Identity** (ex.</span></span> <span data-ttu-id="a88d0-235">BrendaFernandes aqui) ou escolha **"Qualquer"** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="a88d0-236">Se "Qualquer" caixa de seleção não estiver marcada, o nome de usuário de saudação em HANA precisa tooexactly nome de saudação de correspondência de usuário Olá Olá UPN antes de sufixo de domínio de saudação (ou seja, BrittaSimon@contoso.com seria BrittaSimon em HANA).</span><span class="sxs-lookup"><span data-stu-id="a88d0-236">If "ANY" check-box is not checked, then hello user name in HANA needs tooexactly match hello name of hello user in hello UPN before hello domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="a88d0-237">Para fins de teste, atribuir todos **"XS"** usuário de toohello de funções.</span><span class="sxs-lookup"><span data-stu-id="a88d0-237">For testing purposes, assign all **"XS"** roles toohello user.</span></span>

    ![atribuição de funções](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="a88d0-239">Você deve conceder apenas as permissões apropriadas para seus casos de uso.</span><span class="sxs-lookup"><span data-stu-id="a88d0-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="a88d0-240">Salve Olá de usuário.</span><span class="sxs-lookup"><span data-stu-id="a88d0-240">Save hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a88d0-241">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a88d0-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a88d0-242">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSAP HANA.</span><span class="sxs-lookup"><span data-stu-id="a88d0-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP HANA.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="a88d0-244">**tooassign Britta Simon tooSAP HANA, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a88d0-244">**tooassign Britta Simon tooSAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="a88d0-245">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a88d0-247">Na lista de aplicativos hello, selecione **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-247">In hello applications list, select **SAP HANA**.</span></span>

    ![Atribuir usuário](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="a88d0-249">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202] 

4. <span data-ttu-id="a88d0-251">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a88d0-251">Click **Add** button.</span></span> <span data-ttu-id="a88d0-252">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a88d0-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="a88d0-254">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="a88d0-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a88d0-255">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a88d0-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a88d0-256">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a88d0-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a88d0-257">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a88d0-257">Testing single sign-on</span></span>

<span data-ttu-id="a88d0-258">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="a88d0-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a88d0-259">Quando você clica em bloco SAP HANA Olá Olá painel de acesso, você deve obter aplicativos do SAP HANA automaticamente assinado em tooyour.</span><span class="sxs-lookup"><span data-stu-id="a88d0-259">When you click hello SAP HANA tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA application.</span></span>
<span data-ttu-id="a88d0-260">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a88d0-260">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a88d0-261">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a88d0-261">Additional resources</span></span>

* [<span data-ttu-id="a88d0-262">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a88d0-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a88d0-263">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a88d0-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

