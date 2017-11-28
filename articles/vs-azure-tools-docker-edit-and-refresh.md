---
title: "aplicativos de aaaDebugging em um contêiner de Docker local | Microsoft Docs"
description: "Saiba como toomodify um aplicativo que é executado em um contêiner de Docker local, atualizar o contêiner de saudação por meio de editar e atualizar e definir pontos de interrupção de depuração"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="e4519-103">Depuração de aplicativos em um contêiner de Docker local</span><span class="sxs-lookup"><span data-stu-id="e4519-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="e4519-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e4519-104">Overview</span></span>
<span data-ttu-id="e4519-105">Olá Visual Studio Tools para o Docker fornece uma toodevelop de maneira consistente em e validar seu aplicativo localmente em um contêiner do Docker do Linux.</span><span class="sxs-lookup"><span data-stu-id="e4519-105">hello Visual Studio Tools for Docker provides a consistent way toodevelop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="e4519-106">Você não tem contêiner de saudação toorestart cada vez que você faz com que um código de alteração.</span><span class="sxs-lookup"><span data-stu-id="e4519-106">You don't have toorestart hello container each time you make a code change.</span></span>
<span data-ttu-id="e4519-107">Este artigo ilustra como toostart de recurso de "Editar e atualizar" hello toouse um aplicativo Web do ASP.NET Core em um contêiner de Docker local, faça as alterações necessárias e, em seguida, atualizar Olá navegador toosee essas alterações.</span><span class="sxs-lookup"><span data-stu-id="e4519-107">This article illustrates how toouse hello "Edit and Refresh" feature toostart an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh hello browser toosee those changes.</span></span>
<span data-ttu-id="e4519-108">Este artigo também mostra como tooset pontos de interrupção de depuração.</span><span class="sxs-lookup"><span data-stu-id="e4519-108">This article also shows you how tooset breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="e4519-109">O suporte do Contêiner do Windows estará disponível em uma versão futura</span><span class="sxs-lookup"><span data-stu-id="e4519-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="e4519-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e4519-110">Prerequisites</span></span>
<span data-ttu-id="e4519-111">Olá ferramentas a seguir deve ser instalado.</span><span class="sxs-lookup"><span data-stu-id="e4519-111">hello following tools must be installed.</span></span>

