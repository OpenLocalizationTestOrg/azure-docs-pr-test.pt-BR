---
title: "aaaConfigure PHP em aplicativos de Web do serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba como tooconfigure Olá instalação do PHP padrão ou adicionar uma instalação personalizada do PHP para aplicativos Web no serviço de aplicativo do Azure."
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2e461e4a269a4ce5614f5f05560f38bc53066251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="8e847-103">Configurar o PHP em aplicativos Web do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="8e847-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="8e847-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="8e847-104">Introduction</span></span>
<span data-ttu-id="8e847-105">Este guia mostrará como tooconfigure Olá interno em tempo de execução do PHP para aplicativos Web no [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714), forneça um tempo de execução do PHP personalizado e habilitar extensões.</span><span class="sxs-lookup"><span data-stu-id="8e847-105">This guide will show you how tooconfigure hello built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="8e847-106">toouse do serviço de aplicativo, inscreva-se para Olá [avaliação gratuita].</span><span class="sxs-lookup"><span data-stu-id="8e847-106">toouse App Service, sign up for hello [free trial].</span></span> <span data-ttu-id="8e847-107">Olá tooget mais deste guia, você deve primeiro criar um aplicativo web do PHP no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e847-107">tooget hello most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a><span data-ttu-id="8e847-108">Como: versão do PHP alteração Olá interno</span><span class="sxs-lookup"><span data-stu-id="8e847-108">How to: Change hello built-in PHP version</span></span>
<span data-ttu-id="8e847-109">Por padrão, quando você cria um aplicativo Web do Serviço de Aplicativo, o PHP 5.5 é instalado e fica imediatamente disponível para uso.</span><span class="sxs-lookup"><span data-stu-id="8e847-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="8e847-110">Olá melhor maneira toosee Olá disponível revisão, sua configuração padrão, e extensões habilitadas hello é toodeploy um script que chama Olá [phpinfo ()] função.</span><span class="sxs-lookup"><span data-stu-id="8e847-110">hello best way toosee hello available release revision, its default configuration, and hello enabled extensions is toodeploy a script that calls hello [phpinfo()] function.</span></span>

