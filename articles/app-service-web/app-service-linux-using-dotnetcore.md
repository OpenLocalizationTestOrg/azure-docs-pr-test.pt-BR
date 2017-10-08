---
title: aaaUse .NET Core no aplicativo Web no Linux | Microsoft Docs
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
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="2c2e8-104">Usar o .NET Core em um aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="2c2e8-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="2c2e8-105">[Aplicativo da Web](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) no Linux fornece um serviço de hospedagem na web altamente escalonável, aplicação de patch automática usando o sistema de operacional Linux Olá.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using hello Linux operating system.</span></span> <span data-ttu-id="2c2e8-106">Este tutorial contém instruções passo a passo mostra como toocreate uma [.NET Core](https://docs.microsoft.com/aspnet/core/) aplicativo no aplicativo web do Azure no Linux.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-106">This tutorial contains step-by-step instructions showing how toocreate a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Aplicativo Web no Linux][10]

<span data-ttu-id="2c2e8-108">Você pode seguir estas etapas hello usando um computador Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c2e8-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2c2e8-109">Prerequisites</span></span> ##

<span data-ttu-id="2c2e8-110">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-110">toocomplete this tutorial:</span></span> 

* <span data-ttu-id="2c2e8-111">Instalar Olá [.NET Core SDK](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="2c2e8-111">Install hello [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="2c2e8-112">Instale o [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="2c2e8-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="2c2e8-113">Criar um aplicativo .NET Core local</span><span class="sxs-lookup"><span data-stu-id="2c2e8-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="2c2e8-114">Inicie uma nova sessão de terminal.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-114">Start a new terminal session.</span></span> <span data-ttu-id="2c2e8-115">Crie um diretório chamado `hellodotnetcore`e alterar Olá tooit de diretório atual.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-115">Create a directory named `hellodotnetcore`, and change hello current directory tooit.</span></span> <span data-ttu-id="2c2e8-116">Em seguida, digite o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-116">Then type hello following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="2c2e8-117">Este comando cria três arquivos (*hellodotnetcore.csproj*, *Program.cs*, e *Startup.cs*) e uma pasta vazia (*wwwroot /*) no diretório atual da saudação.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under hello current directory.</span></span> <span data-ttu-id="2c2e8-118">Olá conteúdo de `.csproj` arquivo deve ser semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-118">hello content of `.csproj` file should look like hello following:</span></span> 

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

<span data-ttu-id="2c2e8-119">Como esse aplicativo é um aplicativo web, um tooan de referência do pacote ASP.NET Core foi automaticamente adicionada toohello *hellodotnetcore.csproj* arquivo.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-119">Since this app is a web application, a reference tooan ASP.NET Core package was automatically added toohello *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="2c2e8-120">número de versão de saudação do pacote de saudação é definido toohello escolhido do framework de acordo com.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-120">hello version number of hello package is set according toohello chosen framework.</span></span> <span data-ttu-id="2c2e8-121">Este exemplo faz referência à versão 1.1.2 do ASP.NET Core porque o .NET Core 1.1 é usado.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-hello-application-locally"></a><span data-ttu-id="2c2e8-122">Compilar e testar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="2c2e8-122">Build and test hello application locally</span></span> ##

<span data-ttu-id="2c2e8-123">Você pode compilar e executar seu aplicativo .NET Core com hello `dotnet restore` comando seguido Olá `dotnet run` de comando, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-123">You can build and run your .NET Core app with hello `dotnet restore` command followed by hello `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="2c2e8-124">Quando o aplicativo hello é iniciado, ele exibe uma mensagem indicando que o aplicativo hello está escutando as solicitações de tooincoming em uma porta.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-124">When hello application starts, it displays a message indicating hello app is listening tooincoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

<span data-ttu-id="2c2e8-125">Testá-lo navegando muito`http://localhost:5000/` com seu navegador.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-125">Test it by browsing too`http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="2c2e8-126">Se tudo estiver funcionando bem, você verá "Olá, Mundo!"</span><span class="sxs-lookup"><span data-stu-id="2c2e8-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="2c2e8-127">como o texto de saudação do resultado.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-127">as hello result text.</span></span>

![Testar com um navegador][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a><span data-ttu-id="2c2e8-129">Criar um aplicativo .NET Core em Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2c2e8-129">Create a .NET Core app in hello Azure Portal</span></span> ##

<span data-ttu-id="2c2e8-130">Primeiro, é necessário toocreate um aplicativo web vazio.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-130">First you need toocreate an empty web app.</span></span> <span data-ttu-id="2c2e8-131">Faça logon no toohello [portal do Azure](https://portal.azure.com/) e criar um novo [Web App no Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="2c2e8-131">Log in toohello [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Criar um aplicativo Web][1]

<span data-ttu-id="2c2e8-133">Olá quando **criar** página será aberta, forneça detalhes sobre seu aplicativo web:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-133">When hello **Create** page opens, provide details about your web app:</span></span>

![Escolher uma pilha de tempo de execução do .NET Core][2]

<span data-ttu-id="2c2e8-135">Tabela a seguir de saudação uso como um toofill guia saída Olá **criar** página e, em seguida, selecione **Okey** e **criar** toocreate Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-135">Use hello following table as a guide toofill out hello **Create** page, then select **OK** and **Create** toocreate hello app.</span></span>

| <span data-ttu-id="2c2e8-136">Configuração</span><span class="sxs-lookup"><span data-stu-id="2c2e8-136">Setting</span></span>      | <span data-ttu-id="2c2e8-137">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="2c2e8-137">Suggested value</span></span>  | <span data-ttu-id="2c2e8-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="2c2e8-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="2c2e8-139">Nome do aplicativo</span><span class="sxs-lookup"><span data-stu-id="2c2e8-139">App name</span></span> | <span data-ttu-id="2c2e8-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="2c2e8-140">hellodotnetcore</span></span>  | <span data-ttu-id="2c2e8-141">nome de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-141">hello name of your app.</span></span> <span data-ttu-id="2c2e8-142">Esse nome deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-142">This name must be unique.</span></span> |
| <span data-ttu-id="2c2e8-143">Assinatura</span><span class="sxs-lookup"><span data-stu-id="2c2e8-143">Subscription</span></span> | <span data-ttu-id="2c2e8-144">Escolher uma assinatura existente</span><span class="sxs-lookup"><span data-stu-id="2c2e8-144">Choose an existing subscription</span></span> | <span data-ttu-id="2c2e8-145">Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-145">hello Azure subscription.</span></span> |
| <span data-ttu-id="2c2e8-146">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2c2e8-146">Resource Group</span></span> | <span data-ttu-id="2c2e8-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2c2e8-147">myResourceGroup</span></span> |  <span data-ttu-id="2c2e8-148">aplicativo Hello recursos do Azure grupo toocontain Olá web.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-148">hello Azure resource group toocontain hello web app.</span></span> |
| <span data-ttu-id="2c2e8-149">Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="2c2e8-149">App Service Plan</span></span> | <span data-ttu-id="2c2e8-150">Nome do plano do Serviço de Aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="2c2e8-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="2c2e8-151">saudação do plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-151">hello App Service plan.</span></span>  |
| <span data-ttu-id="2c2e8-152">Configurar o contêiner</span><span class="sxs-lookup"><span data-stu-id="2c2e8-152">Configure Container</span></span> | <span data-ttu-id="2c2e8-153">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="2c2e8-153">.NET Core 1.1</span></span> | <span data-ttu-id="2c2e8-154">Olá tipo de contêiner para este aplicativo web: registro internas, Docker ou privada.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-154">hello type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="2c2e8-155">Origem da imagem</span><span class="sxs-lookup"><span data-stu-id="2c2e8-155">Image source</span></span>  | <span data-ttu-id="2c2e8-156">Interno</span><span class="sxs-lookup"><span data-stu-id="2c2e8-156">Built-in</span></span>  |  <span data-ttu-id="2c2e8-157">origem de saudação da imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-157">hello source of hello image.</span></span> |
| <span data-ttu-id="2c2e8-158">Pilha de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="2c2e8-158">Runtime Stack</span></span>  | <span data-ttu-id="2c2e8-159">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="2c2e8-159">.NET Core 1.1</span></span>  | <span data-ttu-id="2c2e8-160">pilha de tempo de execução Hello e versão.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-160">hello runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="2c2e8-161">Implantar seu aplicativo por meio do Git</span><span class="sxs-lookup"><span data-stu-id="2c2e8-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="2c2e8-162">Use Git toodeploy Olá .NET Core aplicativo tooAzure aplicativo Web do serviço de aplicativo no Linux.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-162">Use Git toodeploy hello .NET Core application tooAzure App Service Web App on Linux.</span></span>

<span data-ttu-id="2c2e8-163">novo aplicativo web do Azure e Olá já tem Git implantação configurada.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-163">hello new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="2c2e8-164">Você encontrará uma URL de implantação do Git Olá navegando toohello URL a seguir depois de inserir o nome do aplicativo web:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-164">You will find hello Git deployment URL by navigating toohello following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="2c2e8-165">Olá URL de Git tem Olá formulário com base no nome do aplicativo da web a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-165">hello Git URL has hello following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="2c2e8-166">Execute Olá aplicativo web do Azure tooyour de aplicativo local do comandos toodeploy Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-166">Run hello following commands toodeploy hello local application tooyour Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="2c2e8-167">Não é necessário toopush todos os arquivos no *bin /* ou *obj /* diretórios porque seu aplicativo é criado na nuvem Olá Olá do aplicativo quando os arquivos de origem são enviados por push tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-167">You don't need toopush any files under *bin/* or *obj/* directories because your application is built in hello cloud when hello application's source files are pushed tooAzure.</span></span> <span data-ttu-id="2c2e8-168">Após a conclusão do processo de compilação hello, arquivos binários são copiados para o diretório do aplicativo hello em *inicial/site/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-168">After hello build process is complete, binary files are copied into hello application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="2c2e8-169">Confirme que o relatório de operações de implantação remota Olá sucesso.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-169">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="2c2e8-170">Operações de envio podem levar um tempo desde a resolução de pacote e executado na nuvem de saudação do processo de compilação.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-170">Push operations may take a while since package resolution and build process run in hello cloud.</span></span> <span data-ttu-id="2c2e8-171">Você verá várias mensagens de status, inclusive algumas informando que os arquivos foram copiados.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="2c2e8-172">saída de Hello deve ser a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-172">hello output should look similar toohello following:</span></span>

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
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="2c2e8-173">Após a conclusão da implantação Olá, reinicie seu aplicativo web para efeito de tootake implantação hello.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-173">Once hello deployment has completed, restart your web app for hello deployment tootake effect.</span></span> <span data-ttu-id="2c2e8-174">toodo isso, vá toohello portal do Azure e navegue toohello **visão geral** página do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-174">toodo this, go toohello Azure portal and navigate toohello **Overview** page of your web app.</span></span> <span data-ttu-id="2c2e8-175">Selecione Olá **reiniciar** botão na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-175">Select hello **Restart** button in hello page.</span></span> <span data-ttu-id="2c2e8-176">Quando uma janela pop-up aparece, selecione **Sim** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="2c2e8-176">When a popup window shows up, select **Yes** tooconfirm.</span></span> <span data-ttu-id="2c2e8-177">Em seguida, você pode procurar o aplicativo Web, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="2c2e8-177">You can then browse your web app, as shown here:</span></span>

![Pesquisa no .NET Core aplicativo implantado tooAzure do serviço de aplicativo no Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="2c2e8-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2c2e8-179">Next steps</span></span>
* [<span data-ttu-id="2c2e8-180">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="2c2e8-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
