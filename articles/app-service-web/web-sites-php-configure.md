---
title: "Configurar o PHP em Aplicativos Web do Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Saiba como configurar a instalação padrão do PHP ou adicione uma instalação de PHP personalizada para aplicativos Web no Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: 624dd416f37aacdb3d2f6e59afdc2efe646e610b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="bfe4b-103">Configurar o PHP em aplicativos Web do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="bfe4b-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="bfe4b-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="bfe4b-104">Introduction</span></span>
<span data-ttu-id="bfe4b-105">Este guia mostrará como configurar o tempo de execução do PHP interno para aplicativos Web no [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714), fornecer um tempo de execução personalizado do PHP e habilitar extensões.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-105">This guide will show you how to configure the built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="bfe4b-106">Para usar o Serviço de Aplicativo, inscreva-se para a [avaliação gratuita].</span><span class="sxs-lookup"><span data-stu-id="bfe4b-106">To use App Service, sign up for the [free trial].</span></span> <span data-ttu-id="bfe4b-107">Para aproveitar ao máximo este guia, você deve primeiro criar um aplicativo Web do PHP no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-107">To get the most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-the-built-in-php-version"></a><span data-ttu-id="bfe4b-108">Como: alterar a versão interna do PHP</span><span class="sxs-lookup"><span data-stu-id="bfe4b-108">How to: Change the built-in PHP version</span></span>
<span data-ttu-id="bfe4b-109">Por padrão, quando você cria um aplicativo Web do Serviço de Aplicativo, o PHP 5.5 é instalado e fica imediatamente disponível para uso.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="bfe4b-110">A melhor forma de visualizar a revisão da versão, sua configuração padrão e as extensões habilitadas é implantar um script que chame a função [phpinfo()] .</span><span class="sxs-lookup"><span data-stu-id="bfe4b-110">The best way to see the available release revision, its default configuration, and the enabled extensions is to deploy a script that calls the [phpinfo()] function.</span></span>

