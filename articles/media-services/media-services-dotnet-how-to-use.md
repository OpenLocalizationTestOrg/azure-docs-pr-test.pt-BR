---
title: "Como configurar o computador para desenvolvimento dos serviços de mídia com o .NET"
description: "Conheça os pré-requisitos para os Serviços de Mídia usando o SDK dos Serviços de Mídia para .NET. Saiba também como criar um aplicativo do Visual Studio."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: 15828bc74937a036871b26493498232ec7cf6f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="ca7df-104">Desenvolvimento de serviços de mídia com o .NET</span><span class="sxs-lookup"><span data-stu-id="ca7df-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="ca7df-105">Este tópico discute como começar a desenvolver aplicativos de serviços de mídia usando o .NET.</span><span class="sxs-lookup"><span data-stu-id="ca7df-105">This topic discusses how to start developing Media Services applications using .NET.</span></span>

<span data-ttu-id="ca7df-106">A biblioteca do **SDK do .NET dos Serviços de Mídia** permite que você programe em relação aos serviços de mídia usando o .NET.</span><span class="sxs-lookup"><span data-stu-id="ca7df-106">The **Azure Media Services .NET SDK** library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="ca7df-107">Para facilitar ainda mais o desenvolvimento com o .NET, a biblioteca de **Extensões do SDK do .NET dos Serviços de Mídia** é fornecida.</span><span class="sxs-lookup"><span data-stu-id="ca7df-107">To make it even easier to develop with .NET, the **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="ca7df-108">Esta biblioteca contém um conjunto de métodos de extensão e funções auxiliares simplificam o seu código .NET.</span><span class="sxs-lookup"><span data-stu-id="ca7df-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="ca7df-109">As duas bibliotecas estão disponíveis por meio do **NuGet** e **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="ca7df-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca7df-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ca7df-110">Prerequisites</span></span>
* <span data-ttu-id="ca7df-111">Uma conta de Serviços de Mídia em uma assinatura nova ou existente do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca7df-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="ca7df-112">Confira o tópico [Criar uma conta dos Serviços de Mídia](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="ca7df-112">See the topic [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="ca7df-113">Sistemas operacionais: Windows 10, Windows 7, Windows 2008 R2 ou Windows 8.</span><span class="sxs-lookup"><span data-stu-id="ca7df-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="ca7df-114">.NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="ca7df-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="ca7df-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca7df-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="ca7df-116">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca7df-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="ca7df-117">Esta seção mostra como criar um projeto no Visual Studio e configurá-lo para o desenvolvimento de Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="ca7df-117">This section shows you how to create a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="ca7df-118">Nesse caso, o projeto é um aplicativo de console C# do Windows, mas as mesmas etapas de configuração mostradas aqui se aplicam a outros tipos de projetos que podem ser criados para aplicativos de Serviços de Mídia (por exemplo, um aplicativo do Windows Forms ou um aplicativo Web ASP .NET).</span><span class="sxs-lookup"><span data-stu-id="ca7df-118">In this case, the project is a C# Windows console application, but the same setup steps shown here apply to other types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="ca7df-119">Esta seção mostra como usar **NuGet** para adicionar extensões do SDK do .NET dos Serviços de Mídia e outras bibliotecas dependentes.</span><span class="sxs-lookup"><span data-stu-id="ca7df-119">This section shows how to use **NuGet** to add Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="ca7df-120">Como alternativa, você pode obter os bits mais recentes do SDK do .NET dos Serviços de Mídia no GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) ou [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), criar a solução e adicionar as referências ao projeto do cliente.</span><span class="sxs-lookup"><span data-stu-id="ca7df-120">Alternatively, you can get the latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build the solution, and add the references to the client project.</span></span> <span data-ttu-id="ca7df-121">Todas as dependências necessárias são baixadas e extraídas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ca7df-121">All the necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="ca7df-122">No Visual Studio, crie um novo aplicativo de console C#.</span><span class="sxs-lookup"><span data-stu-id="ca7df-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="ca7df-123">Digite o **Nome**, o **Local** e o **Nome da solução** e clique em OK.</span><span class="sxs-lookup"><span data-stu-id="ca7df-123">Enter the **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="ca7df-124">Compilar a solução.</span><span class="sxs-lookup"><span data-stu-id="ca7df-124">Build the solution.</span></span>
3. <span data-ttu-id="ca7df-125">Use o **NuGet** para instalar e adicionar as **Extensões do SDK do .NET dos Serviços de Mídia do Azure** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="ca7df-125">Use **NuGet** to install and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="ca7df-126">Instalar esse pacote também instala o **SDK do .NET dos Serviços de Mídia** e adiciona todas as outras dependências necessárias.</span><span class="sxs-lookup"><span data-stu-id="ca7df-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="ca7df-127">Certifique-se de que você tenha a versão mais recente do NuGet instalada.</span><span class="sxs-lookup"><span data-stu-id="ca7df-127">Ensure that you have the newest version of NuGet installed.</span></span> <span data-ttu-id="ca7df-128">Para obter mais informações e instruções de instalação, consulte [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="ca7df-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="ca7df-129">No Gerenciador de Soluções, clique com o botão direito no nome do projeto e escolha Gerenciar pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="ca7df-129">In Solution Explorer, right-click the name of the project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="ca7df-130">A caixa de diálogo Gerenciar Pacotes NuGet será exibida.</span><span class="sxs-lookup"><span data-stu-id="ca7df-130">The Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="ca7df-131">Na Galeria Online, procure por extensões de serviços de mídia do Azure, escolha extensões do SDK do .NET dos Serviços de Mídia e, em seguida, clique no botão Instalar.</span><span class="sxs-lookup"><span data-stu-id="ca7df-131">In the Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click the Install button.</span></span>
   
    <span data-ttu-id="ca7df-132">O projeto é modificado e faz referência às extensões do SDK do .NET dos Serviços de Mídia, ao SDK do .NET dos Serviços de Mídia e a outros assemblies dependentes adicionados.</span><span class="sxs-lookup"><span data-stu-id="ca7df-132">The project is modified and references to the Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="ca7df-133">Para promover um ambiente de desenvolvimento mais limpo, considere a ativação da restauração de pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="ca7df-133">To promote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="ca7df-134">Para obter mais informações, consulte [Restauração do pacote NuGet"](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="ca7df-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="ca7df-135">Adicionar uma referência ao assembly **System.Configuration** .</span><span class="sxs-lookup"><span data-stu-id="ca7df-135">Add a reference to **System.Configuration** assembly.</span></span> <span data-ttu-id="ca7df-136">Este assembly contém a classe System.Configuration.**ConfigurationManager** que é utilizada para acessar arquivos de configuração (por exemplo, App.config).</span><span class="sxs-lookup"><span data-stu-id="ca7df-136">This assembly contains the System.Configuration.**ConfigurationManager** class that is used to access configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="ca7df-137">Para adicionar referências usando a caixa de diálogo Gerenciar referências, clique com o botão direito do mouse no nome do projeto no Gerenciador de Soluções.</span><span class="sxs-lookup"><span data-stu-id="ca7df-137">To add references using the Manage References dialog, right-click the project name in the Solution Explorer.</span></span> <span data-ttu-id="ca7df-138">Em seguida, selecione Adicionar e Referências.</span><span class="sxs-lookup"><span data-stu-id="ca7df-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="ca7df-139">Aparece a caixa de diálogo Gerenciar referências.</span><span class="sxs-lookup"><span data-stu-id="ca7df-139">The Manage References dialog appears.</span></span>
8. <span data-ttu-id="ca7df-140">Em assemblies do .NET Framework, localize e selecione o assembly System.Configuration e pressione OK.</span><span class="sxs-lookup"><span data-stu-id="ca7df-140">Under .NET framework assemblies, find and select the System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="ca7df-141">Abra o arquivo App.config e adicione uma seção *appSettings* ao arquivo.</span><span class="sxs-lookup"><span data-stu-id="ca7df-141">Open the App.config file and add an *appSettings* section to the file.</span></span>     
   
    <span data-ttu-id="ca7df-142">Defina os valores necessários para conexão à API de Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="ca7df-142">Set the values that are needed to connect to the Media Services API.</span></span> <span data-ttu-id="ca7df-143">Para obter mais informações, consulte [Acessar a API dos Serviços de Mídia do Azure com autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ca7df-143">For more information, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="ca7df-144">Se você estiver usando [autenticação de usuário](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication), seu arquivo de configuração provavelmente terá valores para seu domínio de locatário do Azure AD e o ponto de extremidade de API de REST do AMS.</span><span class="sxs-lookup"><span data-stu-id="ca7df-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and the AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="ca7df-145">A maioria dos exemplos de código na documentação dos Serviços de Mídia do Azure usa um tipo de usuário (interativo) de autenticação para se conectar à API do AMS.</span><span class="sxs-lookup"><span data-stu-id="ca7df-145">Most code samples in the Azure Media Services documentation set, use a user (interactive) type of authentication to connect to the AMS API.</span></span> <span data-ttu-id="ca7df-146">Esse método de autenticação funcionará bem para gerenciamento ou monitoramento de aplicativos nativos: aplicativos móveis, aplicativos do Windows e aplicativos de Console.</span><span class="sxs-lookup"><span data-stu-id="ca7df-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="ca7df-147">Esse método de autenticação não é adequado para o servidor, serviços Web, tipo de aplicativos de APIs.</span><span class="sxs-lookup"><span data-stu-id="ca7df-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="ca7df-148">Para obter mais informações, consulte [Acessar a API do AMS com autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ca7df-148">For more information, see [Access the AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="ca7df-149">Substitua as instruções **using** existentes no início do arquivo Program.cs pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="ca7df-149">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="ca7df-150">Neste ponto, você está pronto para começar a desenvolver um aplicativo de Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="ca7df-150">At this point, you are ready to start developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="ca7df-151">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ca7df-151">Example</span></span>

<span data-ttu-id="ca7df-152">Aqui está um pequeno exemplo que se conecta à API do AMS e lista todos os Processadores de Mídia disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ca7df-152">Here is a small example that connects to the AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a><span data-ttu-id="ca7df-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca7df-153">Next steps</span></span>

<span data-ttu-id="ca7df-154">Agora [você pode conectar-se à API do AMS](media-services-use-aad-auth-to-access-ams-api.md) e começar a [desenvolver](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ca7df-154">Now [you can connect to the AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="ca7df-155">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="ca7df-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ca7df-156">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="ca7df-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

