---
title: "Criar funções Web e de trabalho do Azure para PHP | Microsoft Docs"
description: "Um guia para a criação de funções da Web do PHP e de trabalho em um serviço de nuvem do Azure e para a configuração do tempo de execução do PHP."
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
ms.openlocfilehash: 214fdcfe20f3fa4ebcbe41308404f8b7e7d15310
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-php-web-and-worker-roles"></a><span data-ttu-id="0432b-103">Como criar funções Web e de trabalho do PHP</span><span class="sxs-lookup"><span data-stu-id="0432b-103">How to create PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="0432b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0432b-104">Overview</span></span>
<span data-ttu-id="0432b-105">Este guia mostrará como criar funções Web ou de trabalho do PHP em um ambiente de desenvolvimento Windows, como escolher uma versão específica do PHP nas versões "internas" disponíveis, como alterar a configuração do PHP, habilitar extensões e, finalmente, como implantar no Azure.</span><span class="sxs-lookup"><span data-stu-id="0432b-105">This guide will show you how to create PHP web or worker roles in a Windows development environment, choose a specific version of PHP from the "built-in" versions available, change the PHP configuration, enable extensions, and finally, deploy to Azure.</span></span> <span data-ttu-id="0432b-106">Também descreve como configurar uma função Web ou de trabalho para usar um tempo de execução do PHP (com configuração e extensões personalizadas) que você fornece.</span><span class="sxs-lookup"><span data-stu-id="0432b-106">It also describes how to configure a web or worker role to use a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="0432b-107">O que são funções Web e de Trabalho do PHP?</span><span class="sxs-lookup"><span data-stu-id="0432b-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="0432b-108">O Azure fornece três modelos de computação para a execução de aplicativos: Serviço de Aplicativo do Azure, Máquinas Virtuais do Azure e Serviços de Nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="0432b-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="0432b-109">Todos os três modelos oferecem suporte ao PHP.</span><span class="sxs-lookup"><span data-stu-id="0432b-109">All three models support PHP.</span></span> <span data-ttu-id="0432b-110">Os Serviços de Nuvem, que incluem as funções Web e de trabalho, fornecem a *PaaS (plataforma como serviço)*.</span><span class="sxs-lookup"><span data-stu-id="0432b-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="0432b-111">Dentro de um serviço de nuvem, uma função web fornece um servidor Web de IIS (Serviços de Informações da Internet) dedicado, usado para hospedar aplicativos Web de front-end.</span><span class="sxs-lookup"><span data-stu-id="0432b-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front-end web applications.</span></span> <span data-ttu-id="0432b-112">Uma função de trabalho pode executar tarefas assíncronas, de execução longa ou perpétuas, independentemente da interação do usuário ou da entrada.</span><span class="sxs-lookup"><span data-stu-id="0432b-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="0432b-113">Para obter mais informações sobre essas opções, consulte [Opções de hospedagem de computação fornecidas pelo Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="0432b-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="0432b-114">Baixar o SDK do Azure para PHP</span><span class="sxs-lookup"><span data-stu-id="0432b-114">Download the Azure SDK for PHP</span></span>
<span data-ttu-id="0432b-115">O [SDK do Azure para PHP] consiste em vários componentes.</span><span class="sxs-lookup"><span data-stu-id="0432b-115">The [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="0432b-116">Este artigo usará dois deles: o Azure PowerShell e os emuladores do Azure.</span><span class="sxs-lookup"><span data-stu-id="0432b-116">This article will use two of them: Azure PowerShell and the Azure emulators.</span></span> <span data-ttu-id="0432b-117">Esses dois componentes podem ser instalados pelo Microsoft Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="0432b-117">These two components can be installed via the Microsoft Web Platform Installer.</span></span> <span data-ttu-id="0432b-118">Para obter mais informações, confira [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0432b-118">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="0432b-119">Criar um projeto de Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="0432b-119">Create a Cloud Services project</span></span>
<span data-ttu-id="0432b-120">A primeira etapa na criação de uma função Web ou de trabalho do PHP é criar um projeto de Serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="0432b-120">The first step in creating a PHP web or worker role is to create an Azure Service project.</span></span> <span data-ttu-id="0432b-121">um projeto de Serviço do Azure serve como um contêiner lógico para as funções da Web e de trabalho, e contém os arquivos de [definição do serviço (.csdef) ] e [configuração do serviço (.cscfg)] do projeto.</span><span class="sxs-lookup"><span data-stu-id="0432b-121">an Azure Service project serves as a logical container for web and worker roles, and it contains the project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="0432b-122">Para criar um novo projeto de Serviço do Azure, execute o Azure PowerShell como administrador e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0432b-122">To create a new Azure Service project, run Azure PowerShell as an administrator, and execute the following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="0432b-123">Esse comando criará um novo diretório (`myProject`) ao qual você pode adicionar funções Web e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0432b-123">This command will create a new directory (`myProject`) to which you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="0432b-124">Adicionar funções de trabalho ou Web PHP</span><span class="sxs-lookup"><span data-stu-id="0432b-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="0432b-125">Para adicionar uma função Web do PHP a um projeto, execute o seguinte comando no diretório raiz do projeto:</span><span class="sxs-lookup"><span data-stu-id="0432b-125">To add a PHP web role to a project, run the following command from within the project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="0432b-126">Para uma função de trabalho, use este comando:</span><span class="sxs-lookup"><span data-stu-id="0432b-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="0432b-127">O `roleName` é opcional.</span><span class="sxs-lookup"><span data-stu-id="0432b-127">The `roleName` parameter is optional.</span></span> <span data-ttu-id="0432b-128">Se for omitido, o nome da função será gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0432b-128">If it is omitted, the role name will be automatically generated.</span></span> <span data-ttu-id="0432b-129">A primeira função web criada será `WebRole1`, a segunda será `WebRole2` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="0432b-129">The first web role created will be `WebRole1`, the second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="0432b-130">A primeira função de trabalho criada será `WorkerRole1`, a segunda será `WorkerRole2` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="0432b-130">The first worker role created will be `WorkerRole1`, the second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-the-built-in-php-version"></a><span data-ttu-id="0432b-131">Especificar a versão do PHP interno</span><span class="sxs-lookup"><span data-stu-id="0432b-131">Specify the built-in PHP version</span></span>
<span data-ttu-id="0432b-132">Quando você adiciona uma função Web ou de trabalho do PHP a um projeto, os arquivos de configuração do projeto são modificados para que o PHP seja instalado em cada instância da web ou de trabalho do seu aplicativo quando ele for implantado.</span><span class="sxs-lookup"><span data-stu-id="0432b-132">When you add a PHP web or worker role to a project, the project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="0432b-133">Para ver a versão do PHP que será instalada por padrão, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0432b-133">To see the version of PHP that will be installed by default, run the following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="0432b-134">A saída do comando acima será semelhante à mostrada a seguir.</span><span class="sxs-lookup"><span data-stu-id="0432b-134">The output from the command above will look similar to what is shown below.</span></span> <span data-ttu-id="0432b-135">Neste exemplo, o sinalizador `IsDefault` está definido como `true` para PHP 5.3.17 indicando que ele será a versão do PHP padrão instalada.</span><span class="sxs-lookup"><span data-stu-id="0432b-135">In this example, the `IsDefault` flag is set to `true` for PHP 5.3.17, indicating that it will be the default PHP version installed.</span></span>

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

<span data-ttu-id="0432b-136">Você pode definir a versão de tempo de execução do PHP para qualquer uma das versões do PHP listadas.</span><span class="sxs-lookup"><span data-stu-id="0432b-136">You can set the PHP runtime version to any of the PHP versions that are listed.</span></span> <span data-ttu-id="0432b-137">Por exemplo, para definir a versão do PHP (para uma função com o nome `roleName`) como 5.4.0, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0432b-137">For example, to set the PHP version (for a role with the name `roleName`) to 5.4.0, use the following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="0432b-138">As versões de PHP disponíveis podem mudar no futuro.</span><span class="sxs-lookup"><span data-stu-id="0432b-138">Available PHP versions may change in the future.</span></span>
>
>

## <a name="customize-the-built-in-php-runtime"></a><span data-ttu-id="0432b-139">Personalizar o tempo de execução do PHP interno</span><span class="sxs-lookup"><span data-stu-id="0432b-139">Customize the built-in PHP runtime</span></span>
<span data-ttu-id="0432b-140">Você tem controle total sobre a configuração do tempo de execução do PHP que é instalado quando você segue as etapas acima, incluindo a modificação das configurações de `php.ini` e a habilitação de extensões.</span><span class="sxs-lookup"><span data-stu-id="0432b-140">You have complete control over the configuration of the PHP runtime that is installed when you follow the steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="0432b-141">Para personalizar o tempo de execução do PHP interno, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="0432b-141">To customize the built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="0432b-142">Adicione uma nova pasta, chamada `php`, ao diretório `bin` da sua função web.</span><span class="sxs-lookup"><span data-stu-id="0432b-142">Add a new folder, named `php`, to the `bin` directory of your web role.</span></span> <span data-ttu-id="0432b-143">Para uma função de trabalho, adicione-o ao diretório raiz da função.</span><span class="sxs-lookup"><span data-stu-id="0432b-143">For a worker role, add it to the role's root directory.</span></span>
2. <span data-ttu-id="0432b-144">Na pasta `php`, crie outra pasta chamada `ext`.</span><span class="sxs-lookup"><span data-stu-id="0432b-144">In the `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="0432b-145">Coloque todos os arquivos de extensão `.dll` (por exemplo, `php_mongo.dll`) que você deseja habilitar nessa pasta.</span><span class="sxs-lookup"><span data-stu-id="0432b-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want to enable in this folder.</span></span>
3. <span data-ttu-id="0432b-146">Adicionar um arquivo `php.ini` à pasta `php`.</span><span class="sxs-lookup"><span data-stu-id="0432b-146">Add a `php.ini` file to the `php` folder.</span></span> <span data-ttu-id="0432b-147">Habilite todas as extensões personalizadas e defina todas as diretivas do PHP nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="0432b-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="0432b-148">Por exemplo, se você quiser ativar o `display_errors` e habilitar a extensão `php_mongo.dll`, os conteúdos do seu arquivo `php.ini` serão da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0432b-148">For example, if you wanted to turn `display_errors` on and enable the `php_mongo.dll` extension, the contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="0432b-149">Todas as configurações que você não definir explicitamente no arquivo `php.ini` que você fornecer serão definidas automaticamente para seus valores padrão.</span><span class="sxs-lookup"><span data-stu-id="0432b-149">Any settings that you don't explicitly set in the `php.ini` file that you provide will automatically be set to their default values.</span></span> <span data-ttu-id="0432b-150">No entanto, lembre-se de que você pode adicionar um arquivo `php.ini` completo.</span><span class="sxs-lookup"><span data-stu-id="0432b-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="0432b-151">Usar seu próprio tempo de execução PHP</span><span class="sxs-lookup"><span data-stu-id="0432b-151">Use your own PHP runtime</span></span>
<span data-ttu-id="0432b-152">Em alguns casos, em vez de selecionar um tempo de execução do PHP interno e configurá-lo conforme descrito acima, você pode desejar fornecer seu próprio tempo de execução do PHP.</span><span class="sxs-lookup"><span data-stu-id="0432b-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want to provide your own PHP runtime.</span></span> <span data-ttu-id="0432b-153">Por exemplo, você pode usar o mesmo tempo de execução do PHP em uma função Web ou de trabalho que você usa no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="0432b-153">For example, you can use the same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="0432b-154">Isso torna mais fácil garantir que o aplicativo não mudará o comportamento no ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0432b-154">This makes it easier to ensure that the application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-to-use-your-own-php-runtime"></a><span data-ttu-id="0432b-155">Configurar uma função web para usar o seu próprio tempo de execução do PHP</span><span class="sxs-lookup"><span data-stu-id="0432b-155">Configure a web role to use your own PHP runtime</span></span>
<span data-ttu-id="0432b-156">Para configurar uma função web para usar um tempo de execução do PHP fornecido por você, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0432b-156">To configure a web role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="0432b-157">Crie um projeto de Serviço do Azure e adicione uma função Web do PHP conforme descrito anteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="0432b-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="0432b-158">Crie uma pasta `php` na pasta `bin` que está no diretório raiz de sua função web e adicione o tempo de execução do PHP (todos os binários, arquivos de configuração, subpastas etc.) à pasta `php`.</span><span class="sxs-lookup"><span data-stu-id="0432b-158">Create a `php` folder in the `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="0432b-159">(OPCIONAL) Se o tempo de execução do PHP usar os [Drivers da Microsoft para PHP para SQL Server][sqlsrv drivers], você precisará configurar a função Web para instalar o [SQL Server Native Client 2012][sql native client] quando ela for provisionada.</span><span class="sxs-lookup"><span data-stu-id="0432b-159">(OPTIONAL) If your PHP runtime uses the [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your web role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="0432b-160">Para fazer isso, adicione o [instalador sqlncli.msi x64] à pasta `bin` no diretório-raiz de sua função Web.</span><span class="sxs-lookup"><span data-stu-id="0432b-160">To do this, add the [sqlncli.msi x64 installer] to the `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="0432b-161">O script de inicialização descrito na próxima etapa executará o instalador silenciosamente quando a função for provisionada.</span><span class="sxs-lookup"><span data-stu-id="0432b-161">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="0432b-162">Se o tempo de execução do PHP não usar os Drivers Microsoft para PHP para SQL Server, você poderá remover a seguinte linha do script mostrado na próxima etapa:</span><span class="sxs-lookup"><span data-stu-id="0432b-162">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="0432b-163">Defina uma tarefa de inicialização que configura os [Serviços de Informações da Internet (IIS)][iis.net] para usar o tempo de execução do PHP para manipular solicitações de páginas `.php`.</span><span class="sxs-lookup"><span data-stu-id="0432b-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] to use your PHP runtime to handle requests for `.php` pages.</span></span> <span data-ttu-id="0432b-164">Para fazer isso, abra o arquivo `setup_web.cmd` (no arquivo `bin` do diretório raiz da função web) em um editor de texto e substitua seu conteúdo pelo script a seguir:</span><span class="sxs-lookup"><span data-stu-id="0432b-164">To do this, open the `setup_web.cmd` file (in the `bin` file of your web role's root directory) in a text editor and replace its contents with the following script:</span></span>

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
5. <span data-ttu-id="0432b-165">Adicione os arquivos do aplicativo ao diretório raiz da função Web.</span><span class="sxs-lookup"><span data-stu-id="0432b-165">Add your application files to your web role's root directory.</span></span> <span data-ttu-id="0432b-166">Esse será o diretório raiz do servidor web.</span><span class="sxs-lookup"><span data-stu-id="0432b-166">This will be the web server's root directory.</span></span>
6. <span data-ttu-id="0432b-167">Publique seu aplicativo como descrito na seção abaixo, [Publicar seu aplicativo](#publish-your-application).</span><span class="sxs-lookup"><span data-stu-id="0432b-167">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="0432b-168">O script `download.ps1` (na pasta `bin` do diretório raiz da função web) pode ser excluído após a realização das etapas descritas acima para usar seu próprio tempo de execução do PHP.</span><span class="sxs-lookup"><span data-stu-id="0432b-168">The `download.ps1` script (in the `bin` folder of the web role's root directory) can be deleted after you follow the steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-to-use-your-own-php-runtime"></a><span data-ttu-id="0432b-169">Configurar uma função de trabalho para usar o seu próprio tempo de execução do PHP</span><span class="sxs-lookup"><span data-stu-id="0432b-169">Configure a worker role to use your own PHP runtime</span></span>
<span data-ttu-id="0432b-170">Para configurar uma função de trabalho para usar um tempo de execução do PHP fornecido por você, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0432b-170">To configure a worker role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="0432b-171">Crie um projeto de Serviço do Azure e adicione uma função de trabalho do PHP conforme descrito anteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="0432b-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="0432b-172">Crie uma pasta `php` no diretório raiz de sua função de trabalho e adicione o tempo de execução do PHP (todos os binários, arquivos de configuração, subpastas etc.) para a pasta `php`.</span><span class="sxs-lookup"><span data-stu-id="0432b-172">Create a `php` folder in the worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="0432b-173">(OPCIONAL) Se o tempo de execução do PHP usar [Drivers da Microsoft para PHP para SQL Server][sqlsrv drivers], você precisará configurar a função de trabalho para instalar o [SQL Server Native Client 2012][sql native client] quando ela for provisionada.</span><span class="sxs-lookup"><span data-stu-id="0432b-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your worker role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="0432b-174">Para fazer isso, adicione o [instalador sqlncli.msi x64] ao diretório raiz da função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0432b-174">To do this, add the [sqlncli.msi x64 installer] to the worker role's root directory.</span></span> <span data-ttu-id="0432b-175">O script de inicialização descrito na próxima etapa executará o instalador silenciosamente quando a função for provisionada.</span><span class="sxs-lookup"><span data-stu-id="0432b-175">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="0432b-176">Se o tempo de execução do PHP não usar os Drivers Microsoft para PHP para SQL Server, você poderá remover a seguinte linha do script mostrado na próxima etapa:</span><span class="sxs-lookup"><span data-stu-id="0432b-176">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="0432b-177">Defina uma tarefa de inicialização que adiciona o executável `php.exe` à variável de ambiente PATH da função de trabalho quando a função é configurada.</span><span class="sxs-lookup"><span data-stu-id="0432b-177">Define a startup task that adds your `php.exe` executable to the worker role's PATH environment variable when the role is provisioned.</span></span> <span data-ttu-id="0432b-178">Para fazer isso, abra o arquivo `setup_worker.cmd` (no diretório raiz da função de trabalho) em um editor de texto e substitua seu conteúdo pelo script a seguir:</span><span class="sxs-lookup"><span data-stu-id="0432b-178">To do this, open the `setup_worker.cmd` file (in the worker role's root directory) in a text editor and replace its contents with the following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service to the web root directory...
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
5. <span data-ttu-id="0432b-179">Adicione os arquivos do aplicativo ao diretório raiz da função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0432b-179">Add your application files to your worker role's root directory.</span></span>
6. <span data-ttu-id="0432b-180">Publique seu aplicativo como descrito na seção abaixo, [Publicar seu aplicativo](#publish-your-application).</span><span class="sxs-lookup"><span data-stu-id="0432b-180">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-the-compute-and-storage-emulators"></a><span data-ttu-id="0432b-181">Executar seu aplicativo nos emuladores de computação e de armazenamento</span><span class="sxs-lookup"><span data-stu-id="0432b-181">Run your application in the compute and storage emulators</span></span>
<span data-ttu-id="0432b-182">Os emuladores do Azure fornecem um ambiente local no qual você pode testar seu aplicativo do Azure antes de implantá-lo na nuvem.</span><span class="sxs-lookup"><span data-stu-id="0432b-182">The Azure emulators provide a local environment in which you can test your Azure application before you deploy it to the cloud.</span></span> <span data-ttu-id="0432b-183">Existem algumas diferenças entre os emuladores e o ambiente do Azure.</span><span class="sxs-lookup"><span data-stu-id="0432b-183">There are some differences between the emulators and the Azure environment.</span></span> <span data-ttu-id="0432b-184">Para entender isso melhor, consulte [Usar o emulador de armazenamento do Azure para desenvolvimento e teste](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="0432b-184">To understand this better, see [Use the Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="0432b-185">Observe que você deve ter instalado o PHP localmente para usar o emulador de computação.</span><span class="sxs-lookup"><span data-stu-id="0432b-185">Note that you must have PHP installed locally to use the compute emulator.</span></span> <span data-ttu-id="0432b-186">O emulador de computação usará sua instalação local do PHP para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0432b-186">The compute emulator will use your local PHP installation to run your application.</span></span>

<span data-ttu-id="0432b-187">Para executar seu projeto nos emuladores, execute o seguinte comando no diretório raiz do projeto:</span><span class="sxs-lookup"><span data-stu-id="0432b-187">To run your project in the emulators, execute the following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="0432b-188">Você verá uma saída semelhante a essa:</span><span class="sxs-lookup"><span data-stu-id="0432b-188">You will see output similar to this:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="0432b-189">Você pode ver o aplicativo em execução no emulador abrindo um navegador da Web e navegando até o endereço local mostrado na saída (`http://127.0.0.1:81` na saída de exemplo acima).</span><span class="sxs-lookup"><span data-stu-id="0432b-189">You can see your application running in the emulator by opening a web browser and browsing to the local address shown in the output (`http://127.0.0.1:81` in the example output above).</span></span>

<span data-ttu-id="0432b-190">Para parar os emuladores, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="0432b-190">To stop the emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="0432b-191">Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="0432b-191">Publish your application</span></span>
<span data-ttu-id="0432b-192">Para publicar seu aplicativo, você precisa primeiro importar suas configurações de publicação usando o cmdlet [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) .</span><span class="sxs-lookup"><span data-stu-id="0432b-192">To publish your application, you need to first import your publish settings by using the [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="0432b-193">Em seguida, você pode publicar o aplicativo usando o cmdlet [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) .</span><span class="sxs-lookup"><span data-stu-id="0432b-193">Then you can publish your application by using the [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="0432b-194">Para obter informações sobre como entrar, confira [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0432b-194">For information about signing in, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0432b-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0432b-195">Next steps</span></span>
<span data-ttu-id="0432b-196">Para obter mais informações, consulte o [Centro de Desenvolvimento PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="0432b-196">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[SDK do Azure para PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[definição do serviço (.csdef) ]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[configuração do serviço (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[instalador sqlncli.msi x64]: http://go.microsoft.com/fwlink/?LinkID=239648
