---
title: "API de relatório aaaPrerequisites tooaccess Olá AD do Azure | Microsoft Docs"
description: "Saiba sobre a API de relatório do hello pré-requisitos tooaccess Olá AD do Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="85356-103">API de relatório pré-requisitos tooaccess Olá AD do Azure</span><span class="sxs-lookup"><span data-stu-id="85356-103">Prerequisites tooaccess hello Azure AD reporting API</span></span>

<span data-ttu-id="85356-104">Olá [reporting APIs do AD do Azure](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) fornece acesso programático toohello dados por meio de um conjunto de APIs com base em REST.</span><span class="sxs-lookup"><span data-stu-id="85356-104">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="85356-105">Você pode chamar essas APIs de várias ferramentas e linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="85356-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="85356-106">Olá reporting API usa [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) APIs da web do toohello tooauthorize acesso.</span><span class="sxs-lookup"><span data-stu-id="85356-106">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="85356-107">tooget acessar dados de relatório toohello por meio da API de Olá, é necessário toohave uma saudação funções atribuídas a seguir:</span><span class="sxs-lookup"><span data-stu-id="85356-107">tooget access toohello reporting data through hello API, you need toohave one of hello following roles assigned:</span></span>

- <span data-ttu-id="85356-108">Leitor de segurança</span><span class="sxs-lookup"><span data-stu-id="85356-108">Security Reader</span></span>
- <span data-ttu-id="85356-109">Administrador de Segurança</span><span class="sxs-lookup"><span data-stu-id="85356-109">Security Admin</span></span>
- <span data-ttu-id="85356-110">Administrador global</span><span class="sxs-lookup"><span data-stu-id="85356-110">Global Admin</span></span>


<span data-ttu-id="85356-111">tooprepare seu toohello acesso API de relatório, você deve:</span><span class="sxs-lookup"><span data-stu-id="85356-111">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="85356-112">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="85356-112">Register an application</span></span> 
2. <span data-ttu-id="85356-113">Conceder permissões</span><span class="sxs-lookup"><span data-stu-id="85356-113">Grant permissions</span></span> 
3. <span data-ttu-id="85356-114">Reunir definições de configuração</span><span class="sxs-lookup"><span data-stu-id="85356-114">Gather configuration settings</span></span> 