<span data-ttu-id="bfe4b-111">As versões 5.6 e 7.0 do PHP também estão disponíveis, mas não são habilitadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="bfe4b-112">Para atualizar a versão do PHP, execute um destes métodos:</span><span class="sxs-lookup"><span data-stu-id="bfe4b-112">To update the PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="bfe4b-113">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bfe4b-113">Azure Portal</span></span>
1. <span data-ttu-id="bfe4b-114">Navegue até seu aplicativo Web no [Portal do Azure](https://portal.azure.com) e clique no botão **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="bfe4b-114">Browse to your web app in the [Azure Portal](https://portal.azure.com) and click on the **Settings** button.</span></span>
   
    ![Configurações do aplicativo Web][settings-button]
2. <span data-ttu-id="bfe4b-116">Na folha **Configurações**, selecione **Configurações do aplicativo** e escolha a nova versão do PHP.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-116">From the **Settings** blade select **Application Settings** and choose the new PHP version.</span></span>
   
    ![Configurações do aplicativo][application-settings]
3. <span data-ttu-id="bfe4b-118">Clique no botão **Salvar** na parte superior da folha **Configurações do aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-118">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Salvar definições de configuração][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="bfe4b-120">PowerShell do Azure (Windows)</span><span class="sxs-lookup"><span data-stu-id="bfe4b-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="bfe4b-121">Abra o Azure PowerShell e faça logon em sua conta:</span><span class="sxs-lookup"><span data-stu-id="bfe4b-121">Open Azure PowerShell, and login to your account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="bfe4b-122">Defina a versão PHP do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-122">Set the PHP version for the web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="bfe4b-123">A versão do PHP agora está definida.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-123">The PHP version is now set.</span></span> <span data-ttu-id="bfe4b-124">Você pode confirmar essas configurações:</span><span class="sxs-lookup"><span data-stu-id="bfe4b-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="bfe4b-125">Interface de linha de comando do Azure (Linux, Mac, Windows)</span><span class="sxs-lookup"><span data-stu-id="bfe4b-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="bfe4b-126">Para usar a Interface de Linha de Comando do Azure, é necessário ter **Node.js** instalado no computador.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-126">To use the Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="bfe4b-127">Abra o Terminal e faça logon em sua conta.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-127">Open Terminal, and login to your account.</span></span>
   
        azure login
2. <span data-ttu-id="bfe4b-128">Defina a versão PHP do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-128">Set the PHP version for the web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="bfe4b-129">A versão do PHP agora está definida.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-129">The PHP version is now set.</span></span> <span data-ttu-id="bfe4b-130">Você pode confirmar essas configurações:</span><span class="sxs-lookup"><span data-stu-id="bfe4b-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="bfe4b-131">Os comandos da [CLI 2.0 do Azure](https://github.com/Azure/azure-cli) equivalentes aos mencionados acima são:</span><span class="sxs-lookup"><span data-stu-id="bfe4b-131">The [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent to the above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-the-built-in-php-configurations"></a><span data-ttu-id="bfe4b-132">Como: alterar as configurações internas do PHP</span><span class="sxs-lookup"><span data-stu-id="bfe4b-132">How to: Change the built-in PHP configurations</span></span>
<span data-ttu-id="bfe4b-133">Para qualquer tempo de execução interno do PHP, é possível alterar qualquer uma das opções de configuração seguindo as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-133">For any built-in PHP runtime, you can change any of the configuration options by following the steps below.</span></span> <span data-ttu-id="bfe4b-134">(Para obter informações sobre diretrizes de php. ini, consulte [Lista de diretrizes de php. ini].)</span><span class="sxs-lookup"><span data-stu-id="bfe4b-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="bfe4b-135">Alterando as configurações de PHP\_INI\_USER, PHP\_INI\_PERDIR e PHP\_INI\_ALL</span><span class="sxs-lookup"><span data-stu-id="bfe4b-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="bfe4b-136">Adicione um arquivo [.user.ini] no seu diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-136">Add a [.user.ini] file to your root directory.</span></span>
2. <span data-ttu-id="bfe4b-137">Adicione as definições de configuração ao arquivo `.user.ini` usando a mesma sintaxe que você usaria em um arquivo `php.ini`.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-137">Add configuration settings to the `.user.ini` file using the same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="bfe4b-138">Por exemplo, se você quisesse ativar a configuração `display_errors` e definir a configuração `upload_max_filesize` como 10 M, o arquivo `.user.ini` conteria este texto:</span><span class="sxs-lookup"><span data-stu-id="bfe4b-138">For example, if you wanted to turn the `display_errors` setting on and set `upload_max_filesize` setting to 10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on to write errors to d:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="bfe4b-139">Implante seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-139">Deploy your web app.</span></span>
4. <span data-ttu-id="bfe4b-140">Reinicie o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-140">Restart the web app.</span></span> <span data-ttu-id="bfe4b-141">(É necessário reiniciar, pois a frequência com a qual o PHP lê arquivos `.user.ini` é regida pela configuração`user_ini.cache_ttl`, que é uma configuração de nível de sistema e é, por padrão, 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="bfe4b-141">(Restarting is necessary because the frequency with which PHP reads `.user.ini` files is governed by the `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="bfe4b-142">Reiniciar o aplicativo Web força o PHP a ler as novas configurações no arquivo `.user.ini` ).</span><span class="sxs-lookup"><span data-stu-id="bfe4b-142">Restarting the web app forces PHP to read the new settings in the `.user.ini` file.)</span></span>

<span data-ttu-id="bfe4b-143">Uma alternativa ao uso de um arquivo `.user.ini` é usar a função [ini_set()] em scripts para definir opções de configuração que não sejam diretrizes de nível de sistema.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-143">As an alternative to using a `.user.ini` file, you can use the [ini_set()] function in scripts to set configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="bfe4b-144">Alterando as configurações de PHP\_INI\_SYSTEM</span><span class="sxs-lookup"><span data-stu-id="bfe4b-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="bfe4b-145">Adicionar uma Configuração de Aplicativo a seu aplicativo Web com a chave `PHP_INI_SCAN_DIR` e o valor `d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="bfe4b-145">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="bfe4b-146">Crie um arquivo `settings.ini` usando o console Kudu (http://&lt;nome-do-site&gt;.scm.azurewebsite.net) no diretório `d:\home\site\ini`.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in the `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="bfe4b-147">Adicione as definições de configuração ao arquivo `settings.ini` usando a mesma sintaxe que você usaria em um arquivo php.ini.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-147">Add configuration settings to the `settings.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="bfe4b-148">Por exemplo, se você quisesse apontar a configuração `curl.cainfo` para um arquivo `*.crt` e definir a configuração 'wincache.maxfilesize' como 512 K, o arquivo `settings.ini` conteria este texto:</span><span class="sxs-lookup"><span data-stu-id="bfe4b-148">For example, if you wanted to point the `curl.cainfo` setting to a `*.crt` file and set 'wincache.maxfilesize' setting to 512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="bfe4b-149">Reinicie seu aplicativo Web para carregar as alterações.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-149">Restart your Web App to load the changes.</span></span>

## <a name="how-to-enable-extensions-in-the-default-php-runtime"></a><span data-ttu-id="bfe4b-150">Como: habilitar extensões no tempo de execução padrão do PHP</span><span class="sxs-lookup"><span data-stu-id="bfe4b-150">How to: Enable extensions in the default PHP runtime</span></span>
<span data-ttu-id="bfe4b-151">Conforme indicado na seção anterior, a melhor forma de visualizar a versão padrão do PHP, sua configuração padrão e as extensões habilitadas é implantar um script que chame [phpinfo()].</span><span class="sxs-lookup"><span data-stu-id="bfe4b-151">As noted in the previous section, the best way to see the default PHP version, its default configuration, and the enabled extensions is to deploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="bfe4b-152">Para habilitar extensões adicionais, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="bfe4b-152">To enable additional extensions, follow the steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="bfe4b-153">Configurar por meio de configurações ini</span><span class="sxs-lookup"><span data-stu-id="bfe4b-153">Configure via ini settings</span></span>
1. <span data-ttu-id="bfe4b-154">Adicione um diretório `ext` ao diretório `d:\home\site`.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-154">Add a `ext` directory to the `d:\home\site` directory.</span></span>
2. <span data-ttu-id="bfe4b-155">Coloque arquivos de extensão `.dll` no diretório `ext` (por exemplo, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="bfe4b-155">Put `.dll` extension files in the `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="bfe4b-156">Certifique-se de que as extensões sejam compatíveis com a versão padrão do PHP e também com nts (non-thread-safe) e VC9.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-156">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="bfe4b-157">Adicionar uma Configuração de Aplicativo a seu aplicativo Web com a chave `PHP_INI_SCAN_DIR` e o valor `d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="bfe4b-157">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="bfe4b-158">Crie um arquivo `ini` em `d:\home\site\ini` chamado `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="bfe4b-159">Adicione as definições de configuração ao arquivo `extensions.ini` usando a mesma sintaxe que você usaria em um arquivo php.ini.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-159">Add configuration settings to the `extensions.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="bfe4b-160">Por exemplo, se você desejasse habilitar as extensões MongoDB e XDebug, o arquivo `extensions.ini` conteria este texto:</span><span class="sxs-lookup"><span data-stu-id="bfe4b-160">For example, if you wanted to enable the MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="bfe4b-161">Reinicie seu aplicativo Web para carregar as alterações.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-161">Restart your Web App to load the changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="bfe4b-162">Configurar por meio de Configuração de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="bfe4b-162">Configure via App Setting</span></span>
1. <span data-ttu-id="bfe4b-163">Adicione um diretório `bin` ao diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-163">Add a `bin` directory to the root directory.</span></span>
2. <span data-ttu-id="bfe4b-164">Coloque arquivos de extensão `.dll` no diretório `bin` (por exemplo, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="bfe4b-164">Put `.dll` extension files in the `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="bfe4b-165">Certifique-se de que as extensões sejam compatíveis com a versão padrão do PHP e também com nts (non-thread-safe) e VC9.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-165">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="bfe4b-166">Implante seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-166">Deploy your web app.</span></span>
4. <span data-ttu-id="bfe4b-167">Navegue até o aplicativo Web no Portal do Azure e clique no botão **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="bfe4b-167">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Configurações do aplicativo Web][settings-button]
5. <span data-ttu-id="bfe4b-169">Na folha **Configurações**, selecione **Configurações do Aplicativo** e role até a seção **Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-169">From the **Settings** blade select **Application Settings** and scroll to the **App settings** section.</span></span>
6. <span data-ttu-id="bfe4b-170">Na seção **Configurações do aplicativo**, crie uma chave **PHP_EXTENSIONS**.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-170">In the **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="bfe4b-171">O valor para essa chave seria um caminho relativo à raiz do site: **bin\seu-arquivo-de-ext**.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-171">The value for this key would be a path relative to website root: **bin\your-ext-file**.</span></span>
   
    ![Habilitar extensões em configurações do aplicativo][php-extensions]
7. <span data-ttu-id="bfe4b-173">Clique no botão **Salvar** na parte superior da folha **Configurações do aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-173">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Salvar definições de configuração][save-button]

<span data-ttu-id="bfe4b-175">Também há suporte para extensões Zend usando uma chave **PHP_ZENDEXTENSIONS**.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="bfe4b-176">Para habilitar várias extensões, inclua uma lista de arquivos `.dll` separados por vírgulas para o valor de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-176">To enable multiple extensions, include a comma-separated list of `.dll` files for the app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="bfe4b-177">Como: usar um tempo de execução personalizado do PHP</span><span class="sxs-lookup"><span data-stu-id="bfe4b-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="bfe4b-178">Em vez do tempo de execução padrão do PHP, os aplicativos Web do Serviço de Aplicativo podem usar um tempo de execução de PHP fornecido por você para executar scripts PHP.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-178">Instead of the default PHP runtime, App Service Web Apps can use a PHP runtime that you provide to execute PHP scripts.</span></span> <span data-ttu-id="bfe4b-179">O tempo de execução que você fornece pode ser configurado por um arquivo `php.ini` também fornecido por você.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-179">The runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="bfe4b-180">Para usar um tempo de execução personalizado do PHP com aplicativos Web, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-180">To use a custom PHP runtime with Web Apps, follow the steps below.</span></span>

1. <span data-ttu-id="bfe4b-181">Obtenha uma versão do PHP ou VC11 para Windows que seja não thread safe e compatível com a versão VC9.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="bfe4b-182">Versões recentes do PHP para Windows podem ser encontradas aqui: [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="bfe4b-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="bfe4b-183">Versões mais antigas podem ser encontradas neste arquivo morto: [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="bfe4b-183">Older releases can be found in the archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="bfe4b-184">Modifique o arquivo `php.ini` para o seu tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-184">Modify the `php.ini` file for your runtime.</span></span> <span data-ttu-id="bfe4b-185">Observe que quaisquer definições de configuração que forem diretrizes exclusivamente de nível de sistema serão ignoradas por Aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="bfe4b-186">(Para informações sobre diretrizes de nível de sistema apenas, consulte [Lista de diretrizes de php. ini].)</span><span class="sxs-lookup"><span data-stu-id="bfe4b-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="bfe4b-187">Opcionalmente, adicione extensões para o seu tempo de execução do PHP e habilite-as no arquivo `php.ini` .</span><span class="sxs-lookup"><span data-stu-id="bfe4b-187">Optionally, add extensions to your PHP runtime and enable them in the `php.ini` file.</span></span>
4. <span data-ttu-id="bfe4b-188">Adicione o diretório `bin` ao seu diretório raiz e coloque lá o diretório que contém o seu tempo de execução do PHP (por exemplo, `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="bfe4b-188">Add a `bin` directory to your root directory, and put the directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="bfe4b-189">Implante seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-189">Deploy your web app.</span></span>
6. <span data-ttu-id="bfe4b-190">Navegue até o aplicativo Web no Portal do Azure e clique no botão **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="bfe4b-190">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Configurações do aplicativo Web][settings-button]
7. <span data-ttu-id="bfe4b-192">Na folha **Configurações**, selecione **Configurações do Aplicativo** e role até a seção **Mapeamentos de manipulador**.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-192">From the **Settings** blade select **Application Settings** and scroll to the **Handler mappings** section.</span></span> <span data-ttu-id="bfe4b-193">Adicione `*.php` ao campo Extensão e adicionar o caminho para o executável `php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-193">Add `*.php` to the Extension field and add the path to the `php-cgi.exe` executable.</span></span> <span data-ttu-id="bfe4b-194">Se você colocar seu tempo de execução do PHP no diretório `bin` na raiz do aplicativo, o caminho será `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-194">If you put your PHP runtime in the `bin` directory in the root of you application, the path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![Especificar o manipulador em mapeamentos de manipulador][handler-mappings]
8. <span data-ttu-id="bfe4b-196">Clique no botão **Salvar** na parte superior da folha **Configurações do aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-196">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Salvar definições de configuração][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="bfe4b-198">Como habilitar a automação do Criador no Azure</span><span class="sxs-lookup"><span data-stu-id="bfe4b-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="bfe4b-199">Por padrão, o Serviço de Aplicativo não fará nada com o composer.json se você tiver um em seu projeto PHP.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="bfe4b-200">Se você usar a [implantação Git](app-service-deploy-local-git.md), você poderá habilitar o composer.json durante o `git push` habilitando a extensão do Criador.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="bfe4b-201">Você pode [votar para obter o suporte de primeira classe do Criador no Serviço de Aplicativo aqui](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip).</span><span class="sxs-lookup"><span data-stu-id="bfe4b-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="bfe4b-202">Na folha do aplicativo Web PHP no [portal do Azure](https://portal.azure.com), clique em **Ferramentas** > **Extensões**.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-202">In your PHP web app's blade in the [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Folha de configurações do Portal do Azure para habilitar a automação do Criador no Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="bfe4b-204">Clique em **Adicionar** e em **Criador**.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Adicionar extensão do Criador para habilitar sua respectiva automação no Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="bfe4b-206">Clique em **OK** para aceitar os termos legais.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-206">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="bfe4b-207">Clique em **OK** novamente para adicionar a extensão.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-207">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="bfe4b-208">Agora, a folha **Extensões instaladas** mostrará a Extensão do criador.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-208">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="bfe4b-209">![Aceite os termos legais para habilitar a automação do Criador no Azure](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="bfe4b-209">![Accept legal terms to enable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="bfe4b-210">Agora, execute `git add`, `git commit` e `git push` como na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-210">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="bfe4b-211">Agora, você verá que o Compositor está instalando dependências definidas no composer.json.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Implantação do Git com a automação do Criador no Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="bfe4b-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bfe4b-213">Next steps</span></span>
<span data-ttu-id="bfe4b-214">Para obter mais informações, veja o [Centro de Desenvolvimento PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="bfe4b-214">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="bfe4b-215">Se você deseja começar a usar o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, vá até [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-215">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="bfe4b-216">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="bfe4b-216">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="bfe4b-217">[avaliação gratuita]: https://www.windowsazure.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="bfe4b-217">[free trial]: https://www.windowsazure.com/pricing/free-trial/</span></span>
<span data-ttu-id="bfe4b-218">[phpinfo()]: http://php.net/manual/en/function.phpinfo.php</span><span class="sxs-lookup"><span data-stu-id="bfe4b-218">[phpinfo()]: http://php.net/manual/en/function.phpinfo.php</span></span>
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
<span data-ttu-id="bfe4b-219">[Lista de diretrizes de php. ini]: http://www.php.net/manual/en/ini.list.php</span><span class="sxs-lookup"><span data-stu-id="bfe4b-219">[List of php.ini directives]: http://www.php.net/manual/en/ini.list.php</span></span>
<span data-ttu-id="bfe4b-220">[.user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span><span class="sxs-lookup"><span data-stu-id="bfe4b-220">[.user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span></span>
<span data-ttu-id="bfe4b-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span><span class="sxs-lookup"><span data-stu-id="bfe4b-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span></span>
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
<span data-ttu-id="bfe4b-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span><span class="sxs-lookup"><span data-stu-id="bfe4b-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span></span>
<span data-ttu-id="bfe4b-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span><span class="sxs-lookup"><span data-stu-id="bfe4b-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span></span>
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

