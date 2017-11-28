---
title: erros de cliente de Docker aaaTroubleshooting no Windows usando o Visual Studio | Microsoft Docs
description: Solucionar problemas encontrados ao usar o Visual Studio toocreate e implantar tooDocker de aplicativos web no Windows usando o Visual Studio.
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 7421ae8e044d58fc412d748fb870da4c9b2fdb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="5ee4a-103">Solucionar problemas de desenvolvimento do Docker no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5ee4a-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="5ee4a-104">Quando você estiver trabalhando com o Visual Studio Tools para Docker Preview, você pode encontrar alguns problemas devido à natureza de saudação da visualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of hello nature of hello preview.</span></span>
<span data-ttu-id="5ee4a-105">Veja a seguir alguns problemas comuns e suas resoluções.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="5ee4a-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="5ee4a-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="5ee4a-107">**Contêineres do Linux**</span><span class="sxs-lookup"><span data-stu-id="5ee4a-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="5ee4a-108">Os erros de compilação ocorrem durante a depuração de um aplicativo Web ou de um console do .NET Core</span><span class="sxs-lookup"><span data-stu-id="5ee4a-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="5ee4a-109">Isso pode ser relacionado toonot unidade Olá onde reside o projeto de saudação de compartilhamento com o Docker para Windows.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-109">This could be related toonot sharing hello drive where hello project resides with Docker for Windows.</span></span>  <span data-ttu-id="5ee4a-110">Você pode receber um erro como Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="5ee4a-110">You may receive an error like hello following:</span></span>

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="5ee4a-111">tooresolve esse problema:</span><span class="sxs-lookup"><span data-stu-id="5ee4a-111">tooresolve this issue:</span></span>

1. <span data-ttu-id="5ee4a-112">Clique com botão direito **Docker para Windows** Olá área de notificação e, em seguida, selecione **configurações**.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-112">Right-click **Docker for Windows** in hello notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="5ee4a-113">Selecione **unidades compartilhadas** e compartilhar Olá unidade onde o projeto Olá reside.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-113">Select **Shared Drives** and share hello drive where hello project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="5ee4a-114">**Contêineres do Windows**</span><span class="sxs-lookup"><span data-stu-id="5ee4a-114">**Windows containers**</span></span>

<span data-ttu-id="5ee4a-115">Olá problemas a seguir são toodebugging específico do .NET Framework web e console de aplicativos em contêineres do Windows.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-115">hello following issues are specific toodebugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="5ee4a-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5ee4a-116">Prerequisites</span></span>

1. <span data-ttu-id="5ee4a-117">Visual Studio 2017 RC (ou posterior) com hello .NET Core e carga de trabalho de visualização de Docker deve ser instalada.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-117">Visual Studio 2017 RC (or later) with hello .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="5ee4a-118">Atualização de Aniversário do Windows 10 com os últimos patches do Windows Update.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="5ee4a-119">Especificamente, o [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) deve ser instalado.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="5ee4a-120">O [Docker para Windows](https://docs.docker.com/docker-for-windows/) (compilação 1.13.0 ou posterior) deve ser instalado.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="5ee4a-121">**Alternar contêineres tooWindows** deve ser selecionado.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-121">**Switch tooWindows containers** must be selected.</span></span> <span data-ttu-id="5ee4a-122">Na área de notificação de saudação, clique em **Docker para Windows**e, em seguida, selecione **alternar contêineres tooWindows**.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-122">In hello notification area, click **Docker for Windows**, and then select **Switch tooWindows containers**.</span></span> <span data-ttu-id="5ee4a-123">Depois de reinicia a máquina hello, certifique-se de que essa configuração é mantida.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-123">After hello machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="5ee4a-124">A saída do console não é exibida na janela de saída do Visual Studio durante a depuração de um aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="5ee4a-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="5ee4a-125">Este é um problema conhecido com o depurador do Visual Studio hello (msvsmon.exe), que atualmente não é projetado para este cenário.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-125">This is a known issue with hello Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="5ee4a-126">Suporte para esse cenário pode ser incluído em uma versão futura.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="5ee4a-127">saída de toosee do aplicativo de console hello no Visual Studio, use **Docker: Iniciar projeto**, que é equivalente a muito**iniciar sem depuração**.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-127">toosee output from hello console application in Visual Studio, use **Docker: Start Project**, which is equivalent too**Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="5ee4a-128">Depurando aplicativos web com hello versão de configuração falha com erro de proibido (403)</span><span class="sxs-lookup"><span data-stu-id="5ee4a-128">Debugging web applications with hello release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="5ee4a-129">toowork esse problema, abra web.release.config na solução hello e comentar ou excluir Olá linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="5ee4a-129">toowork around this issue, open web.release.config in hello solution and comment out or delete hello following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="5ee4a-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="5ee4a-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="5ee4a-131">**Contêineres do Linux**</span><span class="sxs-lookup"><span data-stu-id="5ee4a-131">**Linux containers**</span></span>

