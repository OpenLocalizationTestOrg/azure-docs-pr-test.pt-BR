---
title: Usar o .NET Core em aplicativo Web no Linux | Microsoft Docs
description: Usar o .NET Core em aplicativo Web no Linux.
keywords: "serviço de aplicativo do azure, aplicativo web, dotnet, core, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9226dfb90e52ac2cae2cfc4af7c0705a93f56b44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="50bb0-104">Usar o .NET Core em um aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="50bb0-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="50bb0-105">[Aplicativo Web](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) no Linux fornece um serviço de hospedagem na Web com aplicação de patch automática e altamente escalonável usando o sistema operacional Linux.</span><span class="sxs-lookup"><span data-stu-id="50bb0-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="50bb0-106">Este tutorial contém instruções passo a passo mostrando como criar um aplicativo [.NET Core](https://docs.microsoft.com/aspnet/core/) no aplicativo Web do Azure no Linux.</span><span class="sxs-lookup"><span data-stu-id="50bb0-106">This tutorial contains step-by-step instructions showing how to create a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Aplicativo Web no Linux][10]

<span data-ttu-id="50bb0-108">Você pode seguir as etapas abaixo usando um computador Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="50bb0-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50bb0-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="50bb0-109">Prerequisites</span></span> ##

<span data-ttu-id="50bb0-110">Para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="50bb0-110">To complete this tutorial:</span></span> 

