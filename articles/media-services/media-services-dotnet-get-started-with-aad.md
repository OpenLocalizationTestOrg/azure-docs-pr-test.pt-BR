---
title: "aaaUse tooaccess de autenticação do AD do Azure API de serviços de mídia do Azure com o .NET | Microsoft Docs"
description: "Este tópico mostra como toouse tooaccess de autenticação do Azure Active Directory (AD do Azure) do Azure Media Services (AMS) API com .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a><span data-ttu-id="01cb4-103">Usar tooaccess de autenticação do AD do Azure API de serviços de mídia do Azure com .NET</span><span class="sxs-lookup"><span data-stu-id="01cb4-103">Use Azure AD authentication tooaccess Azure Media Services API with .NET</span></span>

<span data-ttu-id="01cb4-104">A partir do windowsazure.mediaservices 4.0.0.4, os Serviços de Mídia do Azure dão suporte à autenticação baseada no Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="01cb4-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="01cb4-105">Este tópico mostra como toouse tooaccess de autenticação do AD do Azure API de serviços de mídia do Azure com o Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="01cb4-105">This topic shows you how toouse Azure AD  authentication tooaccess Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01cb4-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="01cb4-106">Prerequisites</span></span>

- <span data-ttu-id="01cb4-107">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb4-107">An Azure account.</span></span> <span data-ttu-id="01cb4-108">Para obter detalhes, confira [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="01cb4-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="01cb4-109">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="01cb4-109">A Media Services account.</span></span> <span data-ttu-id="01cb4-110">Para obter mais informações, consulte [criar uma conta de serviços de mídia do Azure usando o portal do Azure de saudação](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="01cb4-110">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="01cb4-111">Olá mais recente [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pacote.</span><span class="sxs-lookup"><span data-stu-id="01cb4-111">hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="01cb4-112">Familiaridade com o tópico Olá [acessar API do Azure Media Services visão geral de autenticação do AAD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="01cb4-112">Familiarity with hello topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="01cb4-113">Ao usar a autenticação do Azure AD com os Serviços de Mídia do Azure, você pode fazer a autenticação usando uma destas duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="01cb4-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="01cb4-114">**Autenticação de usuário** autentica um usuário que está usando Olá aplicativo toointeract com recursos de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb4-114">**User authentication** authenticates a person who is using hello app toointeract with Azure Media Services resources.</span></span> <span data-ttu-id="01cb4-115">aplicativo interativo do Hello primeiro deve solicitar credenciais ao usuário Olá.</span><span class="sxs-lookup"><span data-stu-id="01cb4-115">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="01cb4-116">Um exemplo é um aplicativo de console de gerenciamento que é usado por usuários autorizados toomonitor trabalhos de codificação ou transmissão ao vivo.</span><span class="sxs-lookup"><span data-stu-id="01cb4-116">An example is a management console app that's used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="01cb4-117">A **autenticação de entidade de serviço** autentica um serviço.</span><span class="sxs-lookup"><span data-stu-id="01cb4-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="01cb4-118">Os aplicativos que geralmente usam esse método de autenticação são aplicativos que executam serviços daemon, serviços de camada intermediária ou trabalhos agendados, como aplicativos Web, aplicativos de funções, aplicativos lógicos, APIs ou microsserviços.</span><span class="sxs-lookup"><span data-stu-id="01cb4-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="01cb4-119">Atualmente, os Serviços de Mídia do Azure dão suporte a um modelo de autenticação do Serviço de Controle de Acesso do Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb4-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="01cb4-120">No entanto, a autorização de controle de acesso será toobe preterido no dia 1 de junho de 2018.</span><span class="sxs-lookup"><span data-stu-id="01cb4-120">However, Access Control authorization is going toobe deprecated on June 1, 2018.</span></span> <span data-ttu-id="01cb4-121">É recomendável que você migre o modelo de autenticação do Active Directory do Azure tooan assim que possível.</span><span class="sxs-lookup"><span data-stu-id="01cb4-121">We recommend that you migrate tooan Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="01cb4-122">Obter um token de acesso do Azure AD</span><span class="sxs-lookup"><span data-stu-id="01cb4-122">Get an Azure AD access token</span></span>

<span data-ttu-id="01cb4-123">tooconnect toohello API de serviços de mídia do Azure com a autenticação do AD do Azure, o aplicativo de cliente de Olá precisa toorequest um token de acesso do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb4-123">tooconnect toohello Azure Media Services API with Azure AD authentication, hello client app needs toorequest an Azure AD access token.</span></span> <span data-ttu-id="01cb4-124">Quando você usa o cliente .NET de serviços de mídia de saudação SDK, muitos dos detalhes de saudação sobre como tooacquire um token de acesso do AD do Azure são encapsuladas e simplificada para você no hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) e [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span><span class="sxs-lookup"><span data-stu-id="01cb4-124">When you use hello Media Services .NET client SDK, many of hello details about how tooacquire an Azure AD access token are wrapped and simplified for you in hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="01cb4-125">Por exemplo, você não precisa tooprovide autoridade de saudação do AD do Azure, o URI de recurso de serviços de mídia ou o nativo detalhes do aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01cb4-125">For example, you don't need tooprovide hello Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="01cb4-126">Estes são os valores conhecidos que já são configurados por Olá classe de provedor de token de acesso do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb4-126">These are well-known values that are already configured by hello Azure AD access token provider class.</span></span> 

<span data-ttu-id="01cb4-127">Se você não estiver usando o SDK do .NET do Azure Media Service, recomendamos que você use Olá [biblioteca de autenticação do AD do Azure](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="01cb4-127">If you are not using Azure Media Service .NET SDK, we recommend that you use hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="01cb4-128">tooget valores para parâmetros de saudação que você precisa toouse com biblioteca de autenticação do AD do Azure, consulte [usar configurações de autenticação tooaccess portal do Azure AD do Azure Olá](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="01cb4-128">tooget values for hello parameters that you need toouse with Azure AD Authentication Library, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="01cb4-129">Você também tem a opção de saudação de substituir a implementação padrão Olá Olá **AzureAdTokenProvider** com sua própria implementação.</span><span class="sxs-lookup"><span data-stu-id="01cb4-129">You also have hello option of replacing hello default implementation of hello **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="01cb4-130">Instalar e configurar o SDK do .NET dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="01cb4-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="01cb4-131">autenticação toouse AD do Azure com hello SDK do Media Services .NET, você precisa toohave hello mais recente [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pacote.</span><span class="sxs-lookup"><span data-stu-id="01cb4-131">toouse Azure AD authentication with hello Media Services .NET SDK, you need toohave hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="01cb4-132">Além disso, adicione uma referência toohello **ActiveDirectory** assembly.</span><span class="sxs-lookup"><span data-stu-id="01cb4-132">Also, add a reference toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="01cb4-133">Se você estiver usando um aplicativo existente, incluem hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span><span class="sxs-lookup"><span data-stu-id="01cb4-133">If you are using an existing app, include hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="01cb4-134">No Visual Studio, crie um novo aplicativo de console C#.</span><span class="sxs-lookup"><span data-stu-id="01cb4-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="01cb4-135">Saudação de uso [windowsazure. mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall de pacote do NuGet **SDK do Azure Media Services .NET**.</span><span class="sxs-lookup"><span data-stu-id="01cb4-135">Use hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package tooinstall **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="01cb4-136">referências de tooadd usando o NuGet, levar Olá etapas a seguir: em **Solution Explorer**, nome do projeto hello e, em seguida, selecione **gerenciar pacotes do NuGet**.</span><span class="sxs-lookup"><span data-stu-id="01cb4-136">tooadd references by using NuGet, take hello following steps: in **Solution Explorer**, right-click hello project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="01cb4-137">Em seguida, pesquise **windowsazure.mediaservices** e selecione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="01cb4-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="01cb4-138">-ou-</span><span class="sxs-lookup"><span data-stu-id="01cb4-138">-or-</span></span>

    <span data-ttu-id="01cb4-139">Execução hello seguinte comando no **Package Manager Console** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="01cb4-139">Run hello following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="01cb4-140">Adicionar **usando** tooyour código-fonte.</span><span class="sxs-lookup"><span data-stu-id="01cb4-140">Add **using** tooyour source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="01cb4-141">Usar a autenticação de usuário</span><span class="sxs-lookup"><span data-stu-id="01cb4-141">Use user authentication</span></span>

<span data-ttu-id="01cb4-142">tooconnect toohello API de serviços de mídia do Azure com a opção de autenticação de usuário hello, aplicativo de cliente Olá precisa toorequest um token do AD do Azure usando Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="01cb4-142">tooconnect toohello Azure Media Service API with hello user authentication option, hello client app needs toorequest an Azure AD token by using hello following parameters:</span></span>  

- <span data-ttu-id="01cb4-143">Ponto de extremidade do locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01cb4-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="01cb4-144">informações de locatário Olá podem ser recuperadas da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb4-144">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="01cb4-145">Passe o mouse sobre Olá assinado usuário no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="01cb4-145">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="01cb4-146">URI de recurso dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="01cb4-146">Media Services resource URI.</span></span>
- <span data-ttu-id="01cb4-147">ID do cliente do aplicativo (nativo) dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="01cb4-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="01cb4-148">URI de redirecionamento do aplicativo (nativo) dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="01cb4-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="01cb4-149">valores de saudação para esses parâmetros podem ser encontrados em **AzureEnvironments.AzureCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="01cb4-149">hello values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="01cb4-150">Olá **AzureEnvironments.AzureCloudEnvironment** constante é um auxiliar na Olá .NET SDK tooget definições de variável de ambiente certo Olá para um Data Center pública do Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb4-150">hello **AzureEnvironments.AzureCloudEnvironment** constant is a helper in hello .NET SDK tooget hello right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="01cb4-151">Ele contém configurações de ambiente predefinida para acessar os serviços de mídia em centros de dados públicos Olá somente.</span><span class="sxs-lookup"><span data-stu-id="01cb4-151">It contains pre-defined environment settings for accessing Media Services in hello public data centers only.</span></span> <span data-ttu-id="01cb4-152">Para regiões de nuvem soberana ou governamental, use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** ou **AzureGermanCloudEnvironment**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="01cb4-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="01cb4-153">saudação de exemplo de código a seguir cria um token:</span><span class="sxs-lookup"><span data-stu-id="01cb4-153">hello following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="01cb4-154">toostart programação no Media Services, você precisa toocreate um **CloudMediaContext** instância que representa o contexto de saudação do servidor.</span><span class="sxs-lookup"><span data-stu-id="01cb4-154">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="01cb4-155">Olá **CloudMediaContext** inclui referências tooimportant coleções incluindo trabalhos, ativos, arquivos, políticas de acesso e localizadores.</span><span class="sxs-lookup"><span data-stu-id="01cb4-155">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="01cb4-156">Você também precisa toopass Olá **URI do Media Services de REST do recurso** toohello **CloudMediaContext** construtor.</span><span class="sxs-lookup"><span data-stu-id="01cb4-156">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="01cb4-157">URI de recurso Olá tooget serviços REST de mídia de entrada toohello portal do Azure, selecione sua conta de serviços de mídia do Azure, selecione **acesso à API**e, em seguida, selecione **conectar os serviços de mídia tooAzure com usuário autenticação**.</span><span class="sxs-lookup"><span data-stu-id="01cb4-157">tooget hello resource URI for Media REST Services, sign in toohello Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect tooAzure Media Services with user authentication**.</span></span> 

<span data-ttu-id="01cb4-158">Olá exemplo de código a seguir cria um **CloudMediaContext** instância:</span><span class="sxs-lookup"><span data-stu-id="01cb4-158">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="01cb4-159">saudação de exemplo a seguir mostra como toocreate Olá contexto de token e saudação do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="01cb4-159">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
><span data-ttu-id="01cb4-160">Se você obtiver uma exceção que diz "servidor remoto Olá retornou um erro: não autorizado (401)," consulte Olá [controle de acesso](media-services-use-aad-auth-to-access-ams-api.md#access-control) seção acesso a API de serviços de mídia do Azure com visão geral de autenticação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb4-160">If you get an exception that says "hello remote server returned an error: (401) Unauthorized," see hello [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="01cb4-161">Usar a autenticação de entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="01cb4-161">Use service principal authentication</span></span>
    
<span data-ttu-id="01cb4-162">tooconnect toohello API de serviços de mídia do Azure com a opção de entidade de serviço hello, seu aplicativo de camada intermediária (API da web ou aplicativo web) precisa toorequests um token do AD do Azure com hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="01cb4-162">tooconnect toohello Azure Media Services API with hello service principal option, your middle-tier app (web API or web application) needs toorequests an Azure AD token with hello following parameters:</span></span>  

- <span data-ttu-id="01cb4-163">Ponto de extremidade do locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01cb4-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="01cb4-164">informações de locatário Olá podem ser recuperadas da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb4-164">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="01cb4-165">Passe o mouse sobre Olá assinado usuário no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="01cb4-165">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="01cb4-166">URI de recurso dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="01cb4-166">Media Services resource URI.</span></span>
- <span data-ttu-id="01cb4-167">Valores de aplicativo do Azure AD: Olá **ID do cliente** e **segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="01cb4-167">Azure AD application values: hello **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="01cb4-168">Olá valores hello **ID do cliente** e **segredo do cliente** parâmetros podem ser encontrados no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb4-168">hello values for hello **Client ID** and **Client secret** parameters can be found in hello Azure portal.</span></span> <span data-ttu-id="01cb4-169">Para obter mais informações, consulte [guia de Introdução com o uso de autenticação do AD do Azure Olá portal do Azure](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="01cb4-169">For more information, see [Getting started with Azure AD authentication using hello Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="01cb4-170">Olá exemplo de código a seguir cria um token usando Olá **AzureAdTokenCredentials** construtor **AzureAdClientSymmetricKey** como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="01cb4-170">hello following code example creates a token by using hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="01cb4-171">Você também pode especificar Olá **AzureAdTokenCredentials** construtor **AzureAdClientCertificate** como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="01cb4-171">You can also specify hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="01cb4-172">Para obter instruções sobre como toocreate e configurar um certificado em um formulário que pode ser usado pelo AD do Azure, consulte [tooAzure AD em aplicativos de daemon com certificados - etapas de configuração manual de autenticação](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span><span class="sxs-lookup"><span data-stu-id="01cb4-172">For instructions about how toocreate and configure a certificate in a form that can be used by Azure AD, see [Authenticating tooAzure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="01cb4-173">toostart programação no Media Services, você precisa toocreate um **CloudMediaContext** instância que representa o contexto de saudação do servidor.</span><span class="sxs-lookup"><span data-stu-id="01cb4-173">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="01cb4-174">Você também precisa toopass Olá **URI do Media Services de REST do recurso** toohello **CloudMediaContext** construtor.</span><span class="sxs-lookup"><span data-stu-id="01cb4-174">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="01cb4-175">Você pode obter Olá **URI do Media Services de REST do recurso** valor da saudação também portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="01cb4-175">You can get hello **resource URI for Media REST Services** value from hello Azure portal as well.</span></span>

<span data-ttu-id="01cb4-176">Olá exemplo de código a seguir cria um **CloudMediaContext** instância:</span><span class="sxs-lookup"><span data-stu-id="01cb4-176">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="01cb4-177">saudação de exemplo a seguir mostra como toocreate Olá contexto de token e saudação do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="01cb4-177">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a><span data-ttu-id="01cb4-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01cb4-178">Next steps</span></span>

<span data-ttu-id="01cb4-179">Introdução ao [carregando arquivos tooyour conta](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="01cb4-179">Get started with [uploading files tooyour account](media-services-dotnet-upload-files.md).</span></span>