#### <a name="unable-toovalidate-volume-mapping"></a><span data-ttu-id="5ee4a-132">Mapeamento do volume não é possível toovalidate</span><span class="sxs-lookup"><span data-stu-id="5ee4a-132">Unable toovalidate volume mapping</span></span>
<span data-ttu-id="5ee4a-133">Mapeamento do volume é o código-fonte necessário tooshare hello e binários do seu aplicativo com a pasta de aplicativo hello no contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-133">Volume mapping is required tooshare hello source code and binaries of your application with hello app folder in hello container.</span></span>  <span data-ttu-id="5ee4a-134">Os mapeamentos de volume específico estão contidos em docker-compose.dev.debug.yml e docker-compose.dev.release.yml.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="5ee4a-135">Como os arquivos são alterados na sua máquina host, contêineres de saudação refletem essas alterações em uma estrutura de pasta semelhante.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-135">As files are changed on your host machine, hello containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="5ee4a-136">mapeamento do volume tooenable:</span><span class="sxs-lookup"><span data-stu-id="5ee4a-136">tooenable volume mapping:</span></span>

1. <span data-ttu-id="5ee4a-137">Clique em **Moby** na área de notificação hello e selecione **configurações**.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-137">Click **Moby** in hello notification area and select **Settings**.</span></span>
2. <span data-ttu-id="5ee4a-138">Selecione **Unidades Compartilhadas**.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="5ee4a-139">Selecione a unidade de saudação que hospeda sua unidade de projeto e hello onde % USERPROFILE % reside.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-139">Select hello drive that hosts your project and hello drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="5ee4a-140">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-140">Click **Apply**.</span></span>

<span data-ttu-id="5ee4a-141">tootest se o mapeamento do volume estiver funcionando, recriar e selecione F5 de dentro do Visual Studio depois de uma ou mais unidades foram compartilhadas ou executadas Olá código a seguir em um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-141">tootest if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run hello following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="5ee4a-142">Este exemplo pressupõe que a pasta Usuários esteja localizada na unidade C e que ela foi compartilhada.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="5ee4a-143">Examine, conforme necessário, se você compartilhou outra unidade.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="5ee4a-144">Execute Olá código no contêiner do hello Linux a seguir.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-144">Run hello following code in hello Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="5ee4a-145">Você deve ver uma lista de saudação usuários/pasta pública de pastas.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-145">You should see a directory listing from hello Users/Public folder.</span></span> <span data-ttu-id="5ee4a-146">Se nenhum arquivo for exibido e sua pasta /c/Usuários/Público não estiver vazia, o mapeamento de volume não estará configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="5ee4a-147">Alterar toohello fenda espacial diretório toosee Olá conteúdo de saudação `/c/Users/Public` diretório:</span><span class="sxs-lookup"><span data-stu-id="5ee4a-147">Change toohello wormhole directory toosee hello contents of hello `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="5ee4a-148">Quando você está trabalhando com VMs do Linux, o sistema de arquivos de contêiner Olá diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-148">When you're working with Linux VMs, hello container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="5ee4a-149">Compilação: a tarefa "PrepareForBuild" falhou inesperadamente</span><span class="sxs-lookup"><span data-stu-id="5ee4a-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="5ee4a-150">Microsoft.DotNet.Docker.CommandLine.ClientException: Erro ao tentar tooconnect.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying tooconnect.</span></span>

<span data-ttu-id="5ee4a-151">Verifique se o que host Docker saudação padrão está em execução.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-151">Verify that hello default Docker host is running.</span></span> <span data-ttu-id="5ee4a-152">Abra um prompt de comando e execute:</span><span class="sxs-lookup"><span data-stu-id="5ee4a-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="5ee4a-153">Se isso retornar um erro, em seguida, tente Olá toostart **Docker para Windows** aplicativo de área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-153">If this returns an error, then attempt toostart hello **Docker for Windows** desktop app.</span></span> <span data-ttu-id="5ee4a-154">Se o aplicativo de área de trabalho Olá estiver em execução, em seguida, **Moby** devem ser visíveis na área de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-154">If hello desktop app is running, then **Moby** should be visible in hello notification area.</span></span> <span data-ttu-id="5ee4a-155">Clique com botão direito em **Moby** e abra **configurações**.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="5ee4a-156">Clique em **Redefinir** e reinicie o Docker.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="5ee4a-157">Uma caixa de diálogo de erro ocorre ao tentar tooadd Docker suporte ou depurar um aplicativo ASP.NET Core em um contêiner de (F5)</span><span class="sxs-lookup"><span data-stu-id="5ee4a-157">An error dialog occurs when attempting tooadd Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="5ee4a-158">Depois de desinstalar e instalar extensões, Olá cache Managed Extensibility Framework (MEF) no Visual Studio pode ficar corrompida.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-158">After uninstalling and installing extensions, hello Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="5ee4a-159">Quando isso ocorrer, ele pode causar várias mensagens de erro quando você estiver adicionando suporte de Docker e/ou tentar toorun ou depuração (F5) o aplicativo ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting toorun or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="5ee4a-160">Como solução temporária, use Olá seguindo as etapas toodelete e regenerar Olá MEF o cache.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-160">As a temporary workaround, use hello following steps toodelete and regenerate hello MEF cache.</span></span>

1. <span data-ttu-id="5ee4a-161">Feche todas as instâncias do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="5ee4a-162">Abra %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="5ee4a-163">Exclua Olá pastas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee4a-163">Delete hello following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="5ee4a-164">Abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="5ee4a-165">Repita o cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ee4a-165">Attempt hello scenario again.</span></span>
