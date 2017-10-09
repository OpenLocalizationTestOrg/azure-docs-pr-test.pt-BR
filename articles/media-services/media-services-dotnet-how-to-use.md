---
title: "aaaHow tooSet de computador para o desenvolvimento de serviços de mídia com .NET"
description: "Saiba mais sobre os pré-requisitos de saudação do Media Services usando Olá SDK do Media Services para .NET. Saiba também como toocreate um aplicativo do Visual Studio."
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
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="1e6e5-104">Desenvolvimento de serviços de mídia com o .NET</span><span class="sxs-lookup"><span data-stu-id="1e6e5-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="1e6e5-105">Este tópico discute como os serviços de mídia de toostart desenvolver aplicativos usando o .NET.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-105">This topic discusses how toostart developing Media Services applications using .NET.</span></span>

<span data-ttu-id="1e6e5-106">Olá **SDK do Azure Media Services .NET** biblioteca permite tooprogram em relação aos serviços de mídia usando o .NET.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-106">hello **Azure Media Services .NET SDK** library enables you tooprogram against Media Services using .NET.</span></span> <span data-ttu-id="1e6e5-107">toomake mesmo toodevelop mais fácil com o .NET, hello **extensões do SDK do Azure Media Services .NET** biblioteca é fornecida.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-107">toomake it even easier toodevelop with .NET, hello **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="1e6e5-108">Esta biblioteca contém um conjunto de métodos de extensão e funções auxiliares simplificam o seu código .NET.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="1e6e5-109">As duas bibliotecas estão disponíveis por meio do **NuGet** e **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e6e5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1e6e5-110">Prerequisites</span></span>
* <span data-ttu-id="1e6e5-111">Uma conta de Serviços de Mídia em uma assinatura nova ou existente do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="1e6e5-112">Consulte o tópico Olá [como tooCreate uma conta do Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="1e6e5-112">See hello topic [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="1e6e5-113">Sistemas operacionais: Windows 10, Windows 7, Windows 2008 R2 ou Windows 8.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="1e6e5-114">.NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="1e6e5-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="1e6e5-116">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1e6e5-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="1e6e5-117">Esta seção mostra como toocreate um projeto no Visual Studio e configurá-lo para o desenvolvimento de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-117">This section shows you how toocreate a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="1e6e5-118">Nesse caso, projeto de saudação é um aplicativo de console c# Windows, mas hello mesmas etapas de instalação mostradas aqui se aplicam tooother tipos de projetos, que você pode criar aplicativos de serviços de mídia (por exemplo, um aplicativo Windows Forms ou um aplicativo Web ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="1e6e5-118">In this case, hello project is a C# Windows console application, but hello same setup steps shown here apply tooother types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="1e6e5-119">Esta seção mostra como toouse **NuGet** tooadd SDK do Media Services .NET extensões e outras bibliotecas dependentes.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-119">This section shows how toouse **NuGet** tooadd Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="1e6e5-120">Como alternativa, você pode obter os bits mais recentes do SDK do Media Services .NET de saudação do GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) ou [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), compilar solução hello e adicionar projeto de cliente de toohello Olá referências.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-120">Alternatively, you can get hello latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build hello solution, and add hello references toohello client project.</span></span> <span data-ttu-id="1e6e5-121">Todas as dependências necessárias de saudação obtenham baixadas e extraídas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-121">All hello necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="1e6e5-122">No Visual Studio, crie um novo aplicativo de console C#.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="1e6e5-123">Digite hello **nome**, **local**, e **nome da solução**e, em seguida, clique em Okey.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-123">Enter hello **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="1e6e5-124">Compile a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-124">Build hello solution.</span></span>
3. <span data-ttu-id="1e6e5-125">Use **NuGet** tooinstall e adicione **extensões do SDK do Azure Media Services .NET** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="1e6e5-125">Use **NuGet** tooinstall and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="1e6e5-126">Instalar esse pacote também instala o **SDK do .NET dos Serviços de Mídia** e adiciona todas as outras dependências necessárias.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="1e6e5-127">Certifique-se de que você tem a versão mais recente de saudação do NuGet instalada.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-127">Ensure that you have hello newest version of NuGet installed.</span></span> <span data-ttu-id="1e6e5-128">Para obter mais informações e instruções de instalação, consulte [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="1e6e5-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="1e6e5-129">No Gerenciador de soluções, clique o nome de saudação do projeto de saudação e escolha gerenciar pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-129">In Solution Explorer, right-click hello name of hello project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="1e6e5-130">caixa de diálogo Gerenciar pacotes NuGet Olá é exibida.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-130">hello Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="1e6e5-131">Na Galeria de Online hello, pesquisa de extensões de serviços de mídia do Azure, escolha as extensões de SDK .NET do serviços de mídia do Azure e clique em botão de instalar hello.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-131">In hello Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click hello Install button.</span></span>
   
    <span data-ttu-id="1e6e5-132">projeto de saudação é modificado e referencia toohello extensões do SDK do Media Services .NET, SDK do Media Services .NET e outros assemblies dependentes são adicionados.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-132">hello project is modified and references toohello Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="1e6e5-133">toopromote um ambiente de desenvolvimento mais limpo, considere habilitar a restauração de pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-133">toopromote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="1e6e5-134">Para obter mais informações, consulte [Restauração do pacote NuGet"](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="1e6e5-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="1e6e5-135">Adicione uma referência muito**System. Configuration** assembly.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-135">Add a reference too**System.Configuration** assembly.</span></span> <span data-ttu-id="1e6e5-136">Este assembly contém Olá System. Configuration. **ConfigurationManager** classe que é usada tooaccess arquivos de configuração (por exemplo, App. config).</span><span class="sxs-lookup"><span data-stu-id="1e6e5-136">This assembly contains hello System.Configuration.**ConfigurationManager** class that is used tooaccess configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="1e6e5-137">referências de tooadd usando a caixa de diálogo de referências de gerenciar Olá, com o botão direito em nome do projeto Olá no hello Gerenciador de soluções.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-137">tooadd references using hello Manage References dialog, right-click hello project name in hello Solution Explorer.</span></span> <span data-ttu-id="1e6e5-138">Em seguida, selecione Adicionar e Referências.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="1e6e5-139">Olá Gerenciar referências aparecerá.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-139">hello Manage References dialog appears.</span></span>
8. <span data-ttu-id="1e6e5-140">Em assemblies do .NET framework, localize e selecione o assembly System. Configuration de saudação e pressione Okey.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-140">Under .NET framework assemblies, find and select hello System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="1e6e5-141">Abra o arquivo App. config de saudação e adicione um *appSettings* arquivo toohello de seção.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-141">Open hello App.config file and add an *appSettings* section toohello file.</span></span>     
   
    <span data-ttu-id="1e6e5-142">Definir valores de saudação que são necessárias tooconnect toohello API de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-142">Set hello values that are needed tooconnect toohello Media Services API.</span></span> <span data-ttu-id="1e6e5-143">Para obter mais informações, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="1e6e5-143">For more information, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="1e6e5-144">Se você estiver usando [autenticação de usuário](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) seu arquivo de configuração será provavelmente têm valores para o seu domínio de locatário do AD do Azure e Olá ponto de extremidade de API de REST AMS.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and hello AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="1e6e5-145">A maioria dos exemplos de código Olá documentação do Azure Media Services definido, use um tipo de usuário (interativo) de autenticação tooconnect toohello AMS API.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-145">Most code samples in hello Azure Media Services documentation set, use a user (interactive) type of authentication tooconnect toohello AMS API.</span></span> <span data-ttu-id="1e6e5-146">Esse método de autenticação funcionará bem para gerenciamento ou monitoramento de aplicativos nativos: aplicativos móveis, aplicativos do Windows e aplicativos de Console.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="1e6e5-147">Esse método de autenticação não é adequado para o servidor, serviços Web, tipo de aplicativos de APIs.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="1e6e5-148">Para obter mais informações, consulte [Olá acesso AMS API com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="1e6e5-148">For more information, see [Access hello AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="1e6e5-149">Substituir existente Olá **usando** instruções no início de saudação do arquivo Program.cs Olá Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-149">Overwrite hello existing **using** statements at hello beginning of hello Program.cs file with hello following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="1e6e5-150">Neste ponto, você está pronto toostart desenvolvendo um aplicativo de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-150">At this point, you are ready toostart developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="1e6e5-151">Exemplo</span><span class="sxs-lookup"><span data-stu-id="1e6e5-151">Example</span></span>

<span data-ttu-id="1e6e5-152">Aqui está um exemplo pequeno que se conecta toohello AMS API e lista todos os processadores de mídia disponíveis.</span><span class="sxs-lookup"><span data-stu-id="1e6e5-152">Here is a small example that connects toohello AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from hello App.config file.
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

##<a name="next-steps"></a><span data-ttu-id="1e6e5-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1e6e5-153">Next steps</span></span>

<span data-ttu-id="1e6e5-154">Agora [você pode se conectar toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) e iniciar [desenvolvendo](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1e6e5-154">Now [you can connect toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="1e6e5-155">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="1e6e5-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1e6e5-156">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="1e6e5-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