<span data-ttu-id="85356-115">Em caso de dúvidas, problemas ou comentários, [registre um tíquete de suporte](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="85356-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="85356-116">Registrar um aplicativo do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85356-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="85356-117">É necessário tooregister um aplicativo, mesmo se você estiver acessando Olá API usando um script de relatório.</span><span class="sxs-lookup"><span data-stu-id="85356-117">You need tooregister an app even if you are accessing hello reporting API using a script.</span></span> <span data-ttu-id="85356-118">Isso lhe dá uma **ID do aplicativo**, que é necessário para uma chamada de autorização e possibilita que os tokens de tooreceive seu código.</span><span class="sxs-lookup"><span data-stu-id="85356-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code tooreceive tokens.</span></span>

<span data-ttu-id="85356-119">tooconfigure seu diretório tooaccess Olá AD do Azure reporting API, você deve entrar no toohello portal do Azure com uma conta de administrador do Azure que também é um membro da saudação **Administrador Global** função de diretório em seu locatário do AD do Azure .</span><span class="sxs-lookup"><span data-stu-id="85356-119">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure portal with an Azure administrator account that is also a member of hello **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85356-120">Aplicativos em execução sob as credenciais com privilégios de "admin" como isso podem ser muito poderosos, portanto as credenciais de ID/segredo do aplicativo de saudação de tookeep-se de que seja seguro.</span><span class="sxs-lookup"><span data-stu-id="85356-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="85356-121">**tooregister um aplicativo do Active Directory do Azure:**</span><span class="sxs-lookup"><span data-stu-id="85356-121">**tooregister an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="85356-122">Em Olá [portal do Azure](https://portal.azure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="85356-122">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="85356-124">Em Olá **Active Directory do Azure** folha, clique em **registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="85356-124">On hello **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="85356-126">Em Olá **registros do aplicativo** folha, na barra de ferramentas Olá superior hello, clique em **novo registro de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="85356-126">On hello **App registrations** blade, in hello toolbar on hello top, click **New application registration**.</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="85356-128">Em Olá **criar** folha, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="85356-128">On hello **Create** blade, perform hello following steps:</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="85356-130">a.</span><span class="sxs-lookup"><span data-stu-id="85356-130">a.</span></span> <span data-ttu-id="85356-131">Em Olá **nome** caixa de texto, tipo `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="85356-131">In hello **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="85356-132">b.</span><span class="sxs-lookup"><span data-stu-id="85356-132">b.</span></span> <span data-ttu-id="85356-133">Como **Tipo de aplicativo**, selecione **Aplicativo/API Web**.</span><span class="sxs-lookup"><span data-stu-id="85356-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="85356-134">c.</span><span class="sxs-lookup"><span data-stu-id="85356-134">c.</span></span> <span data-ttu-id="85356-135">Em Olá **URL de logon** caixa de texto, tipo `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="85356-135">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="85356-136">d.</span><span class="sxs-lookup"><span data-stu-id="85356-136">d.</span></span> <span data-ttu-id="85356-137">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="85356-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="85356-138">Conceder permissões</span><span class="sxs-lookup"><span data-stu-id="85356-138">Grant permissions</span></span> 

<span data-ttu-id="85356-139">objetivo de saudação desta etapa é toogrant seu aplicativo **ler dados do diretório** permissões toohello **Windows Azure Active Directory** API.</span><span class="sxs-lookup"><span data-stu-id="85356-139">hello objective of this step is toogrant your application **Read directory data** permissions toohello **Windows Azure Active Directory** API.</span></span>

![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="85356-141">**toogrant a saudação de toouse de permissão do aplicativo API:**</span><span class="sxs-lookup"><span data-stu-id="85356-141">**toogrant your application permission toouse hello API:**</span></span>

1. <span data-ttu-id="85356-142">Em Olá **registros do aplicativo** folha, na lista de aplicativos de saudação, clique em **aplicativo de API Reporting**.</span><span class="sxs-lookup"><span data-stu-id="85356-142">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="85356-143">Em Olá **aplicativo de API Reporting** folha, na barra de ferramentas Olá superior hello, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="85356-143">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="85356-145">Em Olá **configurações** folha, clique em **as permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="85356-145">On hello **Settings** blade, click **Required permissions**.</span></span> 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="85356-147">Em Olá **as permissões necessárias** folha em Olá **API** lista, clique em **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="85356-147">On hello **Required permissions** blade, in hello **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="85356-149">Em Olá **habilitar acesso** folha, selecione **ler dados do diretório**.</span><span class="sxs-lookup"><span data-stu-id="85356-149">On hello **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="85356-151">Na barra de ferramentas de saudação na parte superior do hello, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="85356-151">In hello toolbar on hello top, click **Save**.</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="85356-153">Reunir definições de configuração</span><span class="sxs-lookup"><span data-stu-id="85356-153">Gather configuration settings</span></span> 
<span data-ttu-id="85356-154">Esta seção mostra como Olá tooget seguir as configurações de seu diretório:</span><span class="sxs-lookup"><span data-stu-id="85356-154">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="85356-155">Nome de domínio</span><span class="sxs-lookup"><span data-stu-id="85356-155">Domain name</span></span>
* <span data-ttu-id="85356-156">ID do cliente</span><span class="sxs-lookup"><span data-stu-id="85356-156">Client ID</span></span>
* <span data-ttu-id="85356-157">Segredo do cliente</span><span class="sxs-lookup"><span data-stu-id="85356-157">Client secret</span></span>

<span data-ttu-id="85356-158">Você precisa esses valores quando configurar chamadas toohello reporting API.</span><span class="sxs-lookup"><span data-stu-id="85356-158">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="85356-159">Obter seu nome de domínio</span><span class="sxs-lookup"><span data-stu-id="85356-159">Get your domain name</span></span>

<span data-ttu-id="85356-160">**tooget seu nome de domínio:**</span><span class="sxs-lookup"><span data-stu-id="85356-160">**tooget your domain name:**</span></span>

1. <span data-ttu-id="85356-161">Em Olá [portal do Azure](https://portal.azure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="85356-161">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="85356-163">Em Olá **Active Directory do Azure** folha, clique em **nomes de domínio**.</span><span class="sxs-lookup"><span data-stu-id="85356-163">On hello **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="85356-165">Copie o nome de domínio da lista de saudação de domínios.</span><span class="sxs-lookup"><span data-stu-id="85356-165">Copy your domain name from hello list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="85356-166">Obtenha a ID do cliente do aplicativo</span><span class="sxs-lookup"><span data-stu-id="85356-166">Get your application's client ID</span></span>

<span data-ttu-id="85356-167">**tooget ID do cliente do aplicativo:**</span><span class="sxs-lookup"><span data-stu-id="85356-167">**tooget your application's client ID:**</span></span>

1. <span data-ttu-id="85356-168">Em Olá [portal do Azure](https://portal.azure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="85356-168">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="85356-170">Em Olá **registros do aplicativo** folha, na lista de aplicativos de saudação, clique em **aplicativo de API Reporting**.</span><span class="sxs-lookup"><span data-stu-id="85356-170">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="85356-171">Em Olá **aplicativo de API Reporting** blade, a saudação **ID do aplicativo**, clique em **clique toocopy**.</span><span class="sxs-lookup"><span data-stu-id="85356-171">On hello **Reporting API application** blade, at hello **Application ID**, click **Click toocopy**.</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="85356-173">Obter seu segredo do cliente do aplicativo</span><span class="sxs-lookup"><span data-stu-id="85356-173">Get your application's client secret</span></span>
<span data-ttu-id="85356-174">tooget cliente do aplicativo segredo, você precisa toocreate uma nova chave e salve seu valor ao salvar a nova chave de saudação porque ele não é possível tooretrieve este valor posteriormente mais.</span><span class="sxs-lookup"><span data-stu-id="85356-174">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

<span data-ttu-id="85356-175">**tooget segredo do cliente do aplicativo:**</span><span class="sxs-lookup"><span data-stu-id="85356-175">**tooget your application's client secret:**</span></span>

1. <span data-ttu-id="85356-176">Em Olá [portal do Azure](https://portal.azure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="85356-176">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="85356-178">Em Olá **registros do aplicativo** folha, na lista de aplicativos de saudação, clique em **aplicativo de API Reporting**.</span><span class="sxs-lookup"><span data-stu-id="85356-178">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="85356-179">Em Olá **aplicativo de API Reporting** folha, na barra de ferramentas Olá superior hello, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="85356-179">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="85356-181">Em Olá **configurações** folha em Olá **APIR acesso** seção, clique em **chaves**.</span><span class="sxs-lookup"><span data-stu-id="85356-181">On hello **Settings** blade, in hello **APIR Access** section, click **Keys**.</span></span> 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="85356-183">Em Olá **chaves** folha, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="85356-183">On hello **Keys** blade, perform hello following steps:</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="85356-185">a.</span><span class="sxs-lookup"><span data-stu-id="85356-185">a.</span></span> <span data-ttu-id="85356-186">Em Olá **descrição** caixa de texto, tipo `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="85356-186">In hello **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="85356-187">b.</span><span class="sxs-lookup"><span data-stu-id="85356-187">b.</span></span> <span data-ttu-id="85356-188">Como **Expira**, selecione **Em 2 anos**.</span><span class="sxs-lookup"><span data-stu-id="85356-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="85356-189">c.</span><span class="sxs-lookup"><span data-stu-id="85356-189">c.</span></span> <span data-ttu-id="85356-190">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="85356-190">Click **Save**.</span></span>

    <span data-ttu-id="85356-191">d.</span><span class="sxs-lookup"><span data-stu-id="85356-191">d.</span></span> <span data-ttu-id="85356-192">Copie o valor da chave hello.</span><span class="sxs-lookup"><span data-stu-id="85356-192">Copy hello key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="85356-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85356-193">Next Steps</span></span>
* <span data-ttu-id="85356-194">Seria você como tooaccess Olá dados de saudação do AD do Azure API de relatório de modo programático?</span><span class="sxs-lookup"><span data-stu-id="85356-194">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="85356-195">Check-out [Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="85356-195">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="85356-196">Se você quiser toofind mais informações sobre os relatórios do Active Directory do Azure, consulte Olá [do Azure Active Directory Reporting guia](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="85356-196">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

