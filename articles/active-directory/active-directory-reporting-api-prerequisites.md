---
title: "Olá AD do Azure aaaPrerequisites tooaccess reporting API. | Microsoft Docs"
description: "Saiba sobre a API de relatório do hello pré-requisitos tooaccess Olá AD do Azure"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="20678-104">API de relatório pré-requisitos tooaccess Olá AD do Azure</span><span class="sxs-lookup"><span data-stu-id="20678-104">Prerequisites tooaccess hello Azure AD reporting API</span></span>
<span data-ttu-id="20678-105">Olá [reporting APIs do AD do Azure](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) fornece acesso programático toohello dados por meio de um conjunto de APIs com base em REST.</span><span class="sxs-lookup"><span data-stu-id="20678-105">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="20678-106">Você pode chamar essas APIs de várias ferramentas e linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="20678-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="20678-107">Olá reporting API usa [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) APIs da web do toohello tooauthorize acesso.</span><span class="sxs-lookup"><span data-stu-id="20678-107">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="20678-108">tooprepare seu toohello acesso API de relatório, você deve:</span><span class="sxs-lookup"><span data-stu-id="20678-108">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="20678-109">Crie um aplicativo em seu locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="20678-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="20678-110">Grant Olá aplicativo as permissões apropriadas tooaccess Olá dados do Azure AD</span><span class="sxs-lookup"><span data-stu-id="20678-110">Grant hello application appropriate permissions tooaccess hello Azure AD data</span></span>
3. <span data-ttu-id="20678-111">Reúna as definições de configuração de seu diretório</span><span class="sxs-lookup"><span data-stu-id="20678-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="20678-112">Para dúvidas, problemas ou comentários, entre em contato com a [Ajuda de relatório do AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="20678-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="20678-113">Criar um aplicativo Azure AD</span><span class="sxs-lookup"><span data-stu-id="20678-113">Create an Azure AD application</span></span>
<span data-ttu-id="20678-114">tooconfigure seu diretório tooaccess Olá AD do Azure reporting API, você deve entrar no toohello portal clássico do Azure com uma conta de administrador de assinatura do Azure que também é um membro da função de diretório Olá Administrador Global em seu locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="20678-114">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure classic portal with an Azure subscription administrator account that is also a member of hello Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20678-115">Aplicativos em execução sob as credenciais com privilégios de "admin" como isso podem ser muito poderosos, portanto as credenciais de ID/segredo do aplicativo de saudação de tookeep-se de que seja seguro.</span><span class="sxs-lookup"><span data-stu-id="20678-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="20678-116">Em Olá [portal clássico do Azure](https://manage.windowsazure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="20678-116">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="20678-118">De saudação **do active directory** , selecione seu diretório.</span><span class="sxs-lookup"><span data-stu-id="20678-118">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="20678-119">No menu de saudação na parte superior de saudação, clique em **aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="20678-119">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="20678-121">Na barra inferior de saudação, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="20678-121">On hello bottom bar, click **Add**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="20678-123">Em Olá **o que fazer você deseja toodo?** caixa de diálogo, clique em **adicionar um aplicativo que minha organização esteja desenvolvendo**.</span><span class="sxs-lookup"><span data-stu-id="20678-123">On hello **What do you want toodo?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="20678-125">Em Olá **Conte-nos sobre seu aplicativo** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="20678-125">On hello **Tell us about your application** dialog, perform hello following steps:</span></span> 
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="20678-127">a.</span><span class="sxs-lookup"><span data-stu-id="20678-127">a.</span></span> <span data-ttu-id="20678-128">Em Olá **nome** caixa de texto, digite um nome (por exemplo: aplicativo de API de relatório).</span><span class="sxs-lookup"><span data-stu-id="20678-128">In hello **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="20678-129">b.</span><span class="sxs-lookup"><span data-stu-id="20678-129">b.</span></span> <span data-ttu-id="20678-130">Selecione **Aplicativo Web e/ou API Web**.</span><span class="sxs-lookup"><span data-stu-id="20678-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="20678-131">c.</span><span class="sxs-lookup"><span data-stu-id="20678-131">c.</span></span> <span data-ttu-id="20678-132">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="20678-132">Click **Next**.</span></span>
7. <span data-ttu-id="20678-133">Em Olá **propriedades do aplicativo** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="20678-133">On hello **App properties** dialog, perform hello following steps:</span></span> 
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="20678-135">a.</span><span class="sxs-lookup"><span data-stu-id="20678-135">a.</span></span> <span data-ttu-id="20678-136">Em Olá **URL de logon** caixa de texto, tipo `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="20678-136">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="20678-137">b.</span><span class="sxs-lookup"><span data-stu-id="20678-137">b.</span></span> <span data-ttu-id="20678-138">Em Olá **URI da ID do aplicativo** caixa de texto, tipo ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="20678-138">In hello **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="20678-139">c.</span><span class="sxs-lookup"><span data-stu-id="20678-139">c.</span></span> <span data-ttu-id="20678-140">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="20678-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="20678-141">Conceder a saudação de toouse de permissão do aplicativo API</span><span class="sxs-lookup"><span data-stu-id="20678-141">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="20678-142">Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="20678-142">In hello [Azure classic portal](https://manage.windowsazure.com/), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="20678-144">De saudação **do active directory** , selecione seu diretório.</span><span class="sxs-lookup"><span data-stu-id="20678-144">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="20678-145">No menu de saudação na parte superior de saudação, clique em **aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="20678-145">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="20678-147">Na lista de aplicativos hello, selecione seu aplicativo recém-criado.</span><span class="sxs-lookup"><span data-stu-id="20678-147">In hello applications list, select your newly created application.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="20678-149">No menu de saudação na parte superior de saudação, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="20678-149">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="20678-151">Em hello **permissões tooother aplicativos** seção para hello **Active Directory do Azure** recursos, clique em hello **permissões de aplicativo** lista suspensa e, em seguida, Selecione **ler dados do diretório**.</span><span class="sxs-lookup"><span data-stu-id="20678-151">In hello **Permissions tooother applications** section, for hello **Azure Active Directory** resource, click hello **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="20678-153">Na barra inferior de saudação, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="20678-153">On hello bottom bar, click **Save**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="20678-155">Reúna as definições de configuração de seu diretório</span><span class="sxs-lookup"><span data-stu-id="20678-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="20678-156">Esta seção mostra como Olá tooget seguir as configurações de seu diretório:</span><span class="sxs-lookup"><span data-stu-id="20678-156">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="20678-157">Nome de domínio</span><span class="sxs-lookup"><span data-stu-id="20678-157">Domain name</span></span>
* <span data-ttu-id="20678-158">ID do cliente</span><span class="sxs-lookup"><span data-stu-id="20678-158">Client ID</span></span>
* <span data-ttu-id="20678-159">Segredo do cliente</span><span class="sxs-lookup"><span data-stu-id="20678-159">Client secret</span></span>

<span data-ttu-id="20678-160">Você precisa esses valores quando configurar chamadas toohello reporting API.</span><span class="sxs-lookup"><span data-stu-id="20678-160">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="20678-161">Obter seu nome de domínio</span><span class="sxs-lookup"><span data-stu-id="20678-161">Get your domain name</span></span>
1. <span data-ttu-id="20678-162">Em Olá [portal clássico do Azure](https://manage.windowsazure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="20678-162">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="20678-164">De saudação **do active directory** , selecione seu diretório.</span><span class="sxs-lookup"><span data-stu-id="20678-164">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="20678-165">No menu de saudação na parte superior de saudação, clique em **domínios**.</span><span class="sxs-lookup"><span data-stu-id="20678-165">In hello menu on hello top, click **Domains**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="20678-167">Em Olá **nome de domínio** coluna, copie o seu nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="20678-167">In hello **Domain Name** column, copy your domain name.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a><span data-ttu-id="20678-169">Obter ID do cliente do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="20678-169">Get hello application's client ID</span></span>
1. <span data-ttu-id="20678-170">Em Olá [portal clássico do Azure](https://manage.windowsazure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="20678-170">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="20678-172">De saudação **do active directory** , selecione seu diretório.</span><span class="sxs-lookup"><span data-stu-id="20678-172">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="20678-173">No menu de saudação na parte superior de saudação, clique em **aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="20678-173">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="20678-175">Na lista de aplicativos hello, selecione seu aplicativo recém-criado.</span><span class="sxs-lookup"><span data-stu-id="20678-175">In hello applications list, select your newly created application.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="20678-177">No menu de saudação na parte superior de saudação, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="20678-177">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="20678-179">Copie a **ID do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="20678-179">Copy your **Client ID**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a><span data-ttu-id="20678-181">Obter o segredo do cliente do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="20678-181">Get hello application's client secret</span></span>
<span data-ttu-id="20678-182">tooget cliente do aplicativo segredo, você precisa toocreate uma nova chave e salve seu valor ao salvar a nova chave de saudação porque ele não é possível tooretrieve este valor posteriormente mais.</span><span class="sxs-lookup"><span data-stu-id="20678-182">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

1. <span data-ttu-id="20678-183">Em Olá [portal clássico do Azure](https://manage.windowsazure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="20678-183">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="20678-185">De saudação **do active directory** , selecione seu diretório.</span><span class="sxs-lookup"><span data-stu-id="20678-185">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="20678-186">No menu de saudação na parte superior de saudação, clique em **aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="20678-186">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="20678-188">Na lista de aplicativos hello, selecione seu aplicativo recém-criado.</span><span class="sxs-lookup"><span data-stu-id="20678-188">In hello applications list, select your newly created application.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="20678-190">No menu de saudação na parte superior de saudação, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="20678-190">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="20678-192">Em Olá **chaves** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="20678-192">In hello **Keys** section, perform hello following steps:</span></span> 
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="20678-194">a.</span><span class="sxs-lookup"><span data-stu-id="20678-194">a.</span></span> <span data-ttu-id="20678-195">Na lista de duração hello, selecione uma duração</span><span class="sxs-lookup"><span data-stu-id="20678-195">From hello duration list, select a duration</span></span>
   
    <span data-ttu-id="20678-196">b.</span><span class="sxs-lookup"><span data-stu-id="20678-196">b.</span></span> <span data-ttu-id="20678-197">Na barra inferior de saudação, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="20678-197">On hello bottom bar, click **Save**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="20678-199">c.</span><span class="sxs-lookup"><span data-stu-id="20678-199">c.</span></span> <span data-ttu-id="20678-200">Copie o valor da chave hello.</span><span class="sxs-lookup"><span data-stu-id="20678-200">Copy hello key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20678-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="20678-201">Next Steps</span></span>
* <span data-ttu-id="20678-202">Seria você como tooaccess Olá dados de saudação do AD do Azure API de relatório de modo programático?</span><span class="sxs-lookup"><span data-stu-id="20678-202">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="20678-203">Check-out [Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="20678-203">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="20678-204">Se você quiser toofind mais informações sobre os relatórios do Active Directory do Azure, consulte Olá [do Azure Active Directory Reporting guia](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="20678-204">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

