---
title: "aaaCreate Azure funções web e de trabalho para PHP | Microsoft Docs"
description: "Uma guia toocreating PHP funções web e de trabalho em um serviço de nuvem do Azure e configurar Olá PHP em tempo de execução."
services: 
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 04a6e8c9c379cb0f854645941b6bc7d614bb91f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-php-web-and-worker-roles"></a><span data-ttu-id="1ad54-103">Como as funções de web e de trabalho PHP toocreate</span><span class="sxs-lookup"><span data-stu-id="1ad54-103">How toocreate PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="1ad54-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1ad54-104">Overview</span></span>
<span data-ttu-id="1ad54-105">Este guia mostrará como toocreate PHP web ou trabalho funções em um ambiente de desenvolvimento do Windows, escolher uma versão específica do PHP hello "internas" versões disponíveis, alterar a configuração de PHP hello, habilitar extensões e por fim, implantar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1ad54-105">This guide will show you how toocreate PHP web or worker roles in a Windows development environment, choose a specific version of PHP from hello "built-in" versions available, change hello PHP configuration, enable extensions, and finally, deploy tooAzure.</span></span> <span data-ttu-id="1ad54-106">Ele também descreve como tooconfigure toouse uma função web ou de trabalho um tempo de execução do PHP (com configuração personalizada e extensões) que você fornecer.</span><span class="sxs-lookup"><span data-stu-id="1ad54-106">It also describes how tooconfigure a web or worker role toouse a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="1ad54-107">O que são funções Web e de Trabalho do PHP?</span><span class="sxs-lookup"><span data-stu-id="1ad54-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="1ad54-108">O Azure fornece três modelos de computação para a execução de aplicativos: Serviço de Aplicativo do Azure, Máquinas Virtuais do Azure e Serviços de Nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad54-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="1ad54-109">Todos os três modelos oferecem suporte ao PHP.</span><span class="sxs-lookup"><span data-stu-id="1ad54-109">All three models support PHP.</span></span> <span data-ttu-id="1ad54-110">Os Serviços de Nuvem, que incluem as funções Web e de trabalho, fornecem a *PaaS (plataforma como serviço)*.</span><span class="sxs-lookup"><span data-stu-id="1ad54-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="1ad54-111">Em um serviço de nuvem, uma função web fornece uma web dedicado do Internet Information Services (IIS) aplicativos web front-end do servidor toohost.</span><span class="sxs-lookup"><span data-stu-id="1ad54-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front-end web applications.</span></span> <span data-ttu-id="1ad54-112">Uma função de trabalho pode executar tarefas assíncronas, de execução longa ou perpétuas, independentemente da interação do usuário ou da entrada.</span><span class="sxs-lookup"><span data-stu-id="1ad54-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="1ad54-113">Para obter mais informações sobre essas opções, consulte [Opções de hospedagem de computação fornecidas pelo Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="1ad54-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="1ad54-114">Baixar hello Azure SDK para PHP</span><span class="sxs-lookup"><span data-stu-id="1ad54-114">Download hello Azure SDK for PHP</span></span>
<span data-ttu-id="1ad54-115">Olá [Azure SDK para PHP] consiste em vários componentes.</span><span class="sxs-lookup"><span data-stu-id="1ad54-115">hello [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="1ad54-116">Este artigo usará duas delas: PowerShell do Azure e Olá emuladores do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad54-116">This article will use two of them: Azure PowerShell and hello Azure emulators.</span></span> <span data-ttu-id="1ad54-117">Esses dois componentes podem ser instalados via Olá Microsoft Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="1ad54-117">These two components can be installed via hello Microsoft Web Platform Installer.</span></span> <span data-ttu-id="1ad54-118">Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1ad54-118">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="1ad54-119">Criar um projeto de Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="1ad54-119">Create a Cloud Services project</span></span>
<span data-ttu-id="1ad54-120">Olá primeira etapa na criação de uma função web ou de trabalho do PHP é toocreate um projeto de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad54-120">hello first step in creating a PHP web or worker role is toocreate an Azure Service project.</span></span> <span data-ttu-id="1ad54-121">um projeto de serviço do Azure funciona como um contêiner lógico para funções da web e de trabalho, e ele contém do projeto Olá [(. csdef) de definição de serviço] e [a configuração de serviço (. cscfg)] arquivos.</span><span class="sxs-lookup"><span data-stu-id="1ad54-121">an Azure Service project serves as a logical container for web and worker roles, and it contains hello project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="1ad54-122">toocreate um novo projeto de serviço do Azure, execute o Azure PowerShell como administrador e execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad54-122">toocreate a new Azure Service project, run Azure PowerShell as an administrator, and execute hello following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="1ad54-123">Este comando cria um novo diretório (`myProject`) toowhich, você pode adicionar funções web e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1ad54-123">This command will create a new directory (`myProject`) toowhich you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="1ad54-124">Adicionar funções de trabalho ou Web PHP</span><span class="sxs-lookup"><span data-stu-id="1ad54-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="1ad54-125">tooadd um projeto de tooa de função de web PHP, executar Olá comando dentro do diretório raiz do projeto Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad54-125">tooadd a PHP web role tooa project, run hello following command from within hello project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="1ad54-126">Para uma função de trabalho, use este comando:</span><span class="sxs-lookup"><span data-stu-id="1ad54-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="1ad54-127">Olá `roleName` parâmetro é opcional.</span><span class="sxs-lookup"><span data-stu-id="1ad54-127">hello `roleName` parameter is optional.</span></span> <span data-ttu-id="1ad54-128">Se ele for omitido, o nome de função hello será gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1ad54-128">If it is omitted, hello role name will be automatically generated.</span></span> <span data-ttu-id="1ad54-129">função da web primeiro Olá criada será `WebRole1`, Olá segundo será `WebRole2`, e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="1ad54-129">hello first web role created will be `WebRole1`, hello second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="1ad54-130">Olá primeira função de trabalho criada será `WorkerRole1`, Olá segundo será `WorkerRole2`, e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="1ad54-130">hello first worker role created will be `WorkerRole1`, hello second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-hello-built-in-php-version"></a><span data-ttu-id="1ad54-131">Especificar versão do PHP interno Olá</span><span class="sxs-lookup"><span data-stu-id="1ad54-131">Specify hello built-in PHP version</span></span>
<span data-ttu-id="1ad54-132">Quando você adicionar um projeto PHP web ou de trabalho função tooa, arquivos de configuração do projeto Olá são modificados para que o PHP será instalado em cada instância de web ou de trabalho do seu aplicativo quando ele é implantado.</span><span class="sxs-lookup"><span data-stu-id="1ad54-132">When you add a PHP web or worker role tooa project, hello project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="1ad54-133">versão de hello toosee do PHP que será instalado por padrão, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad54-133">toosee hello version of PHP that will be installed by default, run hello following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="1ad54-134">Olá a saída do comando de saudação acima será semelhante toowhat é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="1ad54-134">hello output from hello command above will look similar toowhat is shown below.</span></span> <span data-ttu-id="1ad54-135">Neste exemplo, Olá `IsDefault` sinalizador é definido muito`true` para PHP 5.3.17, indicando que ele seja versão do PHP padrão Olá instalado.</span><span class="sxs-lookup"><span data-stu-id="1ad54-135">In this example, hello `IsDefault` flag is set too`true` for PHP 5.3.17, indicating that it will be hello default PHP version installed.</span></span>

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

<span data-ttu-id="1ad54-136">Você pode definir Olá PHP runtime versão tooany de versões do PHP Olá listados.</span><span class="sxs-lookup"><span data-stu-id="1ad54-136">You can set hello PHP runtime version tooany of hello PHP versions that are listed.</span></span> <span data-ttu-id="1ad54-137">Por exemplo, tooset Olá PHP versão (para uma função com o nome da saudação `roleName`) too5.4.0, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad54-137">For example, tooset hello PHP version (for a role with hello name `roleName`) too5.4.0, use hello following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="1ad54-138">Versões do PHP disponíveis podem ser alterados no hello futuras.</span><span class="sxs-lookup"><span data-stu-id="1ad54-138">Available PHP versions may change in hello future.</span></span>
>
>

## <a name="customize-hello-built-in-php-runtime"></a><span data-ttu-id="1ad54-139">Personalizar o tempo de execução do PHP interno Olá</span><span class="sxs-lookup"><span data-stu-id="1ad54-139">Customize hello built-in PHP runtime</span></span>
<span data-ttu-id="1ad54-140">Você tem controle total sobre a configuração do tempo de execução do PHP Olá que é instalada quando você seguir as etapas de saudação acima, incluindo a modificação de saudação `php.ini` configurações e a habilitação de extensões.</span><span class="sxs-lookup"><span data-stu-id="1ad54-140">You have complete control over hello configuration of hello PHP runtime that is installed when you follow hello steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="1ad54-141">toocustomize Olá interno em tempo de execução do PHP, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="1ad54-141">toocustomize hello built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="1ad54-142">Adicionar uma nova pasta chamada `php`, toohello `bin` diretório de sua função web.</span><span class="sxs-lookup"><span data-stu-id="1ad54-142">Add a new folder, named `php`, toohello `bin` directory of your web role.</span></span> <span data-ttu-id="1ad54-143">Para uma função de trabalho, adicione-o diretório raiz de toohello da função.</span><span class="sxs-lookup"><span data-stu-id="1ad54-143">For a worker role, add it toohello role's root directory.</span></span>
2. <span data-ttu-id="1ad54-144">Em Olá `php` pasta, crie outra pasta chamada `ext`.</span><span class="sxs-lookup"><span data-stu-id="1ad54-144">In hello `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="1ad54-145">Colocar qualquer `.dll` arquivos de extensão (por exemplo, `php_mongo.dll`) que você deseja tooenable nessa pasta.</span><span class="sxs-lookup"><span data-stu-id="1ad54-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want tooenable in this folder.</span></span>
3. <span data-ttu-id="1ad54-146">Adicionar um `php.ini` arquivo toohello `php` pasta.</span><span class="sxs-lookup"><span data-stu-id="1ad54-146">Add a `php.ini` file toohello `php` folder.</span></span> <span data-ttu-id="1ad54-147">Habilite todas as extensões personalizadas e defina todas as diretivas do PHP nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="1ad54-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="1ad54-148">Por exemplo, se você quisesse tooturn `display_errors` em e habilitar Olá `php_mongo.dll` extensão, o conteúdo de saudação do seu `php.ini` arquivo seria o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1ad54-148">For example, if you wanted tooturn `display_errors` on and enable hello `php_mongo.dll` extension, hello contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="1ad54-149">Todas as configurações que você não definir explicitamente Olá `php.ini` arquivo que você fornecer serão automaticamente ser definido como tootheir os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="1ad54-149">Any settings that you don't explicitly set in hello `php.ini` file that you provide will automatically be set tootheir default values.</span></span> <span data-ttu-id="1ad54-150">No entanto, lembre-se de que você pode adicionar um arquivo `php.ini` completo.</span><span class="sxs-lookup"><span data-stu-id="1ad54-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="1ad54-151">Usar seu próprio tempo de execução PHP</span><span class="sxs-lookup"><span data-stu-id="1ad54-151">Use your own PHP runtime</span></span>
<span data-ttu-id="1ad54-152">Em alguns casos, em vez de selecionar um tempo de execução do PHP interno e configurá-lo, conforme descrito acima, convém tooprovide seu próprio tempo de execução do PHP.</span><span class="sxs-lookup"><span data-stu-id="1ad54-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want tooprovide your own PHP runtime.</span></span> <span data-ttu-id="1ad54-153">Por exemplo, você pode usar Olá mesmo tempo de execução do PHP em uma função web ou de trabalho que você usa em seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="1ad54-153">For example, you can use hello same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="1ad54-154">Isso torna mais fácil tooensure aplicativo hello não alterará o comportamento em seu ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1ad54-154">This makes it easier tooensure that hello application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a><span data-ttu-id="1ad54-155">Configurar um toouse de função da web em seu próprio tempo de execução do PHP</span><span class="sxs-lookup"><span data-stu-id="1ad54-155">Configure a web role toouse your own PHP runtime</span></span>
<span data-ttu-id="1ad54-156">tooconfigure uma função de web toouse um tempo de execução do PHP que você fornecer, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="1ad54-156">tooconfigure a web role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="1ad54-157">Crie um projeto de Serviço do Azure e adicione uma função Web do PHP conforme descrito anteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="1ad54-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="1ad54-158">Criar um `php` pasta Olá `bin` pasta que está no diretório raiz da sua função web e, em seguida, adicionar toohello de tempo de execução (todos os binários, arquivos de configuração, as subpastas, etc.) o PHP `php` pasta.</span><span class="sxs-lookup"><span data-stu-id="1ad54-158">Create a `php` folder in hello `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="1ad54-159">(OPCIONAL) Se o tempo de execução do PHP usa Olá [Drivers da Microsoft para PHP para SQL Server][sqlsrv drivers], você precisará tooconfigure seu tooinstall de função web [SQL Server Native Client 2012] [ sql native client] quando ela é provisionada.</span><span class="sxs-lookup"><span data-stu-id="1ad54-159">(OPTIONAL) If your PHP runtime uses hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your web role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="1ad54-160">toodo isso, adicione Olá [sqlncli.msi x64 instalador] toohello `bin` pasta no diretório raiz da sua função web.</span><span class="sxs-lookup"><span data-stu-id="1ad54-160">toodo this, add hello [sqlncli.msi x64 installer] toohello `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="1ad54-161">script de inicialização de saudação descrito na próxima etapa do hello silenciosamente executará instalador hello quando a função hello é provisionada.</span><span class="sxs-lookup"><span data-stu-id="1ad54-161">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="1ad54-162">Se o tempo de execução do PHP não usar Olá Drivers da Microsoft para PHP para SQL Server, você pode remover Olá seguinte linha do script hello mostrado na próxima etapa do hello:</span><span class="sxs-lookup"><span data-stu-id="1ad54-162">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="1ad54-163">Definir uma tarefa de inicialização que configura [serviços de informações da Internet (IIS)] [ iis.net] toouse sua toohandle de tempo de execução do PHP as solicitações de `.php` páginas.</span><span class="sxs-lookup"><span data-stu-id="1ad54-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] toouse your PHP runtime toohandle requests for `.php` pages.</span></span> <span data-ttu-id="1ad54-164">toodo hello, abra `setup_web.cmd` arquivo (em Olá `bin` arquivo da pasta raiz da sua função web) em um editor de texto e substituir seu conteúdo com hello script a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad54-164">toodo this, open hello `setup_web.cmd` file (in hello `bin` file of your web role's root directory) in a text editor and replace its contents with hello following script:</span></span>

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. <span data-ttu-id="1ad54-165">Adicione o diretório raiz do aplicativo arquivos tooyour web da sua função.</span><span class="sxs-lookup"><span data-stu-id="1ad54-165">Add your application files tooyour web role's root directory.</span></span> <span data-ttu-id="1ad54-166">Esse será o diretório raiz do servidor da web hello.</span><span class="sxs-lookup"><span data-stu-id="1ad54-166">This will be hello web server's root directory.</span></span>
6. <span data-ttu-id="1ad54-167">Publicar seu aplicativo conforme descrito em Olá [publicar seu aplicativo](#publish-your-application) seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="1ad54-167">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="1ad54-168">Olá `download.ps1` script (em Olá `bin` pasta Olá web da raiz do diretório da função) podem ser excluídos após as etapas de saudação descritas acima para usar seu próprio tempo de execução do PHP.</span><span class="sxs-lookup"><span data-stu-id="1ad54-168">hello `download.ps1` script (in hello `bin` folder of hello web role's root directory) can be deleted after you follow hello steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a><span data-ttu-id="1ad54-169">Configurar um toouse de função de trabalho em seu próprio tempo de execução do PHP</span><span class="sxs-lookup"><span data-stu-id="1ad54-169">Configure a worker role toouse your own PHP runtime</span></span>
<span data-ttu-id="1ad54-170">tooconfigure uma função de trabalho toouse um tempo de execução do PHP que você fornecer, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="1ad54-170">tooconfigure a worker role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="1ad54-171">Crie um projeto de Serviço do Azure e adicione uma função de trabalho do PHP conforme descrito anteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="1ad54-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="1ad54-172">Criar um `php` pasta no diretório de raiz da função de trabalho Olá e, em seguida, adicione toohello de tempo de execução (todos os binários, arquivos de configuração, as subpastas, etc.) o PHP `php` pasta.</span><span class="sxs-lookup"><span data-stu-id="1ad54-172">Create a `php` folder in hello worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="1ad54-173">(OPCIONAL) Se o tempo de execução do PHP usa [Drivers da Microsoft para PHP para SQL Server][sqlsrv drivers], você precisará tooconfigure seu tooinstall da função de trabalho [SQL Server Native Client 2012] [ sql native client] quando ela é provisionada.</span><span class="sxs-lookup"><span data-stu-id="1ad54-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your worker role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="1ad54-174">toodo isso, adicione Olá [sqlncli.msi x64 instalador] diretório de raiz da função de trabalho toohello.</span><span class="sxs-lookup"><span data-stu-id="1ad54-174">toodo this, add hello [sqlncli.msi x64 installer] toohello worker role's root directory.</span></span> <span data-ttu-id="1ad54-175">script de inicialização de saudação descrito na próxima etapa do hello silenciosamente executará instalador hello quando a função hello é provisionada.</span><span class="sxs-lookup"><span data-stu-id="1ad54-175">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="1ad54-176">Se o tempo de execução do PHP não usar Olá Drivers da Microsoft para PHP para SQL Server, você pode remover Olá seguinte linha do script hello mostrado na próxima etapa do hello:</span><span class="sxs-lookup"><span data-stu-id="1ad54-176">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="1ad54-177">Definir uma tarefa de inicialização que adiciona o `php.exe` variável de ambiente do caminho da função de trabalho executável toohello quando a função hello é provisionada.</span><span class="sxs-lookup"><span data-stu-id="1ad54-177">Define a startup task that adds your `php.exe` executable toohello worker role's PATH environment variable when hello role is provisioned.</span></span> <span data-ttu-id="1ad54-178">toodo isso, abra Olá `setup_worker.cmd` (no diretório de raiz da função de trabalho Olá) em um editor de texto e substitua o seu conteúdo com hello script a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad54-178">toodo this, open hello `setup_worker.cmd` file (in hello worker role's root directory) in a text editor and replace its contents with hello following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service toohello web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. <span data-ttu-id="1ad54-179">Adicione o diretório raiz do seu aplicativo arquivos tooyour da função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1ad54-179">Add your application files tooyour worker role's root directory.</span></span>
6. <span data-ttu-id="1ad54-180">Publicar seu aplicativo conforme descrito em Olá [publicar seu aplicativo](#publish-your-application) seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="1ad54-180">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a><span data-ttu-id="1ad54-181">Executar o aplicativo no hello emuladores de computação e armazenamento</span><span class="sxs-lookup"><span data-stu-id="1ad54-181">Run your application in hello compute and storage emulators</span></span>
<span data-ttu-id="1ad54-182">Olá, emuladores do Azure fornecem um ambiente local em que você pode testar seu aplicativo do Azure antes de implantá-lo toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="1ad54-182">hello Azure emulators provide a local environment in which you can test your Azure application before you deploy it toohello cloud.</span></span> <span data-ttu-id="1ad54-183">Há algumas diferenças entre os emuladores de saudação e hello ambiente do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad54-183">There are some differences between hello emulators and hello Azure environment.</span></span> <span data-ttu-id="1ad54-184">toounderstand isso melhor, consulte [usar o emulador de armazenamento do Azure Olá para desenvolvimento e teste](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="1ad54-184">toounderstand this better, see [Use hello Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="1ad54-185">Observe que você deve ter o PHP instalado localmente emulador de computação toouse hello.</span><span class="sxs-lookup"><span data-stu-id="1ad54-185">Note that you must have PHP installed locally toouse hello compute emulator.</span></span> <span data-ttu-id="1ad54-186">o emulador de computação Olá usará em seu local toorun de instalação do PHP seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ad54-186">hello compute emulator will use your local PHP installation toorun your application.</span></span>

<span data-ttu-id="1ad54-187">toorun seu projeto no emuladores hello, execute Olá seguinte comando do diretório raiz do projeto:</span><span class="sxs-lookup"><span data-stu-id="1ad54-187">toorun your project in hello emulators, execute hello following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="1ad54-188">Você verá toothis semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="1ad54-188">You will see output similar toothis:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="1ad54-189">Você pode ver o aplicativo em execução no emulador Olá abrindo um navegador da web e navegação toohello endereço local mostrado na saída de hello (`http://127.0.0.1:81` na saída de exemplo hello acima).</span><span class="sxs-lookup"><span data-stu-id="1ad54-189">You can see your application running in hello emulator by opening a web browser and browsing toohello local address shown in hello output (`http://127.0.0.1:81` in hello example output above).</span></span>

<span data-ttu-id="1ad54-190">emuladores de saudação toostop, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="1ad54-190">toostop hello emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="1ad54-191">Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1ad54-191">Publish your application</span></span>
<span data-ttu-id="1ad54-192">toopublish seu aplicativo, é necessário importar toofirst suas configurações de publicação usando Olá [AzurePublishSettingsFile de importação](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ad54-192">toopublish your application, you need toofirst import your publish settings by using hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="1ad54-193">Em seguida, você pode publicar seu aplicativo usando Olá [AzureServiceProject publicar](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ad54-193">Then you can publish your application by using hello [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="1ad54-194">Para obter informações sobre como entrar em, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1ad54-194">For information about signing in, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ad54-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ad54-195">Next steps</span></span>
<span data-ttu-id="1ad54-196">Para obter mais informações, consulte Olá [Centro de desenvolvedores PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="1ad54-196">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[Azure SDK para PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[(. csdef) de definição de serviço]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[a configuração de serviço (. cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 instalador]: http://go.microsoft.com/fwlink/?LinkID=239648