<span data-ttu-id="8e847-111">As versões 5.6 e 7.0 do PHP também estão disponíveis, mas não são habilitadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="8e847-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="8e847-112">Olá tooupdate versão do PHP, siga um destes métodos:</span><span class="sxs-lookup"><span data-stu-id="8e847-112">tooupdate hello PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="8e847-113">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8e847-113">Azure Portal</span></span>
1. <span data-ttu-id="8e847-114">Procurar o aplicativo web de tooyour Olá [Portal do Azure](https://portal.azure.com) e clique em Olá **configurações** botão.</span><span class="sxs-lookup"><span data-stu-id="8e847-114">Browse tooyour web app in hello [Azure Portal](https://portal.azure.com) and click on hello **Settings** button.</span></span>
   
    ![Configurações do aplicativo Web][settings-button]
2. <span data-ttu-id="8e847-116">De saudação **configurações** selecione folha **configurações de aplicativo** e escolha a nova versão do PHP hello.</span><span class="sxs-lookup"><span data-stu-id="8e847-116">From hello **Settings** blade select **Application Settings** and choose hello new PHP version.</span></span>
   
    ![Configurações do aplicativo][application-settings]
3. <span data-ttu-id="8e847-118">Clique em Olá **salvar** botão na parte superior de saudação do hello **configurações de aplicativo da Web** folha.</span><span class="sxs-lookup"><span data-stu-id="8e847-118">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Salvar definições de configuração][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="8e847-120">PowerShell do Azure (Windows)</span><span class="sxs-lookup"><span data-stu-id="8e847-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="8e847-121">Abra o PowerShell do Azure e a conta de logon do tooyour:</span><span class="sxs-lookup"><span data-stu-id="8e847-121">Open Azure PowerShell, and login tooyour account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="8e847-122">Defina a versão do PHP Olá para o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e847-122">Set hello PHP version for hello web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="8e847-123">versão do PHP Olá agora está definido.</span><span class="sxs-lookup"><span data-stu-id="8e847-123">hello PHP version is now set.</span></span> <span data-ttu-id="8e847-124">Você pode confirmar essas configurações:</span><span class="sxs-lookup"><span data-stu-id="8e847-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="8e847-125">Interface de linha de comando do Azure (Linux, Mac, Windows)</span><span class="sxs-lookup"><span data-stu-id="8e847-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="8e847-126">toouse Olá Interface de linha de comando do Azure, você deve ter **Node.js** instalado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8e847-126">toouse hello Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="8e847-127">Abra o Terminal e conta de logon do tooyour.</span><span class="sxs-lookup"><span data-stu-id="8e847-127">Open Terminal, and login tooyour account.</span></span>
   
        azure login
2. <span data-ttu-id="8e847-128">Defina a versão do PHP Olá para o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e847-128">Set hello PHP version for hello web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="8e847-129">versão do PHP Olá agora está definido.</span><span class="sxs-lookup"><span data-stu-id="8e847-129">hello PHP version is now set.</span></span> <span data-ttu-id="8e847-130">Você pode confirmar essas configurações:</span><span class="sxs-lookup"><span data-stu-id="8e847-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="8e847-131">Olá [2.0 do CLI do Azure](https://github.com/Azure/azure-cli) comandos são equivalente toohello acima são:</span><span class="sxs-lookup"><span data-stu-id="8e847-131">hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent toohello above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a><span data-ttu-id="8e847-132">Como: alterar as configurações de PHP internas Olá</span><span class="sxs-lookup"><span data-stu-id="8e847-132">How to: Change hello built-in PHP configurations</span></span>
<span data-ttu-id="8e847-133">Para qualquer tempo de execução do PHP interno, você pode alterar qualquer uma das opções de configuração de saudação seguindo as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="8e847-133">For any built-in PHP runtime, you can change any of hello configuration options by following hello steps below.</span></span> <span data-ttu-id="8e847-134">(Para obter informações sobre diretrizes de php. ini, consulte [Lista de diretrizes de php. ini].)</span><span class="sxs-lookup"><span data-stu-id="8e847-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="8e847-135">Alterando as configurações de PHP\_INI\_USER, PHP\_INI\_PERDIR e PHP\_INI\_ALL</span><span class="sxs-lookup"><span data-stu-id="8e847-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="8e847-136">Adicionar um [. user.ini] diretório raiz do arquivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="8e847-136">Add a [.user.ini] file tooyour root directory.</span></span>
2. <span data-ttu-id="8e847-137">Adicionar configuração configurações toohello `.user.ini` arquivo usando Olá a mesma sintaxe que você usaria em um `php.ini` arquivo.</span><span class="sxs-lookup"><span data-stu-id="8e847-137">Add configuration settings toohello `.user.ini` file using hello same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="8e847-138">Por exemplo, se você quisesse Olá tooturn `display_errors` configuração e defina `upload_max_filesize` configuração too10M, o `.user.ini` arquivo deve conter este texto:</span><span class="sxs-lookup"><span data-stu-id="8e847-138">For example, if you wanted tooturn hello `display_errors` setting on and set `upload_max_filesize` setting too10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="8e847-139">Implante seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8e847-139">Deploy your web app.</span></span>
4. <span data-ttu-id="8e847-140">Reinicie o aplicativo da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e847-140">Restart hello web app.</span></span> <span data-ttu-id="8e847-141">(Reinicialização é necessária porque frequência Olá com o PHP lê `.user.ini` arquivos é controlado por Olá `user_ini.cache_ttl` configuração, que é uma configuração de nível de sistema e é de 300 segundos (5 minutos) por padrão.</span><span class="sxs-lookup"><span data-stu-id="8e847-141">(Restarting is necessary because hello frequency with which PHP reads `.user.ini` files is governed by hello `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="8e847-142">Reiniciar aplicativo web de saudação força PHP tooread Olá novas configurações na Olá `.user.ini` arquivo.)</span><span class="sxs-lookup"><span data-stu-id="8e847-142">Restarting hello web app forces PHP tooread hello new settings in hello `.user.ini` file.)</span></span>

<span data-ttu-id="8e847-143">Como uma alternativa toousing um `.user.ini` arquivo, você pode usar o hello [ini_set()] função nas opções de configuração de tooset de scripts que não são diretivas de nível de sistema.</span><span class="sxs-lookup"><span data-stu-id="8e847-143">As an alternative toousing a `.user.ini` file, you can use hello [ini_set()] function in scripts tooset configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="8e847-144">Alterando as configurações de PHP\_INI\_SYSTEM</span><span class="sxs-lookup"><span data-stu-id="8e847-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="8e847-145">Adicionar um tooyour de configuração do aplicativo Web App com chave Olá `PHP_INI_SCAN_DIR` e valor`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="8e847-145">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="8e847-146">Criar um `settings.ini` arquivo usando o Console do Kudu (http://&lt;nome do site&gt;. scm.azurewebsite.net) no hello `d:\home\site\ini` directory.</span><span class="sxs-lookup"><span data-stu-id="8e847-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in hello `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="8e847-147">Adicionar configuração configurações toohello `settings.ini` arquivo usando Olá a mesma sintaxe que você usaria em um arquivo php.ini.</span><span class="sxs-lookup"><span data-stu-id="8e847-147">Add configuration settings toohello `settings.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="8e847-148">Por exemplo, se você quisesse Olá toopoint `curl.cainfo` configuração tooa `*.crt` arquivo e defina 'wincache.maxfilesize' configuração too512K, o `settings.ini` arquivo deve conter este texto:</span><span class="sxs-lookup"><span data-stu-id="8e847-148">For example, if you wanted toopoint hello `curl.cainfo` setting tooa `*.crt` file and set 'wincache.maxfilesize' setting too512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="8e847-149">Reinicie as alterações do aplicativo Web tooload hello.</span><span class="sxs-lookup"><span data-stu-id="8e847-149">Restart your Web App tooload hello changes.</span></span>

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a><span data-ttu-id="8e847-150">Como: habilitar extensões em tempo de execução do PHP saudação padrão</span><span class="sxs-lookup"><span data-stu-id="8e847-150">How to: Enable extensions in hello default PHP runtime</span></span>
<span data-ttu-id="8e847-151">Conforme observado na seção anterior hello, Olá melhor maneira toosee Olá versão padrão do PHP, sua configuração padrão e Olá habilitado extensões é toodeploy um script que chama [phpinfo ()].</span><span class="sxs-lookup"><span data-stu-id="8e847-151">As noted in hello previous section, hello best way toosee hello default PHP version, its default configuration, and hello enabled extensions is toodeploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="8e847-152">extensões adicionais de tooenable, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="8e847-152">tooenable additional extensions, follow hello steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="8e847-153">Configurar por meio de configurações ini</span><span class="sxs-lookup"><span data-stu-id="8e847-153">Configure via ini settings</span></span>
1. <span data-ttu-id="8e847-154">Adicionar um `ext` toohello diretório `d:\home\site` directory.</span><span class="sxs-lookup"><span data-stu-id="8e847-154">Add a `ext` directory toohello `d:\home\site` directory.</span></span>
2. <span data-ttu-id="8e847-155">Colocar `.dll` arquivos de extensão no hello `ext` diretório (por exemplo, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="8e847-155">Put `.dll` extension files in hello `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="8e847-156">Certifique-se de que as extensões de hello são compatíveis com a versão padrão do PHP e são VC9 e compatível com o non-thread-safe (ntes).</span><span class="sxs-lookup"><span data-stu-id="8e847-156">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="8e847-157">Adicionar um tooyour de configuração do aplicativo Web App com chave Olá `PHP_INI_SCAN_DIR` e valor`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="8e847-157">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="8e847-158">Crie um arquivo `ini` em `d:\home\site\ini` chamado `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="8e847-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="8e847-159">Adicionar configuração configurações toohello `extensions.ini` arquivo usando Olá a mesma sintaxe que você usaria em um arquivo php.ini.</span><span class="sxs-lookup"><span data-stu-id="8e847-159">Add configuration settings toohello `extensions.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="8e847-160">Por exemplo, se você quisesse tooenable Olá MongoDB e XDebug extensões, seu `extensions.ini` arquivo deve conter este texto:</span><span class="sxs-lookup"><span data-stu-id="8e847-160">For example, if you wanted tooenable hello MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="8e847-161">Reinicie as alterações do aplicativo Web tooload hello.</span><span class="sxs-lookup"><span data-stu-id="8e847-161">Restart your Web App tooload hello changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="8e847-162">Configurar por meio de Configuração de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8e847-162">Configure via App Setting</span></span>
1. <span data-ttu-id="8e847-163">Adicionar um `bin` diretório raiz do diretório toohello.</span><span class="sxs-lookup"><span data-stu-id="8e847-163">Add a `bin` directory toohello root directory.</span></span>
2. <span data-ttu-id="8e847-164">Colocar `.dll` arquivos de extensão no hello `bin` diretório (por exemplo, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="8e847-164">Put `.dll` extension files in hello `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="8e847-165">Certifique-se de que as extensões de hello são compatíveis com a versão padrão do PHP e são VC9 e compatível com o non-thread-safe (ntes).</span><span class="sxs-lookup"><span data-stu-id="8e847-165">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="8e847-166">Implante seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8e847-166">Deploy your web app.</span></span>
4. <span data-ttu-id="8e847-167">Procurar o aplicativo web de tooyour Olá Portal do Azure e clique em Olá **configurações** botão.</span><span class="sxs-lookup"><span data-stu-id="8e847-167">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Configurações do aplicativo Web][settings-button]
5. <span data-ttu-id="8e847-169">De saudação **configurações** selecione folha **configurações do aplicativo** e role toohello **configurações do aplicativo** seção.</span><span class="sxs-lookup"><span data-stu-id="8e847-169">From hello **Settings** blade select **Application Settings** and scroll toohello **App settings** section.</span></span>
6. <span data-ttu-id="8e847-170">Em Olá **configurações do aplicativo** seção, crie um **PHP_EXTENSIONS** chave.</span><span class="sxs-lookup"><span data-stu-id="8e847-170">In hello **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="8e847-171">valor de saudação para essa chave seria uma raiz do caminho relativo toowebsite: **bin\your-ext-arquivo**.</span><span class="sxs-lookup"><span data-stu-id="8e847-171">hello value for this key would be a path relative toowebsite root: **bin\your-ext-file**.</span></span>
   
    ![Habilitar extensões em configurações do aplicativo][php-extensions]
7. <span data-ttu-id="8e847-173">Clique em Olá **salvar** botão na parte superior de saudação do hello **configurações de aplicativo da Web** folha.</span><span class="sxs-lookup"><span data-stu-id="8e847-173">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Salvar definições de configuração][save-button]

<span data-ttu-id="8e847-175">Também há suporte para extensões Zend usando uma chave **PHP_ZENDEXTENSIONS**.</span><span class="sxs-lookup"><span data-stu-id="8e847-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="8e847-176">tooenable várias extensões, incluir uma lista separada por vírgulas de `.dll` arquivos para o valor de configuração de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8e847-176">tooenable multiple extensions, include a comma-separated list of `.dll` files for hello app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="8e847-177">Como: usar um tempo de execução personalizado do PHP</span><span class="sxs-lookup"><span data-stu-id="8e847-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="8e847-178">Em vez de tempo de execução de saudação padrão PHP, aplicativos de Web do serviço de aplicativo pode usar um tempo de execução do PHP que você forneça tooexecute scripts PHP.</span><span class="sxs-lookup"><span data-stu-id="8e847-178">Instead of hello default PHP runtime, App Service Web Apps can use a PHP runtime that you provide tooexecute PHP scripts.</span></span> <span data-ttu-id="8e847-179">Olá em tempo de execução que você fornece pode ser configurado por um `php.ini` arquivo que você fornecer também.</span><span class="sxs-lookup"><span data-stu-id="8e847-179">hello runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="8e847-180">toouse um tempo de execução do PHP personalizado com aplicativos da Web, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="8e847-180">toouse a custom PHP runtime with Web Apps, follow hello steps below.</span></span>

1. <span data-ttu-id="8e847-181">Obtenha uma versão do PHP ou VC11 para Windows que seja não thread safe e compatível com a versão VC9.</span><span class="sxs-lookup"><span data-stu-id="8e847-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="8e847-182">Versões recentes do PHP para Windows podem ser encontradas aqui: [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="8e847-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="8e847-183">Versões mais antigas podem ser encontrados no arquivo de saudação aqui: [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="8e847-183">Older releases can be found in hello archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="8e847-184">Modificar Olá `php.ini` arquivo para o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="8e847-184">Modify hello `php.ini` file for your runtime.</span></span> <span data-ttu-id="8e847-185">Observe que quaisquer definições de configuração que forem diretrizes exclusivamente de nível de sistema serão ignoradas por Aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="8e847-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="8e847-186">(Para informações sobre diretrizes de nível de sistema apenas, consulte [Lista de diretrizes de php. ini].)</span><span class="sxs-lookup"><span data-stu-id="8e847-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="8e847-187">Opcionalmente, adicione o tempo de execução do PHP extensões tooyour e habilitá-las no hello `php.ini` arquivo.</span><span class="sxs-lookup"><span data-stu-id="8e847-187">Optionally, add extensions tooyour PHP runtime and enable them in hello `php.ini` file.</span></span>
4. <span data-ttu-id="8e847-188">Adicionar um `bin` diretório raiz do diretório tooyour e diretório de saudação put que contém o tempo de execução do PHP nele (por exemplo, `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="8e847-188">Add a `bin` directory tooyour root directory, and put hello directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="8e847-189">Implante seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8e847-189">Deploy your web app.</span></span>
6. <span data-ttu-id="8e847-190">Procurar o aplicativo web de tooyour Olá Portal do Azure e clique em Olá **configurações** botão.</span><span class="sxs-lookup"><span data-stu-id="8e847-190">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Configurações do aplicativo Web][settings-button]
7. <span data-ttu-id="8e847-192">De saudação **configurações** selecione folha **configurações do aplicativo** e role toohello **mapeamentos de manipulador** seção.</span><span class="sxs-lookup"><span data-stu-id="8e847-192">From hello **Settings** blade select **Application Settings** and scroll toohello **Handler mappings** section.</span></span> <span data-ttu-id="8e847-193">Adicionar `*.php` toohello extensão de campo e adicionar Olá caminho toohello `php-cgi.exe` executável.</span><span class="sxs-lookup"><span data-stu-id="8e847-193">Add `*.php` toohello Extension field and add hello path toohello `php-cgi.exe` executable.</span></span> <span data-ttu-id="8e847-194">Se você colocar o tempo de execução do PHP no hello `bin` diretório na raiz de saudação do seu aplicativo, o caminho de saudação será `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="8e847-194">If you put your PHP runtime in hello `bin` directory in hello root of you application, hello path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![Especificar o manipulador em mapeamentos de manipulador][handler-mappings]
8. <span data-ttu-id="8e847-196">Clique em Olá **salvar** botão na parte superior de saudação do hello **configurações de aplicativo da Web** folha.</span><span class="sxs-lookup"><span data-stu-id="8e847-196">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Salvar definições de configuração][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="8e847-198">Como habilitar a automação do Criador no Azure</span><span class="sxs-lookup"><span data-stu-id="8e847-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="8e847-199">Por padrão, o Serviço de Aplicativo não fará nada com o composer.json se você tiver um em seu projeto PHP.</span><span class="sxs-lookup"><span data-stu-id="8e847-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="8e847-200">Se você usar [Git implantação](app-service-deploy-local-git.md), você pode habilitar composer.json processamento durante `git push` habilitando a extensão do criador de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e847-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="8e847-201">Você pode [votar para obter o suporte de primeira classe do Criador no Serviço de Aplicativo aqui](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip).</span><span class="sxs-lookup"><span data-stu-id="8e847-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="8e847-202">No seu PHP web folha do aplicativo no hello [portal do Azure](https://portal.azure.com), clique em **ferramentas** > **extensões**.</span><span class="sxs-lookup"><span data-stu-id="8e847-202">In your PHP web app's blade in hello [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Tooenable de folha de configurações de Portal do Azure automação criador no Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="8e847-204">Clique em **Adicionar** e em **Criador**.</span><span class="sxs-lookup"><span data-stu-id="8e847-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Adicionar a automação do criador extensão tooenable criador no Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="8e847-206">Clique em **Okey** tooaccept os termos legais.</span><span class="sxs-lookup"><span data-stu-id="8e847-206">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="8e847-207">Clique em **Okey** extensão de saudação tooadd novamente.</span><span class="sxs-lookup"><span data-stu-id="8e847-207">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="8e847-208">Olá **extensões instaladas** folha agora mostrará a extensão do criador de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e847-208">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="8e847-209">![Aceitar a automação de criador termos legais tooenable no Azure](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="8e847-209">![Accept legal terms tooenable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="8e847-210">Agora, execute `git add`, `git commit`, e `git push` , como na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="8e847-210">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="8e847-211">Agora, você verá que o Compositor está instalando dependências definidas no composer.json.</span><span class="sxs-lookup"><span data-stu-id="8e847-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Implantação do Git com a automação do Criador no Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="8e847-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8e847-213">Next steps</span></span>
<span data-ttu-id="8e847-214">Para obter mais informações, consulte Olá [Centro de desenvolvedores PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="8e847-214">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="8e847-215">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e847-215">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8e847-216">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="8e847-216">No credit cards required; no commitments.</span></span>
> 
> 

[avaliação gratuita]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo ()]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[Lista de diretrizes de php. ini]: http://www.php.net/manual/en/ini.list.php
[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
[http://windows.php.net/download/]: http://windows.php.net/download/
[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

