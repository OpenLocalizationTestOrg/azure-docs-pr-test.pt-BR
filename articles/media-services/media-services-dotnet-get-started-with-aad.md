---
title: "Usar a autenticação do Azure AD para acessar a API dos Serviços de Mídia do Azure com o .NET | Microsoft Docs"
description: "Este tópico mostra como usar a autenticação do Azure AD (Azure Active Directory) para acessar a API do AMS (Serviços de Mídia do Azure) com o .NET."
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
ms.openlocfilehash: a9355200a05a3aa1b494b76977d38ddc42bfe179
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-ad-authentication-to-access-azure-media-services-api-with-net"></a><span data-ttu-id="33529-103">Usar a autenticação do Azure AD para acessar a API dos Serviços de Mídia do Azure com o .NET</span><span class="sxs-lookup"><span data-stu-id="33529-103">Use Azure AD authentication to access Azure Media Services API with .NET</span></span>

<span data-ttu-id="33529-104">A partir do windowsazure.mediaservices 4.0.0.4, os Serviços de Mídia do Azure dão suporte à autenticação baseada no Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="33529-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="33529-105">Este tópico mostra como usar a autenticação do Azure AD para acessar a API dos Serviços de Mídia do Azure com o Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="33529-105">This topic shows you how to use Azure AD  authentication to access Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33529-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="33529-106">Prerequisites</span></span>