* [<span data-ttu-id="e4519-112">Versão mais recente do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e4519-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="e4519-113">SDK do Microsoft ASP.NET Core 1.0</span><span class="sxs-lookup"><span data-stu-id="e4519-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="e4519-114">toorun localmente contêineres do Docker, será necessário um cliente do docker local.</span><span class="sxs-lookup"><span data-stu-id="e4519-114">toorun Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="e4519-115">Você pode usar o hello [caixa de ferramentas do Docker](https://www.docker.com/products/docker-toolbox), que requer o Hyper-V toobe desabilitado ou você pode usar [Docker para Windows](https://www.docker.com/get-docker), que usa o Hyper-V e requer o Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e4519-115">You can use hello [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V toobe disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="e4519-116">Se usar a caixa de ferramentas do Docker, será necessário muito[configurar o cliente do Docker Olá](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="e4519-116">If using Docker Toolbox, you'll need too[configure hello Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="e4519-117">1. Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="e4519-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="e4519-118">2. Adicionar suporte ao Docker</span><span class="sxs-lookup"><span data-stu-id="e4519-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="e4519-119">3. Editar seu código e atualizar</span><span class="sxs-lookup"><span data-stu-id="e4519-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="e4519-120">tooquickly iterar alterações, você pode iniciar o aplicativo em um contêiner e continuar toomake alterações, exibi-los como faria com o IIS Express.</span><span class="sxs-lookup"><span data-stu-id="e4519-120">tooquickly iterate changes, you can start your application within a container, and continue toomake changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="e4519-121">Definir Olá configuração da solução muito`Debug` e pressione  **&lt;CTRL + F5 >** toobuild o docker de imagens e executá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="e4519-121">Set hello Solution Configuration too`Debug` and press **&lt;CTRL + F5>** toobuild your docker image and run it locally.</span></span>

    <span data-ttu-id="e4519-122">Depois que a imagem de contêiner Olá foi criada e está em execução em um contêiner do Docker, o Visual Studio iniciará Olá Web app no navegador padrão.</span><span class="sxs-lookup"><span data-stu-id="e4519-122">Once hello container image has been built and is running in a Docker container, Visual Studio will launch hello Web app in your default browser.</span></span>
    <span data-ttu-id="e4519-123">Se você estiver usando o navegador Microsoft Edge de saudação ou detêm erros, consulte [solução de problemas](vs-azure-tools-docker-troubleshooting-docker-errors.md) seção.</span><span class="sxs-lookup"><span data-stu-id="e4519-123">If you are using hello Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="e4519-124">Vá toohello sobre a página, que é aqui que vamos toomake nossas alterações.</span><span class="sxs-lookup"><span data-stu-id="e4519-124">Go toohello About page, which is where we're going toomake our changes.</span></span>
3. <span data-ttu-id="e4519-125">Retornar tooVisual Studio e abra `Views\Home\About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="e4519-125">Return tooVisual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="e4519-126">Adicionar Olá seguindo HTML toohello conteúdo final do arquivo hello e salve as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4519-126">Add hello following HTML content toohello end of hello file and save hello changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="e4519-127">Exibir janela de saída de hello, quando Olá compilação .NET é concluída e você vê essas linhas, alterne tooyour back navegador e Olá sobre a página de atualização.</span><span class="sxs-lookup"><span data-stu-id="e4519-127">Viewing hello output window, when hello .NET build is completed and you see these lines, switch back tooyour browser and refresh hello About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. <span data-ttu-id="e4519-128">As alterações foram aplicadas.</span><span class="sxs-lookup"><span data-stu-id="e4519-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="e4519-129">4. Depurar com pontos de interrupção</span><span class="sxs-lookup"><span data-stu-id="e4519-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="e4519-130">Geralmente, as alterações serão necessário mais inspeção, aproveitando Olá depuração de recursos do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4519-130">Often, changes will need further inspection, leveraging hello debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="e4519-131">Retornar tooVisual Studio e abra`Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="e4519-131">Return tooVisual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="e4519-132">Substitua o conteúdo de saudação do método do hello About () com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="e4519-132">Replace hello contents of hello About() method with hello following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="e4519-133">Definir um ponto de interrupção toohello à esquerda da saudação `string message`... linha.</span><span class="sxs-lookup"><span data-stu-id="e4519-133">Set a breakpoint toohello left of hello `string message`... line.</span></span>
4. <span data-ttu-id="e4519-134">Acertos  **&lt;F5 >** toostart depuração.</span><span class="sxs-lookup"><span data-stu-id="e4519-134">Hit **&lt;F5>** toostart debugging.</span></span>
5. <span data-ttu-id="e4519-135">Navegue toohello sobre página toohit seu ponto de interrupção.</span><span class="sxs-lookup"><span data-stu-id="e4519-135">Navigate toohello About page toohit your breakpoint.</span></span>
6. <span data-ttu-id="e4519-136">Alternar ponto de interrupção da saudação tooview tooVisual Studio e inspecionar o valor de saudação da mensagem.</span><span class="sxs-lookup"><span data-stu-id="e4519-136">Switch tooVisual Studio tooview hello breakpoint, and inspect hello value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="e4519-137">Resumo</span><span class="sxs-lookup"><span data-stu-id="e4519-137">Summary</span></span>
<span data-ttu-id="e4519-138">Com [ferramentas do Visual Studio 2015 para Docker](https://aka.ms/DockerToolsForVS), você pode obter produtividade de saudação do trabalhando localmente, com realismo de produção de hello de desenvolvimento em um contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="e4519-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get hello productivity of working locally, with hello production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e4519-139">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="e4519-139">Troubleshooting</span></span>
[<span data-ttu-id="e4519-140">Troubleshooting Visual Studio Docker Development (Solucionar Problemas de Desenvolvimento do Docker do Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e4519-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="e4519-141">Mais informações sobre o Docker com o Visual Studio, Windows e Azure</span><span class="sxs-lookup"><span data-stu-id="e4519-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="e4519-142">[Ferramentas do Docker para Visual Studio](http://aka.ms/dockertoolsforvs) – Desenvolvendo seu código do .NET Core em um contêiner</span><span class="sxs-lookup"><span data-stu-id="e4519-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="e4519-143">[Ferramentas do Docker para o Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) – Criar e Implantar contêineres do docker</span><span class="sxs-lookup"><span data-stu-id="e4519-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="e4519-144">[Ferramentas do Docker para Visual Studio Code](http://aka.ms/dockertoolsforvscode) – Serviços de linguagem para editar arquivos do docker, com futuros cenários e2e</span><span class="sxs-lookup"><span data-stu-id="e4519-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="e4519-145">[Informações do Contêiner do Windows](http://aka.ms/containers)– Informações sobre Windows Server e Nano Server</span><span class="sxs-lookup"><span data-stu-id="e4519-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="e4519-146">[Serviço de Contêiner do Azure](https://azure.microsoft.com/services/container-service/) - [Conteúdo do Serviço de Contêiner do Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="e4519-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="e4519-147">Para obter mais exemplos de como trabalhar com o Docker, consulte [trabalhando com o Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) de saudação [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 conectar [demonstração](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="e4519-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="e4519-148">Para mais guias de início rápido de demonstração de HealthClinic.biz hello, consulte [início rápido do Azure Developer Tools](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="e4519-148">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="e4519-149">Várias ferramentas do Docker</span><span class="sxs-lookup"><span data-stu-id="e4519-149">Various Docker tools</span></span>
[<span data-ttu-id="e4519-150">Algumas ótimas ferramentas do Docker (blog de Steve Lasker)</span><span class="sxs-lookup"><span data-stu-id="e4519-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="e4519-151">Bons artigos</span><span class="sxs-lookup"><span data-stu-id="e4519-151">Good articles</span></span>
[<span data-ttu-id="e4519-152">Introdução tooMicroservices de NGINX</span><span class="sxs-lookup"><span data-stu-id="e4519-152">Introduction tooMicroservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="e4519-153">Apresentações</span><span class="sxs-lookup"><span data-stu-id="e4519-153">Presentations</span></span>
* [<span data-ttu-id="e4519-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e (Steve Lasker: VS ao vivo de Las Vegas 2016 - Docker e2e)</span><span class="sxs-lookup"><span data-stu-id="e4519-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="e4519-155">Introdução tooASP.NET núcleos @ 2016 - onde você na demonstração de compilação</span><span class="sxs-lookup"><span data-stu-id="e4519-155">Introduction tooASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="e4519-156">Developing .NET apps in containers, Channel 9 (Desenvolvendo aplicativos .NET em contêineres, Channel 9)</span><span class="sxs-lookup"><span data-stu-id="e4519-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