* <span data-ttu-id="50bb0-111">Instale o [SDK do .NET Core](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="50bb0-111">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="50bb0-112">Instale o [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="50bb0-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="50bb0-113">Criar um aplicativo .NET Core local</span><span class="sxs-lookup"><span data-stu-id="50bb0-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="50bb0-114">Inicie uma nova sessão de terminal.</span><span class="sxs-lookup"><span data-stu-id="50bb0-114">Start a new terminal session.</span></span> <span data-ttu-id="50bb0-115">Crie um diretório chamado `hellodotnetcore` e altere o diretório atual para ele.</span><span class="sxs-lookup"><span data-stu-id="50bb0-115">Create a directory named `hellodotnetcore`, and change the current directory to it.</span></span> <span data-ttu-id="50bb0-116">Em seguida, digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="50bb0-116">Then type the following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="50bb0-117">Esse comando cria três arquivos (*hellodotnetcore.csproj*, *Program.cs* e *Startup.cs*) e uma pasta vazia (*wwwroot /*) no diretório atual.</span><span class="sxs-lookup"><span data-stu-id="50bb0-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under the current directory.</span></span> <span data-ttu-id="50bb0-118">O conteúdo do arquivo `.csproj` deverá ter a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="50bb0-118">The content of `.csproj` file should look like the following:</span></span> 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

<span data-ttu-id="50bb0-119">Como esse aplicativo é um aplicativo Web, uma referência a um pacote do ASP.NET Core foi adicionada automaticamente ao arquivo *hellodotnetcore.csproj*.</span><span class="sxs-lookup"><span data-stu-id="50bb0-119">Since this app is a web application, a reference to an ASP.NET Core package was automatically added to the *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="50bb0-120">O número da versão do pacote é definido de acordo com o framework escolhida.</span><span class="sxs-lookup"><span data-stu-id="50bb0-120">The version number of the package is set according to the chosen framework.</span></span> <span data-ttu-id="50bb0-121">Este exemplo faz referência à versão 1.1.2 do ASP.NET Core porque o .NET Core 1.1 é usado.</span><span class="sxs-lookup"><span data-stu-id="50bb0-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-the-application-locally"></a><span data-ttu-id="50bb0-122">Compilar e testar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="50bb0-122">Build and test the application locally</span></span> ##

<span data-ttu-id="50bb0-123">Você pode compilar e executar seu aplicativo .NET Core com o comando `dotnet restore` seguido do comando `dotnet run`, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="50bb0-123">You can build and run your .NET Core app with the `dotnet restore` command followed by the `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="50bb0-124">Quando o aplicativo é iniciado, ele exibe uma mensagem indicando que está escutando as solicitações de entrada em uma porta.</span><span class="sxs-lookup"><span data-stu-id="50bb0-124">When the application starts, it displays a message indicating the app is listening to incoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="50bb0-125">Teste-o navegando até `http://localhost:5000/` com seu navegador.</span><span class="sxs-lookup"><span data-stu-id="50bb0-125">Test it by browsing to `http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="50bb0-126">Se tudo estiver funcionando bem, você verá "Olá, Mundo!"</span><span class="sxs-lookup"><span data-stu-id="50bb0-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="50bb0-127">como texto de resultado.</span><span class="sxs-lookup"><span data-stu-id="50bb0-127">as the result text.</span></span>

![Testar com um navegador][7]

## <a name="create-a-net-core-app-in-the-azure-portal"></a><span data-ttu-id="50bb0-129">Criar um aplicativo .NET Core no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="50bb0-129">Create a .NET Core app in the Azure Portal</span></span> ##

<span data-ttu-id="50bb0-130">Primeiro você precisa criar um aplicativo Web vazio.</span><span class="sxs-lookup"><span data-stu-id="50bb0-130">First you need to create an empty web app.</span></span> <span data-ttu-id="50bb0-131">Faça logon no [Portal do Azure](https://portal.azure.com/) e crie um novo [aplicativo Web no Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="50bb0-131">Log in to the [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Criar um aplicativo Web][1]

<span data-ttu-id="50bb0-133">Quando a página **Criar** abrir, forneça detalhes sobre seu aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="50bb0-133">When the **Create** page opens, provide details about your web app:</span></span>

![Escolher uma pilha de tempo de execução do .NET Core][2]

<span data-ttu-id="50bb0-135">Use a tabela a seguir como guia para preencher a página **Criar** e, em seguida, selecione **OK** e **Criar** para criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="50bb0-135">Use the following table as a guide to fill out the **Create** page, then select **OK** and **Create** to create the app.</span></span>

| <span data-ttu-id="50bb0-136">Configuração</span><span class="sxs-lookup"><span data-stu-id="50bb0-136">Setting</span></span>      | <span data-ttu-id="50bb0-137">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="50bb0-137">Suggested value</span></span>  | <span data-ttu-id="50bb0-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="50bb0-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="50bb0-139">Nome do aplicativo</span><span class="sxs-lookup"><span data-stu-id="50bb0-139">App name</span></span> | <span data-ttu-id="50bb0-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="50bb0-140">hellodotnetcore</span></span>  | <span data-ttu-id="50bb0-141">O nome do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="50bb0-141">The name of your app.</span></span> <span data-ttu-id="50bb0-142">Esse nome deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="50bb0-142">This name must be unique.</span></span> |
| <span data-ttu-id="50bb0-143">Assinatura</span><span class="sxs-lookup"><span data-stu-id="50bb0-143">Subscription</span></span> | <span data-ttu-id="50bb0-144">Escolher uma assinatura existente</span><span class="sxs-lookup"><span data-stu-id="50bb0-144">Choose an existing subscription</span></span> | <span data-ttu-id="50bb0-145">A assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="50bb0-145">The Azure subscription.</span></span> |
| <span data-ttu-id="50bb0-146">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="50bb0-146">Resource Group</span></span> | <span data-ttu-id="50bb0-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="50bb0-147">myResourceGroup</span></span> |  <span data-ttu-id="50bb0-148">O nome do grupo de recursos do Azure para conter o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="50bb0-148">The Azure resource group to contain the web app.</span></span> |
| <span data-ttu-id="50bb0-149">Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="50bb0-149">App Service Plan</span></span> | <span data-ttu-id="50bb0-150">Nome do plano do Serviço de Aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="50bb0-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="50bb0-151">O plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="50bb0-151">The App Service plan.</span></span>  |
| <span data-ttu-id="50bb0-152">Configurar o contêiner</span><span class="sxs-lookup"><span data-stu-id="50bb0-152">Configure Container</span></span> | <span data-ttu-id="50bb0-153">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="50bb0-153">.NET Core 1.1</span></span> | <span data-ttu-id="50bb0-154">O tipo de contêiner desse aplicativo Web: registro interno, Docker ou privado.</span><span class="sxs-lookup"><span data-stu-id="50bb0-154">The type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="50bb0-155">Origem da imagem</span><span class="sxs-lookup"><span data-stu-id="50bb0-155">Image source</span></span>  | <span data-ttu-id="50bb0-156">Interno</span><span class="sxs-lookup"><span data-stu-id="50bb0-156">Built-in</span></span>  |  <span data-ttu-id="50bb0-157">A origem da imagem.</span><span class="sxs-lookup"><span data-stu-id="50bb0-157">The source of the image.</span></span> |
| <span data-ttu-id="50bb0-158">Pilha de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="50bb0-158">Runtime Stack</span></span>  | <span data-ttu-id="50bb0-159">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="50bb0-159">.NET Core 1.1</span></span>  | <span data-ttu-id="50bb0-160">A pilha de tempo de execução e a versão.</span><span class="sxs-lookup"><span data-stu-id="50bb0-160">The runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="50bb0-161">Implantar seu aplicativo por meio do Git</span><span class="sxs-lookup"><span data-stu-id="50bb0-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="50bb0-162">Use o Git para implantar o aplicativo .NET Core ao aplicativo Web do Serviço de Aplicativo do Azure no Linux.</span><span class="sxs-lookup"><span data-stu-id="50bb0-162">Use Git to deploy the .NET Core application to Azure App Service Web App on Linux.</span></span>

<span data-ttu-id="50bb0-163">O novo aplicativo Web do Azure já tem uma implantação do Git configurada.</span><span class="sxs-lookup"><span data-stu-id="50bb0-163">The new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="50bb0-164">Você encontrará a URL de implantação do Git navegando até a URL a seguir depois de inserir o nome do aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="50bb0-164">You will find the Git deployment URL by navigating to the following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="50bb0-165">A URL do Git tem o seguinte formato, com base no nome do seu aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="50bb0-165">The Git URL has the following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="50bb0-166">Execute os seguintes comandos para implantar o aplicativo local em seu aplicativo Web do Azure:</span><span class="sxs-lookup"><span data-stu-id="50bb0-166">Run the following commands to deploy the local application to your Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="50bb0-167">Você não precisa enviar nenhum arquivo por push no diretório *bin/* ou *obj/* porque seu aplicativo é criado na nuvem quando os arquivos de origem do aplicativo são enviados por push para o Azure.</span><span class="sxs-lookup"><span data-stu-id="50bb0-167">You don't need to push any files under *bin/* or *obj/* directories because your application is built in the cloud when the application's source files are pushed to Azure.</span></span> <span data-ttu-id="50bb0-168">Depois que o processo de compilação for concluído, os arquivos binários são copiados para o diretório do aplicativo no *inicial/site/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="50bb0-168">After the build process is complete, binary files are copied into the application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="50bb0-169">Confirme que as operações de implantação remota relatam êxito.</span><span class="sxs-lookup"><span data-stu-id="50bb0-169">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="50bb0-170">As operações de envio por push podem demorar, pois a resolução de pacotes e o processo de compilação são executados na nuvem.</span><span class="sxs-lookup"><span data-stu-id="50bb0-170">Push operations may take a while since package resolution and build process run in the cloud.</span></span> <span data-ttu-id="50bb0-171">Você verá várias mensagens de status, inclusive algumas informando que os arquivos foram copiados.</span><span class="sxs-lookup"><span data-stu-id="50bb0-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="50bb0-172">O resultado deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="50bb0-172">The output should look similar to the following:</span></span>

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
To https://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="50bb0-173">Depois que a implantação for concluída, reinicie o aplicativo Web para a implantação entrar em vigor.</span><span class="sxs-lookup"><span data-stu-id="50bb0-173">Once the deployment has completed, restart your web app for the deployment to take effect.</span></span> <span data-ttu-id="50bb0-174">Para isso, vá ao Portal do Azure e navegue até a página **Visão Geral** do seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="50bb0-174">To do this, go to the Azure portal and navigate to the **Overview** page of your web app.</span></span> <span data-ttu-id="50bb0-175">Selecione o botão **Reiniciar** na página.</span><span class="sxs-lookup"><span data-stu-id="50bb0-175">Select the **Restart** button in the page.</span></span> <span data-ttu-id="50bb0-176">Quando uma janela pop-up aparecer, selecione **Sim** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="50bb0-176">When a popup window shows up, select **Yes** to confirm.</span></span> <span data-ttu-id="50bb0-177">Em seguida, você pode procurar o aplicativo Web, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="50bb0-177">You can then browse your web app, as shown here:</span></span>

![Procurar aplicativo .NET Core implantado para o Serviço de Aplicativo do Azure no Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="50bb0-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="50bb0-179">Next steps</span></span>
* [<span data-ttu-id="50bb0-180">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="50bb0-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