- <span data-ttu-id="33529-107">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="33529-107">An Azure account.</span></span> <span data-ttu-id="33529-108">Para obter detalhes, confira [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33529-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="33529-109">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="33529-109">A Media Services account.</span></span> <span data-ttu-id="33529-110">Para obter mais informações, consulte [Criar uma conta dos Serviços de Mídia do Azure usando o portal do Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="33529-110">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="33529-111">O último pacote [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices).</span><span class="sxs-lookup"><span data-stu-id="33529-111">The latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="33529-112">Familiaridade com o tópico [Visão geral do acesso à API dos Serviços de Mídia do Azure com a autenticação do AAD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="33529-112">Familiarity with the topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="33529-113">Ao usar a autenticação do Azure AD com os Serviços de Mídia do Azure, você pode fazer a autenticação usando uma destas duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="33529-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="33529-114">A **autenticação de usuário** autentica uma pessoa que está usando o aplicativo para interagir com os recursos dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="33529-114">**User authentication** authenticates a person who is using the app to interact with Azure Media Services resources.</span></span> <span data-ttu-id="33529-115">O aplicativo interativo deve primeiro solicitar ao usuário as credenciais.</span><span class="sxs-lookup"><span data-stu-id="33529-115">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="33529-116">Um exemplo é um aplicativo de console de gerenciamento usado por usuários autorizados para monitorar trabalhos de codificação ou uma transmissão ao vivo.</span><span class="sxs-lookup"><span data-stu-id="33529-116">An example is a management console app that's used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="33529-117">A **autenticação de entidade de serviço** autentica um serviço.</span><span class="sxs-lookup"><span data-stu-id="33529-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="33529-118">Os aplicativos que geralmente usam esse método de autenticação são aplicativos que executam serviços daemon, serviços de camada intermediária ou trabalhos agendados, como aplicativos Web, aplicativos de funções, aplicativos lógicos, APIs ou microsserviços.</span><span class="sxs-lookup"><span data-stu-id="33529-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="33529-119">Atualmente, os Serviços de Mídia do Azure dão suporte a um modelo de autenticação do Serviço de Controle de Acesso do Azure.</span><span class="sxs-lookup"><span data-stu-id="33529-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="33529-120">No entanto, a autorização de Controle de Acesso será preterida em 1º de junho de 2018.</span><span class="sxs-lookup"><span data-stu-id="33529-120">However, Access Control authorization is going to be deprecated on June 1, 2018.</span></span> <span data-ttu-id="33529-121">Recomendamos que você migre para o modelo de autenticação do Azure Active Directory assim que possível.</span><span class="sxs-lookup"><span data-stu-id="33529-121">We recommend that you migrate to an Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="33529-122">Obter um token de acesso do Azure AD</span><span class="sxs-lookup"><span data-stu-id="33529-122">Get an Azure AD access token</span></span>

<span data-ttu-id="33529-123">Para se conectar à API dos Serviços de Mídia do Azure com a autenticação do Azure AD, o aplicativo cliente precisa solicitar um token de acesso do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33529-123">To connect to the Azure Media Services API with Azure AD authentication, the client app needs to request an Azure AD access token.</span></span> <span data-ttu-id="33529-124">Quando você usa o SDK de cliente do .NET dos Serviços de Mídia, vários detalhes sobre como adquirir um token de acesso do Azure AD são encapsulados e simplificados para você nas classes [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) e [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs).</span><span class="sxs-lookup"><span data-stu-id="33529-124">When you use the Media Services .NET client SDK, many of the details about how to acquire an Azure AD access token are wrapped and simplified for you in the [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="33529-125">Por exemplo, você não precisa fornecer a autoridade do Azure AD, o URI de recurso dos Serviços de Mídia ou os detalhes do aplicativo nativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33529-125">For example, you don't need to provide the Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="33529-126">Esses são valores conhecidos que já são configurados pela classe de provedor do token de acesso do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33529-126">These are well-known values that are already configured by the Azure AD access token provider class.</span></span> 

<span data-ttu-id="33529-127">Se você não estiver usando o SDK do .NET dos Serviços de Mídia do Azure, recomendamos que você use a [Biblioteca de Autenticação do Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="33529-127">If you are not using Azure Media Service .NET SDK, we recommend that you use the [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="33529-128">Para obter valores para os parâmetros que você precisa usar com a Biblioteca de Autenticação do Azure AD, consulte [Usar o portal do Azure para acessar as configurações de autenticação do Azure AD](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="33529-128">To get values for the parameters that you need to use with Azure AD Authentication Library, see [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="33529-129">Você também tem a opção de substituir a implementação padrão do **AzureAdTokenProvider** por sua própria implementação.</span><span class="sxs-lookup"><span data-stu-id="33529-129">You also have the option of replacing the default implementation of the **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="33529-130">Instalar e configurar o SDK do .NET dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="33529-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="33529-131">Para usar a autenticação do Azure AD com o SDK do .NET dos Serviços de Mídia, você precisa ter a última versão do pacote [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices).</span><span class="sxs-lookup"><span data-stu-id="33529-131">To use Azure AD authentication with the Media Services .NET SDK, you need to have the latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="33529-132">Além disso, adicione uma referência ao assembly **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="33529-132">Also, add a reference to the **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="33529-133">Se estiver usando um aplicativo existente, inclua o assembly **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll**.</span><span class="sxs-lookup"><span data-stu-id="33529-133">If you are using an existing app, include the **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="33529-134">No Visual Studio, crie um novo aplicativo de console C#.</span><span class="sxs-lookup"><span data-stu-id="33529-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="33529-135">Use o pacote NuGet [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) para instalar o **SDK do .NET dos Serviços de Mídia do Azure**.</span><span class="sxs-lookup"><span data-stu-id="33529-135">Use the [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package to install **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="33529-136">Para adicionar referências usando o NuGet, realize as seguintes etapas: no **Gerenciador de Soluções**, clique com o botão direito do mouse no nome do projeto e, depois, selecione **Gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="33529-136">To add references by using NuGet, take the following steps: in **Solution Explorer**, right-click the project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="33529-137">Em seguida, pesquise **windowsazure.mediaservices** e selecione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="33529-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="33529-138">-ou-</span><span class="sxs-lookup"><span data-stu-id="33529-138">-or-</span></span>

    <span data-ttu-id="33529-139">Execute o comando a seguir no **Console do Gerenciador de Pacotes** do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33529-139">Run the following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="33529-140">Adicione **using** ao código-fonte.</span><span class="sxs-lookup"><span data-stu-id="33529-140">Add **using** to your source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="33529-141">Usar a autenticação de usuário</span><span class="sxs-lookup"><span data-stu-id="33529-141">Use user authentication</span></span>

<span data-ttu-id="33529-142">Para se conectar à API dos Serviços de Mídia do Azure com a opção de autenticação de usuário, o aplicativo cliente precisa solicitar um token do Azure AD usando os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="33529-142">To connect to the Azure Media Service API with the user authentication option, the client app needs to request an Azure AD token by using the following parameters:</span></span>  

- <span data-ttu-id="33529-143">Ponto de extremidade do locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33529-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="33529-144">As informações do locatário podem ser recuperadas no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="33529-144">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="33529-145">Focalize o usuário conectado no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="33529-145">Hover over the signed-in user in the upper-right corner.</span></span>
- <span data-ttu-id="33529-146">URI de recurso dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="33529-146">Media Services resource URI.</span></span>
- <span data-ttu-id="33529-147">ID do cliente do aplicativo (nativo) dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="33529-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="33529-148">URI de redirecionamento do aplicativo (nativo) dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="33529-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="33529-149">Os valores desses parâmetros podem ser encontrados em **AzureEnvironments.AzureCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="33529-149">The values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="33529-150">A constante **AzureEnvironments.AzureCloudEnvironment** é um auxiliar no SDK do .NET para obtenção das configurações de variável de ambiente corretas de um Data Center público do Azure.</span><span class="sxs-lookup"><span data-stu-id="33529-150">The **AzureEnvironments.AzureCloudEnvironment** constant is a helper in the .NET SDK to get the right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="33529-151">Ela contém configurações de ambiente predefinidas para acessar os Serviços de Mídia apenas nos data centers públicos.</span><span class="sxs-lookup"><span data-stu-id="33529-151">It contains pre-defined environment settings for accessing Media Services in the public data centers only.</span></span> <span data-ttu-id="33529-152">Para regiões de nuvem soberana ou governamental, use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** ou **AzureGermanCloudEnvironment**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="33529-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="33529-153">O seguinte exemplo de código cria um token:</span><span class="sxs-lookup"><span data-stu-id="33529-153">The following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="33529-154">Para começar a programar nos Serviços de Mídia, você precisa criar uma instância **CloudMediaContext** que representa o contexto de servidor.</span><span class="sxs-lookup"><span data-stu-id="33529-154">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="33529-155">O **CloudMediaContext** inclui referências para coleções importantes incluindo trabalhos, ativos, arquivos, políticas de acesso e localizadores.</span><span class="sxs-lookup"><span data-stu-id="33529-155">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="33529-156">Você também precisa passar o **URI de recurso dos Serviços de Mídia REST** para o construtor **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="33529-156">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span></span> <span data-ttu-id="33529-157">Para obter o URI de recurso dos Serviços REST de Mídia, entre no portal do Azure, selecione sua conta dos Serviços de Mídia do Azure, selecione **Acesso à API** e, em seguida, selecione **Conectar aos Serviços de Mídia do Azure com a autenticação de usuário**.</span><span class="sxs-lookup"><span data-stu-id="33529-157">To get the resource URI for Media REST Services, sign in to the Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect to Azure Media Services with user authentication**.</span></span> 

<span data-ttu-id="33529-158">O seguinte exemplo de código cria uma instância **CloudMediaContext**:</span><span class="sxs-lookup"><span data-stu-id="33529-158">The following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="33529-159">O seguinte exemplo mostra como criar o token do Azure AD e o contexto:</span><span class="sxs-lookup"><span data-stu-id="33529-159">The following example shows how to create the Azure AD token and the context:</span></span>

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
><span data-ttu-id="33529-160">Se você receber uma exceção informando que “O servidor remoto retornou um erro: (401) Não autorizado”, consulte a seção [Controle de acesso](media-services-use-aad-auth-to-access-ams-api.md#access-control) de Visão geral do acesso à API dos Serviços de Mídia do Azure com a autenticação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33529-160">If you get an exception that says "The remote server returned an error: (401) Unauthorized," see the [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="33529-161">Usar a autenticação de entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="33529-161">Use service principal authentication</span></span>
    
<span data-ttu-id="33529-162">Para se conectar à API dos Serviços de Mídia do Azure com a opção de entidade de serviço, o aplicativo de camada intermediária (API Web ou aplicativo Web) precisa solicitar um token do Azure AD com os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="33529-162">To connect to the Azure Media Services API with the service principal option, your middle-tier app (web API or web application) needs to requests an Azure AD token with the following parameters:</span></span>  

- <span data-ttu-id="33529-163">Ponto de extremidade do locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33529-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="33529-164">As informações do locatário podem ser recuperadas no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="33529-164">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="33529-165">Focalize o usuário conectado no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="33529-165">Hover over the signed-in user in the upper-right corner.</span></span>
- <span data-ttu-id="33529-166">URI de recurso dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="33529-166">Media Services resource URI.</span></span>
- <span data-ttu-id="33529-167">Valores do aplicativo do Azure AD: a **ID do Cliente** e o **Segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="33529-167">Azure AD application values: the **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="33529-168">Os valores dos parâmetros **ID do Cliente** e **Segredo do cliente** podem ser encontrados no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="33529-168">The values for the **Client ID** and **Client secret** parameters can be found in the Azure portal.</span></span> <span data-ttu-id="33529-169">Para obter mais informações, consulte [Introdução à autenticação do Azure AD usando o portal do Azure](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="33529-169">For more information, see [Getting started with Azure AD authentication using the Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="33529-170">O seguinte exemplo de código cria um token usando o construtor **AzureAdTokenCredentials** que usa **AzureAdClientSymmetricKey** como parâmetro:</span><span class="sxs-lookup"><span data-stu-id="33529-170">The following code example creates a token by using the **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="33529-171">Você também pode especificar o construtor **AzureAdTokenCredentials** que usa **AzureAdClientCertificate** como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="33529-171">You can also specify the **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="33529-172">Para obter instruções sobre como criar e configurar um certificado em um formato que pode ser usado pelo Azure AD, consulte [Autenticando no Azure AD em aplicativos daemon com certificados – etapas de configuração manual](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span><span class="sxs-lookup"><span data-stu-id="33529-172">For instructions about how to create and configure a certificate in a form that can be used by Azure AD, see [Authenticating to Azure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="33529-173">Para começar a programar nos Serviços de Mídia, você precisa criar uma instância **CloudMediaContext** que representa o contexto de servidor.</span><span class="sxs-lookup"><span data-stu-id="33529-173">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="33529-174">Você também precisa passar o **URI de recurso dos Serviços de Mídia REST** para o construtor **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="33529-174">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span></span> <span data-ttu-id="33529-175">Também obtenha o valor do **URI de recurso dos Serviços REST de Mídia** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="33529-175">You can get the **resource URI for Media REST Services** value from the Azure portal as well.</span></span>

<span data-ttu-id="33529-176">O seguinte exemplo de código cria uma instância **CloudMediaContext**:</span><span class="sxs-lookup"><span data-stu-id="33529-176">The following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="33529-177">O seguinte exemplo mostra como criar o token do Azure AD e o contexto:</span><span class="sxs-lookup"><span data-stu-id="33529-177">The following example shows how to create the Azure AD token and the context:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="33529-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33529-178">Next steps</span></span>

<span data-ttu-id="33529-179">Comece a [carregar arquivos para sua conta](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="33529-179">Get started with [uploading files to your account](media-services-dotnet-upload-files.md).</span></span>
