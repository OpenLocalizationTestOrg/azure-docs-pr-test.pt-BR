---
title: aaaAuthenticate com APIs de REST do Mobile Engagement
description: Descreve como tooauthenticate com APIs de REST do Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="62cfe-103">Autenticar com APIs REST do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="62cfe-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="62cfe-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="62cfe-104">Overview</span></span>
<span data-ttu-id="62cfe-105">Este documento descreve como tooget um Oauth válida do AAD token tooauthenticate com hello APIs de REST do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="62cfe-105">This document describes how tooget a valid AAD Oauth token tooauthenticate with hello Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="62cfe-106">Supõe-se que você tenha uma assinatura válida do Azure e criou um aplicativo do Mobile Engagement usando um dos nossos [Tutoriais de Desenvolvedor](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="62cfe-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="62cfe-107">Autenticação</span><span class="sxs-lookup"><span data-stu-id="62cfe-107">Authentication</span></span>
<span data-ttu-id="62cfe-108">Um token OAuth baseado no Microsoft Azure Active Directory é usado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="62cfe-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="62cfe-109">Tooauthentication uma API de pedido, um cabeçalho de autorização deve ser adicionado solicitação tooevery que é de saudação formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="62cfe-109">In order tooauthentication an API request, an authorization header must be added tooevery request which is of hello following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="62cfe-110">Tokens de Azure Active Directory expiram em 1 hora.</span><span class="sxs-lookup"><span data-stu-id="62cfe-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="62cfe-111">Há tooget de várias maneiras de um token.</span><span class="sxs-lookup"><span data-stu-id="62cfe-111">There are several ways tooget a token.</span></span> <span data-ttu-id="62cfe-112">Já que Olá que APIs geralmente são chamados de um serviço de nuvem, você deseja toouse uma chave de API.</span><span class="sxs-lookup"><span data-stu-id="62cfe-112">Since hello APIs are generally called from a cloud service, you want toouse an API key.</span></span> <span data-ttu-id="62cfe-113">Uma chave de API na terminologia do Azure é chamada de senha de uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="62cfe-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="62cfe-114">Olá, procedimento a seguir descreve uma maneira toosetting-up manualmente.</span><span class="sxs-lookup"><span data-stu-id="62cfe-114">hello following procedure describes one way toosetting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="62cfe-115">Configuração única (usando script)</span><span class="sxs-lookup"><span data-stu-id="62cfe-115">One-time setup (using script)</span></span>
<span data-ttu-id="62cfe-116">Você deve seguir o conjunto de instruções abaixo da configuração de saudação tooperform usando um script do PowerShell que demora Olá mínimo para a instalação, mas usa padrões mais permitidos Olá de saudação.</span><span class="sxs-lookup"><span data-stu-id="62cfe-116">You should follow hello set of instructions below tooperform hello setup using a PowerShell script which takes hello minimum time for setup but uses hello most permissible defaults.</span></span> <span data-ttu-id="62cfe-117">Opcionalmente, você também pode seguir as instruções de Olá Olá [configuração manual](mobile-engagement-api-authentication-manual.md) para fazer isso da saudação diretamente o portal do Azure e configuração mais refinada.</span><span class="sxs-lookup"><span data-stu-id="62cfe-117">Optionally, you can also follow hello instructions in hello [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from hello Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="62cfe-118">Obter versão mais recente de saudação do Azure PowerShell de [aqui](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="62cfe-118">Get hello latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="62cfe-119">Para obter mais informações sobre as instruções de download do hello, você poderá ver isso [link](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="62cfe-119">For more information on hello download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="62cfe-120">Depois de instalar o Azure PowerShell, use a seguir Olá comandos tooensure que você tenha Olá **do módulo Azure** instalado:</span><span class="sxs-lookup"><span data-stu-id="62cfe-120">Once Azure PowerShell is installed, use hello following commands tooensure that you have hello **Azure module** installed:</span></span>
   
    <span data-ttu-id="62cfe-121">a.</span><span class="sxs-lookup"><span data-stu-id="62cfe-121">a.</span></span> <span data-ttu-id="62cfe-122">Verifique se o módulo do PowerShell do Azure hello está disponível na lista de saudação de módulos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="62cfe-122">Make sure hello Azure PowerShell module is available in hello list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![Módulos do Azure disponíveis][1]
   
    <span data-ttu-id="62cfe-124">b.</span><span class="sxs-lookup"><span data-stu-id="62cfe-124">b.</span></span> <span data-ttu-id="62cfe-125">Se você não encontrar módulo do PowerShell do Azure Olá Olá acima da lista, em seguida, é necessário a seguir Olá toorun:</span><span class="sxs-lookup"><span data-stu-id="62cfe-125">If you do not find hello Azure PowerShell module in hello above list then you need toorun hello following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="62cfe-126">Toohello de logon do Azure Resource Manager do PowerShell executando Olá o comando a seguir e fornecendo seu nome de usuário e senha para sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="62cfe-126">Login toohello Azure Resource Manager from PowerShell by running hello following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="62cfe-127">Se você tiver várias assinaturas, em seguida, você deve executar o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="62cfe-127">If you have multiple subscriptions then you should run hello following:</span></span>
   
    <span data-ttu-id="62cfe-128">a.</span><span class="sxs-lookup"><span data-stu-id="62cfe-128">a.</span></span> <span data-ttu-id="62cfe-129">Obter uma lista de todas as suas assinaturas e Olá cópia SubscriptionId de assinatura Olá que deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="62cfe-129">Get a list of all your subscriptions and copy hello SubscriptionId of hello subscription you want toouse.</span></span> <span data-ttu-id="62cfe-130">Verifique se esta assinatura está Olá mesmo um que possua Olá aplicativo móvel do contrato que você toointeract com usando Olá APIs.</span><span class="sxs-lookup"><span data-stu-id="62cfe-130">Make sure this subscription is hello same one which has hello Mobile Engagement App which you are going toointeract with using hello APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="62cfe-131">b.</span><span class="sxs-lookup"><span data-stu-id="62cfe-131">b.</span></span> <span data-ttu-id="62cfe-132">Comando a seguir de execução Olá os toobe de assinatura de saudação da tooconfigure do SubscriptionId Olá fornecendo usado.</span><span class="sxs-lookup"><span data-stu-id="62cfe-132">Run hello following command providing hello SubscriptionId tooconfigure hello subscription toobe used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="62cfe-133">Copiar texto de saudação de saudação [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) máquina local tooyour de script e salve-o como um cmdlet do PowerShell (por exemplo, `APIAuth.ps1`) e execute-o `.\APIAuth.ps1`.</span><span class="sxs-lookup"><span data-stu-id="62cfe-133">Copy hello text for hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script tooyour local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="62cfe-134">Olá script solicitará que você tooprovide uma entrada para **principalName**.</span><span class="sxs-lookup"><span data-stu-id="62cfe-134">hello script will ask you tooprovide an input for **principalName**.</span></span> <span data-ttu-id="62cfe-135">Forneça um nome adequado aqui que você deseja toouse toocreate seu aplicativo do Active Directory (por exemplo, APIAuth).</span><span class="sxs-lookup"><span data-stu-id="62cfe-135">Provide a suitable name here that you want toouse toocreate your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="62cfe-136">Após a conclusão do script hello, ele exibirá Olá seguintes quatro valores que você precisará tooauthenticate programaticamente com o AD, portanto, certifique-se de que toocopy-los.</span><span class="sxs-lookup"><span data-stu-id="62cfe-136">After hello script completes, it will display hello following four values that you will need tooauthenticate programmatically with AD so make sure toocopy them.</span></span> 
   
    <span data-ttu-id="62cfe-137">**TenantId**, **SubscriptionId**, **ApplicationId** e **Secret**.</span><span class="sxs-lookup"><span data-stu-id="62cfe-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="62cfe-138">Use o TenantId como `{TENANT_ID}`, o ApplicationId como `{CLIENT_ID}` e o Secret como `{CLIENT_SECRET}`.</span><span class="sxs-lookup"><span data-stu-id="62cfe-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="62cfe-139">A política de segurança padrão pode impedir a execução de scripts do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62cfe-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="62cfe-140">Nesse caso, configure temporariamente a execução do script execução política tooallow usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="62cfe-140">If so, you temporarily configure your execution policy tooallow script execution using hello following command:</span></span>
   > 
   > <span data-ttu-id="62cfe-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="62cfe-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="62cfe-142">Aqui está como conjunto de saudação de cmdlets do PS seria semelhante.</span><span class="sxs-lookup"><span data-stu-id="62cfe-142">Here is how hello set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="62cfe-143">Verifique no portal de gerenciamento do Azure de saudação que um novo aplicativo do AD foi criado com o nome da saudação você fornecido toohello script chamado **principalName** em **Mostrar aplicativos que minha empresa possui**.</span><span class="sxs-lookup"><span data-stu-id="62cfe-143">Check in hello Azure Management portal that a new AD application was created with hello name you provided toohello script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a><span data-ttu-id="62cfe-144">Etapas tooget um token válido</span><span class="sxs-lookup"><span data-stu-id="62cfe-144">Steps tooget a valid token</span></span>
1. <span data-ttu-id="62cfe-145">Chamar a API de saudação com hello parâmetros a seguir e certifique-se de que tooreplace Olá LOCATÁRIO\_ID, o cliente\_ID e o cliente\_segredo:</span><span class="sxs-lookup"><span data-stu-id="62cfe-145">Call hello API with hello following parameters and make sure tooreplace hello TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="62cfe-146">**URL da solicitação** como *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span><span class="sxs-lookup"><span data-stu-id="62cfe-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="62cfe-147">**Cabeçalho HTTP Content-Type** : *application/x-www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="62cfe-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="62cfe-148">**Corpo da Solicitação HTTP** como *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="62cfe-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="62cfe-149">a seguir Olá é um exemplo de solicitação:</span><span class="sxs-lookup"><span data-stu-id="62cfe-149">hello following is an example request:</span></span>
     
       <span data-ttu-id="62cfe-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="62cfe-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="62cfe-151">Aqui está um exemplo de resposta:</span><span class="sxs-lookup"><span data-stu-id="62cfe-151">Here is an example response:</span></span>
     
       <span data-ttu-id="62cfe-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="62cfe-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="62cfe-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="62cfe-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="62cfe-154">Este exemplo incluído a codificação de URL de parâmetros de POSTAGEM Olá, `resource` valor é realmente `https://management.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="62cfe-154">This example included URL encoding of hello POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="62cfe-155">Tenha cuidado de codificação de URL tooalso `{CLIENT_SECRET}` pois ele pode conter caracteres especiais.</span><span class="sxs-lookup"><span data-stu-id="62cfe-155">Be careful tooalso URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="62cfe-156">Para testar, é possível usar uma ferramenta de cliente HTTP como o [Fiddler](http://www.telerik.com/fiddler) ou a [extensão Chrome Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span><span class="sxs-lookup"><span data-stu-id="62cfe-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="62cfe-157">Agora em cada chamada de API, cabeçalho de solicitação de autorização Olá incluem:</span><span class="sxs-lookup"><span data-stu-id="62cfe-157">Now in every API call, include hello authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="62cfe-158">Se você receber um código de 401 status retornado, verificação de corpo de resposta hello, ele pode informar Olá token tiver expirado.</span><span class="sxs-lookup"><span data-stu-id="62cfe-158">If you get a 401 status code returned, check hello response body, it might tell you hello token is expired.</span></span> <span data-ttu-id="62cfe-159">Nesse caso, obtenha um novo token.</span><span class="sxs-lookup"><span data-stu-id="62cfe-159">In that case, get a new token.</span></span>

## <a name="using-hello-apis"></a><span data-ttu-id="62cfe-160">Usando APIs de saudação</span><span class="sxs-lookup"><span data-stu-id="62cfe-160">Using hello APIs</span></span>
<span data-ttu-id="62cfe-161">Agora que você tem um token válido, você está pronto toomake Olá API chamadas.</span><span class="sxs-lookup"><span data-stu-id="62cfe-161">Now that you have a valid token, you are ready toomake hello API calls.</span></span>

1. <span data-ttu-id="62cfe-162">Cada solicitação de API, você precisará toopass um token válido, ainda que você obteve na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="62cfe-162">In each API request, you will need toopass a valid, unexpired token which you obtained in hello previous section.</span></span>
2. <span data-ttu-id="62cfe-163">Você precisará tooplug em alguns parâmetros na solicitação Olá URI que identifica seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="62cfe-163">You will need tooplug in some parameters into hello request URI which identifies your application.</span></span> <span data-ttu-id="62cfe-164">URI de solicitação Olá semelhante ao seguinte Olá</span><span class="sxs-lookup"><span data-stu-id="62cfe-164">hello request URI looks like hello following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="62cfe-165">parâmetros de saudação tooget, clique no nome do seu aplicativo e clique em Painel de controle e você verá uma página como a seguir Olá com todos os Olá 3 parâmetros.</span><span class="sxs-lookup"><span data-stu-id="62cfe-165">tooget hello parameters, click on your application name and click Dashboard and you will see a page like hello following with all hello 3 parameters.</span></span>
   
   * <span data-ttu-id="62cfe-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="62cfe-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="62cfe-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="62cfe-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="62cfe-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="62cfe-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="62cfe-169">**4** nome de seu grupo de recursos será toobe **MobileEngagement** , a menos que você criou um novo.</span><span class="sxs-lookup"><span data-stu-id="62cfe-169">**4** Your Resource Group name is going toobe **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Parâmetros de URI da API do Mobile Engagement][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="62cfe-171">Ignorar Olá API raiz endereço como era para Olá APIs anteriores.</span><span class="sxs-lookup"><span data-stu-id="62cfe-171">Ignore hello API Root Address as this was for hello previous APIs.</span></span><br/>
> 2. <span data-ttu-id="62cfe-172">Se você criou o aplicativo hello usando o portal clássico do Azure, em seguida, você precisa de nome de recurso de aplicativo de Olá toouse que é diferente do nome de aplicativo hello em si.</span><span class="sxs-lookup"><span data-stu-id="62cfe-172">If you created hello app using Azure Classic portal then you need toouse hello Application Resource name which is different than hello Application name itself.</span></span> <span data-ttu-id="62cfe-173">Se você criou o aplicativo hello no hello Portal do Azure, em seguida, você deve usar Olá nome do aplicativo em si (não há nenhuma diferenciação entre o nome de recurso do aplicativo e o nome do aplicativo para aplicativos criados no novo portal de saudação).</span><span class="sxs-lookup"><span data-stu-id="62cfe-173">If you created hello app in hello Azure Portal then you should use hello App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in hello new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



