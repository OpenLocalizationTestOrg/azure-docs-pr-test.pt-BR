---
title: "Pré-requisitos para acessar a API de relatório do Azure AD. | Microsoft Docs"
description: "Aprenda sobre os pré-requisitos para acessar a API de relatório do Azure AD"
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
ms.openlocfilehash: 6e409fc56b77f37dac7f37382e664c577666ad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="148e6-104">Pré-requisitos para acessar a API de relatório do Azure AD</span><span class="sxs-lookup"><span data-stu-id="148e6-104">Prerequisites to access the Azure AD reporting API</span></span>
<span data-ttu-id="148e6-105">As [APIs de relatório do Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) fornecem acesso programático aos dados através de um conjunto de APIs baseadas em REST.</span><span class="sxs-lookup"><span data-stu-id="148e6-105">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="148e6-106">Você pode chamar essas APIs de várias ferramentas e linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="148e6-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="148e6-107">A API de relatório usa [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) para autorizar o acesso às APIs da Web.</span><span class="sxs-lookup"><span data-stu-id="148e6-107">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="148e6-108">Para preparar seu acesso à API de relatório, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="148e6-108">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="148e6-109">Crie um aplicativo em seu locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="148e6-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="148e6-110">Conceda as permissões apropriadas do aplicativo para acessar os dados do Azure AD</span><span class="sxs-lookup"><span data-stu-id="148e6-110">Grant the application appropriate permissions to access the Azure AD data</span></span>
3. <span data-ttu-id="148e6-111">Reúna as definições de configuração de seu diretório</span><span class="sxs-lookup"><span data-stu-id="148e6-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="148e6-112">Para dúvidas, problemas ou comentários, entre em contato com a [Ajuda de relatório do AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="148e6-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="148e6-113">Criar um aplicativo Azure AD</span><span class="sxs-lookup"><span data-stu-id="148e6-113">Create an Azure AD application</span></span>
<span data-ttu-id="148e6-114">Para configurar seu diretório a fim de acessar a API de relatório do Azure AD, você deve entrar Portal Clássico do Azure com uma conta de administrador de assinatura do Azure que também é membro da função de diretório de Administrador Global em seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="148e6-114">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure classic portal with an Azure subscription administrator account that is also a member of the Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="148e6-115">Aplicativos em execução com credenciais com privilégios de "admin" como esse podem ser muito poderosos, portanto certifique-se de proteger as credenciais de ID/segredo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="148e6-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="148e6-116">No [portal clássico do Azure](https://manage.windowsazure.com), no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="148e6-116">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="148e6-118">Na lista de **diretórios ativos** , selecione o diretório.</span><span class="sxs-lookup"><span data-stu-id="148e6-118">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="148e6-119">No menu superior, clique em **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="148e6-119">In the menu on the top, click **Applications**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="148e6-121">Na barra de ferramentas inferior, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="148e6-121">On the bottom bar, click **Add**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="148e6-123">Na caixa de diálogo **O que você deseja fazer?**, clique em **Adicionar um aplicativo que minha organização esteja desenvolvendo**.</span><span class="sxs-lookup"><span data-stu-id="148e6-123">On the **What do you want to do?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="148e6-125">Na página de diálogo **Conte-nos sobre este usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="148e6-125">On the **Tell us about your application** dialog, perform the following steps:</span></span> 
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="148e6-127">a.</span><span class="sxs-lookup"><span data-stu-id="148e6-127">a.</span></span> <span data-ttu-id="148e6-128">Na caixa de texto **Nome** , digite um nome (por exemplo: Aplicativo de API de Relatório).</span><span class="sxs-lookup"><span data-stu-id="148e6-128">In the **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="148e6-129">b.</span><span class="sxs-lookup"><span data-stu-id="148e6-129">b.</span></span> <span data-ttu-id="148e6-130">Selecione **Aplicativo Web e/ou API Web**.</span><span class="sxs-lookup"><span data-stu-id="148e6-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="148e6-131">c.</span><span class="sxs-lookup"><span data-stu-id="148e6-131">c.</span></span> <span data-ttu-id="148e6-132">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="148e6-132">Click **Next**.</span></span>
7. <span data-ttu-id="148e6-133">Na caixa de diálogo **Propriedades de aplicativo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="148e6-133">On the **App properties** dialog, perform the following steps:</span></span> 
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="148e6-135">a.</span><span class="sxs-lookup"><span data-stu-id="148e6-135">a.</span></span> <span data-ttu-id="148e6-136">Na caixa de texto **URL de Entrada**, digite `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="148e6-136">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="148e6-137">b.</span><span class="sxs-lookup"><span data-stu-id="148e6-137">b.</span></span> <span data-ttu-id="148e6-138">Na caixa de texto **URI da ID do Aplicativo**, digite ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="148e6-138">In the **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="148e6-139">c.</span><span class="sxs-lookup"><span data-stu-id="148e6-139">c.</span></span> <span data-ttu-id="148e6-140">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="148e6-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="148e6-141">Conceda permissão ao aplicativo para usar a API</span><span class="sxs-lookup"><span data-stu-id="148e6-141">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="148e6-142">No [portal clássico do Azure](https://manage.windowsazure.com/), no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="148e6-142">In the [Azure classic portal](https://manage.windowsazure.com/), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="148e6-144">Na lista de **diretórios ativos** , selecione o diretório.</span><span class="sxs-lookup"><span data-stu-id="148e6-144">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="148e6-145">No menu superior, clique em **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="148e6-145">In the menu on the top, click **Applications**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="148e6-147">Na lista de aplicativos, selecione o aplicativo recém-criado.</span><span class="sxs-lookup"><span data-stu-id="148e6-147">In the applications list, select your newly created application.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="148e6-149">No menu na parte superior, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="148e6-149">In the menu on the top, click **Configure**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="148e6-151">Na seção **Permissões para outros aplicativos**, para o recurso **Azure Active Directory**, clique na lista suspensa **Permissões de Aplicativo** e selecione **Ler dados de diretório**.</span><span class="sxs-lookup"><span data-stu-id="148e6-151">In the **Permissions to other applications** section, for the **Azure Active Directory** resource, click the **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="148e6-153">Na barra inferior, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="148e6-153">On the bottom bar, click **Save**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="148e6-155">Reúna as definições de configuração de seu diretório</span><span class="sxs-lookup"><span data-stu-id="148e6-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="148e6-156">Esta seção mostra como obter as seguintes configurações de seu diretório:</span><span class="sxs-lookup"><span data-stu-id="148e6-156">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="148e6-157">Nome de domínio</span><span class="sxs-lookup"><span data-stu-id="148e6-157">Domain name</span></span>
* <span data-ttu-id="148e6-158">ID do cliente</span><span class="sxs-lookup"><span data-stu-id="148e6-158">Client ID</span></span>
* <span data-ttu-id="148e6-159">Segredo do cliente</span><span class="sxs-lookup"><span data-stu-id="148e6-159">Client secret</span></span>

<span data-ttu-id="148e6-160">Você precisa desses valores ao configurar chamadas para a API de relatórios.</span><span class="sxs-lookup"><span data-stu-id="148e6-160">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="148e6-161">Obter seu nome de domínio</span><span class="sxs-lookup"><span data-stu-id="148e6-161">Get your domain name</span></span>
1. <span data-ttu-id="148e6-162">No [portal clássico do Azure](https://manage.windowsazure.com), no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="148e6-162">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="148e6-164">Na lista de **diretórios ativos** , selecione o diretório.</span><span class="sxs-lookup"><span data-stu-id="148e6-164">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="148e6-165">No menu na parte superior, clique em **Domínios**.</span><span class="sxs-lookup"><span data-stu-id="148e6-165">In the menu on the top, click **Domains**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="148e6-167">Na coluna **Nome de Domínio** copie seu nome de domínio no campo.</span><span class="sxs-lookup"><span data-stu-id="148e6-167">In the **Domain Name** column, copy your domain name.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a><span data-ttu-id="148e6-169">Obter a ID do cliente do aplicativo</span><span class="sxs-lookup"><span data-stu-id="148e6-169">Get the application's client ID</span></span>
1. <span data-ttu-id="148e6-170">No [portal clássico do Azure](https://manage.windowsazure.com), no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="148e6-170">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="148e6-172">Na lista de **diretórios ativos** , selecione o diretório.</span><span class="sxs-lookup"><span data-stu-id="148e6-172">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="148e6-173">No menu superior, clique em **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="148e6-173">In the menu on the top, click **Applications**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="148e6-175">Na lista de aplicativos, selecione o aplicativo recém-criado.</span><span class="sxs-lookup"><span data-stu-id="148e6-175">In the applications list, select your newly created application.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="148e6-177">No menu na parte superior, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="148e6-177">In the menu on the top, click **Configure**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="148e6-179">Copie a **ID do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="148e6-179">Copy your **Client ID**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a><span data-ttu-id="148e6-181">Obter o segredo do cliente do aplicativo</span><span class="sxs-lookup"><span data-stu-id="148e6-181">Get the application's client secret</span></span>
<span data-ttu-id="148e6-182">Para obter o segredo do cliente do aplicativo, você precisa criar uma nova chave e salvar seu valor ao salvar a nova chave, pois não é possível recuperar este valor posteriormente.</span><span class="sxs-lookup"><span data-stu-id="148e6-182">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

1. <span data-ttu-id="148e6-183">No [portal clássico do Azure](https://manage.windowsazure.com), no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="148e6-183">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="148e6-185">Na lista de **diretórios ativos** , selecione o diretório.</span><span class="sxs-lookup"><span data-stu-id="148e6-185">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="148e6-186">No menu superior, clique em **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="148e6-186">In the menu on the top, click **Applications**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="148e6-188">Na lista de aplicativos, selecione o aplicativo recém-criado.</span><span class="sxs-lookup"><span data-stu-id="148e6-188">In the applications list, select your newly created application.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="148e6-190">No menu na parte superior, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="148e6-190">In the menu on the top, click **Configure**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="148e6-192">Na seção **Chaves** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="148e6-192">In the **Keys** section, perform the following steps:</span></span> 
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="148e6-194">a.</span><span class="sxs-lookup"><span data-stu-id="148e6-194">a.</span></span> <span data-ttu-id="148e6-195">Na lista duração, selecione uma duração</span><span class="sxs-lookup"><span data-stu-id="148e6-195">From the duration list, select a duration</span></span>
   
    <span data-ttu-id="148e6-196">b.</span><span class="sxs-lookup"><span data-stu-id="148e6-196">b.</span></span> <span data-ttu-id="148e6-197">Na barra inferior, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="148e6-197">On the bottom bar, click **Save**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="148e6-199">c.</span><span class="sxs-lookup"><span data-stu-id="148e6-199">c.</span></span> <span data-ttu-id="148e6-200">Copie o valor da chave.</span><span class="sxs-lookup"><span data-stu-id="148e6-200">Copy the key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="148e6-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="148e6-201">Next Steps</span></span>
* <span data-ttu-id="148e6-202">Você gostaria de acessar os dados da API de relatório do Azure AD de uma maneira programática?</span><span class="sxs-lookup"><span data-stu-id="148e6-202">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="148e6-203">Confira [Introdução à API de Relatório do Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="148e6-203">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="148e6-204">Se você quiser saber mais sobre os relatórios do Azure Active Directory, confira o [Guia de relatórios do Azure Active Directory](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="148e6-204">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

