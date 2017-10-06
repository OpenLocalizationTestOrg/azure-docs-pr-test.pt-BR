---
title: "Tutorial: integração do Azure Active Directory com o M-Files | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e milhões de arquivos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e1d268da53312b1d2c12e29d66b1a5b66d0cdcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="35693-103">Tutorial: integração do Azure Active Directory com o M-Files</span><span class="sxs-lookup"><span data-stu-id="35693-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="35693-104">Neste tutorial, você aprenderá como toointegrate milhões de arquivos com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="35693-104">In this tutorial, you learn how toointegrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35693-105">Integrando milhões de arquivos com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="35693-105">Integrating M-Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="35693-106">Você pode controlar no AD do Azure que tenha acesso tooM arquivos</span><span class="sxs-lookup"><span data-stu-id="35693-106">You can control in Azure AD who has access tooM-Files</span></span>
- <span data-ttu-id="35693-107">Você pode habilitar seus usuários tooautomatically get conectado tooM-arquivos (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="35693-107">You can enable your users tooautomatically get signed-on tooM-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="35693-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="35693-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="35693-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35693-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35693-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="35693-110">Prerequisites</span></span>

<span data-ttu-id="35693-111">tooconfigure integração do AD do Azure com milhões de arquivos, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="35693-111">tooconfigure Azure AD integration with M-Files, you need hello following items:</span></span>

- <span data-ttu-id="35693-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="35693-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35693-113">Uma assinatura habilitada para logon único do M-Files</span><span class="sxs-lookup"><span data-stu-id="35693-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="35693-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="35693-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="35693-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="35693-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35693-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="35693-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="35693-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35693-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35693-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="35693-118">Scenario description</span></span>
<span data-ttu-id="35693-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="35693-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="35693-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="35693-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35693-121">Adicionando arquivos M da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="35693-121">Adding M-Files from hello gallery</span></span>
2. <span data-ttu-id="35693-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="35693-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-hello-gallery"></a><span data-ttu-id="35693-123">Adicionando arquivos M da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="35693-123">Adding M-Files from hello gallery</span></span>
<span data-ttu-id="35693-124">integração de saudação tooconfigure arquivos-M no AD do Azure, você precisa tooadd milhões de arquivos da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="35693-124">tooconfigure hello integration of M-Files into Azure AD, you need tooadd M-Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="35693-125">**tooadd milhões de arquivos da Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="35693-125">**tooadd M-Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="35693-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="35693-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="35693-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="35693-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="35693-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="35693-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="35693-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="35693-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="35693-133">Na caixa de pesquisa hello, digite **M arquivos**.</span><span class="sxs-lookup"><span data-stu-id="35693-133">In hello search box, type **M-Files**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="35693-135">No painel de resultados de saudação, selecione **M arquivos**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="35693-135">In hello results panel, select **M-Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="35693-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="35693-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="35693-138">Nesta seção, você configurará e testará o logon único do Azure AD com o M-Files, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="35693-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="35693-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em milhões de arquivos é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="35693-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in M-Files is tooa user in Azure AD.</span></span> <span data-ttu-id="35693-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em milhões de arquivos precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="35693-140">In other words, a link relationship between an Azure AD user and hello related user in M-Files needs toobe established.</span></span>

<span data-ttu-id="35693-141">Nos arquivos de M, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="35693-141">In M-Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="35693-142">tooconfigure e teste de logon único do AD do Azure com milhões de arquivos, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="35693-142">tooconfigure and test Azure AD single sign-on with M-Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="35693-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="35693-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="35693-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35693-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="35693-145">**[Criar um usuário de teste de milhões de arquivos](#creating-a-m-files-test-user)**  -toohave um equivalente do Britta Simon em milhões de arquivos que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="35693-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - toohave a counterpart of Britta Simon in M-Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="35693-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="35693-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35693-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="35693-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="35693-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="35693-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="35693-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de milhões de arquivos.</span><span class="sxs-lookup"><span data-stu-id="35693-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="35693-150">**tooconfigure AD do Azure-logon único com milhões de arquivos, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="35693-150">**tooconfigure Azure AD single sign-on with M-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="35693-151">Em Olá portal do Azure, Olá **M arquivos** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="35693-151">In hello Azure portal, on hello **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="35693-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="35693-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="35693-155">Em Olá **domínio milhões de arquivos e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35693-155">On hello **M-Files Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="35693-157">a.</span><span class="sxs-lookup"><span data-stu-id="35693-157">a.</span></span> <span data-ttu-id="35693-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="35693-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="35693-159">b.</span><span class="sxs-lookup"><span data-stu-id="35693-159">b.</span></span> <span data-ttu-id="35693-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="35693-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="35693-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="35693-161">These values are not real.</span></span> <span data-ttu-id="35693-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="35693-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="35693-163">Entre em contato com [equipe de suporte de milhões de arquivos cliente](mailto:support@m-files.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="35693-163">Contact [M-Files Client support team](mailto:support@m-files.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="35693-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="35693-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="35693-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="35693-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="35693-168">tooget SSO configurado para o seu aplicativo, entre em contato com [equipe de suporte a milhões de arquivos](mailto:support@m-files.com) e fornecê-los Olá baixado de metadados.</span><span class="sxs-lookup"><span data-stu-id="35693-168">tooget SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them hello downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="35693-169">Siga Olá próximas etapas, se você quiser tooconfigure SSO para que o aplicativo de área de trabalho do arquivo M.</span><span class="sxs-lookup"><span data-stu-id="35693-169">Follow hello next steps if you want tooconfigure SSO for you M-File desktop application.</span></span> <span data-ttu-id="35693-170">Não há etapas adicionais serão necessárias se você quiser apenas tooconfigure SSO para a versão da web de milhões de arquivos.</span><span class="sxs-lookup"><span data-stu-id="35693-170">No extra steps are required if you only want tooconfigure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="35693-171">Siga Olá próxima etapas tooconfigure Olá M arquivo aplicativo de desktop tooenable SSO com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35693-171">Follow hello next steps tooconfigure hello M-File desktop application tooenable SSO with Azure AD.</span></span> <span data-ttu-id="35693-172">toodownload milhões de arquivos, vá muito[baixar arquivos de M](https://www.m-files.com/en/download-latest-version) página.</span><span class="sxs-lookup"><span data-stu-id="35693-172">toodownload M-Files, go too[M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="35693-173">Olá abrir **configurações de área de trabalho de arquivos-M** janela.</span><span class="sxs-lookup"><span data-stu-id="35693-173">Open hello **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="35693-174">Em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="35693-174">Then, click **Add**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="35693-176">Em Olá **propriedades de Conexão do documento cofre** janela, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35693-176">On hello **Document Vault Connection Properties** window, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="35693-178">Em Olá tipo de seção do servidor, Olá valores da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="35693-178">Under hello Server section type, hello values as follows:</span></span>  

    <span data-ttu-id="35693-179">a.</span><span class="sxs-lookup"><span data-stu-id="35693-179">a.</span></span> <span data-ttu-id="35693-180">Para **Nome**, digite `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="35693-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="35693-181">b.</span><span class="sxs-lookup"><span data-stu-id="35693-181">b.</span></span> <span data-ttu-id="35693-182">Para **Número de Porta**, digite **4466**.</span><span class="sxs-lookup"><span data-stu-id="35693-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="35693-183">c.</span><span class="sxs-lookup"><span data-stu-id="35693-183">c.</span></span> <span data-ttu-id="35693-184">Para **Protocolo**, selecione **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="35693-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="35693-185">d.</span><span class="sxs-lookup"><span data-stu-id="35693-185">d.</span></span> <span data-ttu-id="35693-186">Em Olá **autenticação** campo, selecione **usuário específicos do Windows**.</span><span class="sxs-lookup"><span data-stu-id="35693-186">In hello **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="35693-187">Em seguida, você verá uma página de entrada.</span><span class="sxs-lookup"><span data-stu-id="35693-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="35693-188">Insira suas credenciais do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35693-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="35693-189">e.</span><span class="sxs-lookup"><span data-stu-id="35693-189">e.</span></span> <span data-ttu-id="35693-190">Para Olá **cofre no servidor**, selecione Olá cofre correspondente no servidor.</span><span class="sxs-lookup"><span data-stu-id="35693-190">For hello **Vault on Server**,  select hello corresponding vault on server.</span></span>
 
    <span data-ttu-id="35693-191">f.</span><span class="sxs-lookup"><span data-stu-id="35693-191">f.</span></span> <span data-ttu-id="35693-192">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="35693-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="35693-193">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="35693-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="35693-194">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="35693-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="35693-195">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="35693-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="35693-196">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="35693-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="35693-197">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="35693-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="35693-199">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="35693-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="35693-200">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="35693-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="35693-202">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="35693-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="35693-204">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="35693-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="35693-206">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="35693-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="35693-208">a.</span><span class="sxs-lookup"><span data-stu-id="35693-208">a.</span></span> <span data-ttu-id="35693-209">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35693-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="35693-210">b.</span><span class="sxs-lookup"><span data-stu-id="35693-210">b.</span></span> <span data-ttu-id="35693-211">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="35693-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="35693-212">c.</span><span class="sxs-lookup"><span data-stu-id="35693-212">c.</span></span> <span data-ttu-id="35693-213">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="35693-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="35693-214">d.</span><span class="sxs-lookup"><span data-stu-id="35693-214">d.</span></span> <span data-ttu-id="35693-215">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="35693-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="35693-216">Criar um usuário de teste do M-Files</span><span class="sxs-lookup"><span data-stu-id="35693-216">Creating a M-Files test user</span></span>

<span data-ttu-id="35693-217">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon em milhões de arquivos.</span><span class="sxs-lookup"><span data-stu-id="35693-217">hello objective of this section is toocreate a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="35693-218">Trabalhar com [equipe de suporte a milhões de arquivos](mailto:support@m-files.com) tooadd usuários Olá Olá milhões de arquivos.</span><span class="sxs-lookup"><span data-stu-id="35693-218">Work with  [M-Files support team](mailto:support@m-files.com) tooadd hello users in hello M-Files.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="35693-219">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="35693-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="35693-220">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooM-Files.</span><span class="sxs-lookup"><span data-stu-id="35693-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooM-Files.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="35693-222">**tooassign Britta Simon tooM arquivos, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="35693-222">**tooassign Britta Simon tooM-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="35693-223">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="35693-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="35693-225">Na lista de aplicativos hello, selecione **M arquivos**.</span><span class="sxs-lookup"><span data-stu-id="35693-225">In hello applications list, select **M-Files**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="35693-227">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="35693-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="35693-229">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="35693-229">Click **Add** button.</span></span> <span data-ttu-id="35693-230">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="35693-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="35693-232">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="35693-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="35693-233">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="35693-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="35693-234">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="35693-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="35693-235">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="35693-235">Testing single sign-on</span></span>

<span data-ttu-id="35693-236">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="35693-236">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="35693-237">Quando você clica em Olá milhões de arquivos lado a lado no painel de acesso de saudação, você deverá obter o aplicativo automaticamente assinado em tooyour milhões de arquivos.</span><span class="sxs-lookup"><span data-stu-id="35693-237">When you click hello M-Files tile in hello Access Panel, you should get automatically signed-on tooyour M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="35693-238">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="35693-238">Additional resources</span></span>

* [<span data-ttu-id="35693-239">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="35693-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35693-240">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="35693-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

