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
# <a name="how-toocreate-php-web-and-worker-roles"></a>Como as funções de web e de trabalho PHP toocreate
## <a name="overview"></a>Visão geral
Este guia mostrará como toocreate PHP web ou trabalho funções em um ambiente de desenvolvimento do Windows, escolher uma versão específica do PHP hello "internas" versões disponíveis, alterar a configuração de PHP hello, habilitar extensões e por fim, implantar tooAzure. Ele também descreve como tooconfigure toouse uma função web ou de trabalho um tempo de execução do PHP (com configuração personalizada e extensões) que você fornecer.

## <a name="what-are-php-web-and-worker-roles"></a>O que são funções Web e de Trabalho do PHP?
O Azure fornece três modelos de computação para a execução de aplicativos: Serviço de Aplicativo do Azure, Máquinas Virtuais do Azure e Serviços de Nuvem do Azure. Todos os três modelos oferecem suporte ao PHP. Os Serviços de Nuvem, que incluem as funções Web e de trabalho, fornecem a *PaaS (plataforma como serviço)*. Em um serviço de nuvem, uma função web fornece uma web dedicado do Internet Information Services (IIS) aplicativos web front-end do servidor toohost. Uma função de trabalho pode executar tarefas assíncronas, de execução longa ou perpétuas, independentemente da interação do usuário ou da entrada.

Para obter mais informações sobre essas opções, consulte [Opções de hospedagem de computação fornecidas pelo Azure](cloud-services/cloud-services-choose-me.md).

## <a name="download-hello-azure-sdk-for-php"></a>Baixar hello Azure SDK para PHP
Olá [Azure SDK para PHP] consiste em vários componentes. Este artigo usará duas delas: PowerShell do Azure e Olá emuladores do Azure. Esses dois componentes podem ser instalados via Olá Microsoft Web Platform Installer. Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

## <a name="create-a-cloud-services-project"></a>Criar um projeto de Serviço de Nuvem
Olá primeira etapa na criação de uma função web ou de trabalho do PHP é toocreate um projeto de serviço do Azure. um projeto de serviço do Azure funciona como um contêiner lógico para funções da web e de trabalho, e ele contém do projeto Olá [(. csdef) de definição de serviço] e [a configuração de serviço (. cscfg)] arquivos.

toocreate um novo projeto de serviço do Azure, execute o Azure PowerShell como administrador e execute Olá comando a seguir:

    PS C:\>New-AzureServiceProject myProject

Este comando cria um novo diretório (`myProject`) toowhich, você pode adicionar funções web e de trabalho.

## <a name="add-php-web-or-worker-roles"></a>Adicionar funções de trabalho ou Web PHP
tooadd um projeto de tooa de função de web PHP, executar Olá comando dentro do diretório raiz do projeto Olá a seguir:

    PS C:\myProject> Add-AzurePHPWebRole roleName

Para uma função de trabalho, use este comando:

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> Olá `roleName` parâmetro é opcional. Se ele for omitido, o nome de função hello será gerado automaticamente. função da web primeiro Olá criada será `WebRole1`, Olá segundo será `WebRole2`, e assim por diante. Olá primeira função de trabalho criada será `WorkerRole1`, Olá segundo será `WorkerRole2`, e assim por diante.
>
>

## <a name="specify-hello-built-in-php-version"></a>Especificar versão do PHP interno Olá
Quando você adicionar um projeto PHP web ou de trabalho função tooa, arquivos de configuração do projeto Olá são modificados para que o PHP será instalado em cada instância de web ou de trabalho do seu aplicativo quando ele é implantado. versão de hello toosee do PHP que será instalado por padrão, execute Olá comando a seguir:

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

Olá a saída do comando de saudação acima será semelhante toowhat é mostrado abaixo. Neste exemplo, Olá `IsDefault` sinalizador é definido muito`true` para PHP 5.3.17, indicando que ele seja versão do PHP padrão Olá instalado.

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

Você pode definir Olá PHP runtime versão tooany de versões do PHP Olá listados. Por exemplo, tooset Olá PHP versão (para uma função com o nome da saudação `roleName`) too5.4.0, use Olá comando a seguir:

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> Versões do PHP disponíveis podem ser alterados no hello futuras.
>
>

## <a name="customize-hello-built-in-php-runtime"></a>Personalizar o tempo de execução do PHP interno Olá
Você tem controle total sobre a configuração do tempo de execução do PHP Olá que é instalada quando você seguir as etapas de saudação acima, incluindo a modificação de saudação `php.ini` configurações e a habilitação de extensões.

toocustomize Olá interno em tempo de execução do PHP, siga estas etapas:

1. Adicionar uma nova pasta chamada `php`, toohello `bin` diretório de sua função web. Para uma função de trabalho, adicione-o diretório raiz de toohello da função.
2. Em Olá `php` pasta, crie outra pasta chamada `ext`. Colocar qualquer `.dll` arquivos de extensão (por exemplo, `php_mongo.dll`) que você deseja tooenable nessa pasta.
3. Adicionar um `php.ini` arquivo toohello `php` pasta. Habilite todas as extensões personalizadas e defina todas as diretivas do PHP nesse arquivo. Por exemplo, se você quisesse tooturn `display_errors` em e habilitar Olá `php_mongo.dll` extensão, o conteúdo de saudação do seu `php.ini` arquivo seria o seguinte:

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> Todas as configurações que você não definir explicitamente Olá `php.ini` arquivo que você fornecer serão automaticamente ser definido como tootheir os valores padrão. No entanto, lembre-se de que você pode adicionar um arquivo `php.ini` completo.
>
>

## <a name="use-your-own-php-runtime"></a>Usar seu próprio tempo de execução PHP
Em alguns casos, em vez de selecionar um tempo de execução do PHP interno e configurá-lo, conforme descrito acima, convém tooprovide seu próprio tempo de execução do PHP. Por exemplo, você pode usar Olá mesmo tempo de execução do PHP em uma função web ou de trabalho que você usa em seu ambiente de desenvolvimento. Isso torna mais fácil tooensure aplicativo hello não alterará o comportamento em seu ambiente de produção.

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a>Configurar um toouse de função da web em seu próprio tempo de execução do PHP
tooconfigure uma função de web toouse um tempo de execução do PHP que você fornecer, siga estas etapas:

1. Crie um projeto de Serviço do Azure e adicione uma função Web do PHP conforme descrito anteriormente neste tópico.
2. Criar um `php` pasta Olá `bin` pasta que está no diretório raiz da sua função web e, em seguida, adicionar toohello de tempo de execução (todos os binários, arquivos de configuração, as subpastas, etc.) o PHP `php` pasta.
3. (OPCIONAL) Se o tempo de execução do PHP usa Olá [Drivers da Microsoft para PHP para SQL Server][sqlsrv drivers], você precisará tooconfigure seu tooinstall de função web [SQL Server Native Client 2012] [ sql native client] quando ela é provisionada. toodo isso, adicione Olá [sqlncli.msi x64 instalador] toohello `bin` pasta no diretório raiz da sua função web. script de inicialização de saudação descrito na próxima etapa do hello silenciosamente executará instalador hello quando a função hello é provisionada. Se o tempo de execução do PHP não usar Olá Drivers da Microsoft para PHP para SQL Server, você pode remover Olá seguinte linha do script hello mostrado na próxima etapa do hello:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Definir uma tarefa de inicialização que configura [serviços de informações da Internet (IIS)] [ iis.net] toouse sua toohandle de tempo de execução do PHP as solicitações de `.php` páginas. toodo hello, abra `setup_web.cmd` arquivo (em Olá `bin` arquivo da pasta raiz da sua função web) em um editor de texto e substituir seu conteúdo com hello script a seguir:

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
5. Adicione o diretório raiz do aplicativo arquivos tooyour web da sua função. Esse será o diretório raiz do servidor da web hello.
6. Publicar seu aplicativo conforme descrito em Olá [publicar seu aplicativo](#publish-your-application) seção abaixo.

> [!NOTE]
> Olá `download.ps1` script (em Olá `bin` pasta Olá web da raiz do diretório da função) podem ser excluídos após as etapas de saudação descritas acima para usar seu próprio tempo de execução do PHP.
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a>Configurar um toouse de função de trabalho em seu próprio tempo de execução do PHP
tooconfigure uma função de trabalho toouse um tempo de execução do PHP que você fornecer, siga estas etapas:

1. Crie um projeto de Serviço do Azure e adicione uma função de trabalho do PHP conforme descrito anteriormente neste tópico.
2. Criar um `php` pasta no diretório de raiz da função de trabalho Olá e, em seguida, adicione toohello de tempo de execução (todos os binários, arquivos de configuração, as subpastas, etc.) o PHP `php` pasta.
3. (OPCIONAL) Se o tempo de execução do PHP usa [Drivers da Microsoft para PHP para SQL Server][sqlsrv drivers], você precisará tooconfigure seu tooinstall da função de trabalho [SQL Server Native Client 2012] [ sql native client] quando ela é provisionada. toodo isso, adicione Olá [sqlncli.msi x64 instalador] diretório de raiz da função de trabalho toohello. script de inicialização de saudação descrito na próxima etapa do hello silenciosamente executará instalador hello quando a função hello é provisionada. Se o tempo de execução do PHP não usar Olá Drivers da Microsoft para PHP para SQL Server, você pode remover Olá seguinte linha do script hello mostrado na próxima etapa do hello:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Definir uma tarefa de inicialização que adiciona o `php.exe` variável de ambiente do caminho da função de trabalho executável toohello quando a função hello é provisionada. toodo isso, abra Olá `setup_worker.cmd` (no diretório de raiz da função de trabalho Olá) em um editor de texto e substitua o seu conteúdo com hello script a seguir:

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
5. Adicione o diretório raiz do seu aplicativo arquivos tooyour da função de trabalho.
6. Publicar seu aplicativo conforme descrito em Olá [publicar seu aplicativo](#publish-your-application) seção abaixo.

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a>Executar o aplicativo no hello emuladores de computação e armazenamento
Olá, emuladores do Azure fornecem um ambiente local em que você pode testar seu aplicativo do Azure antes de implantá-lo toohello nuvem. Há algumas diferenças entre os emuladores de saudação e hello ambiente do Azure. toounderstand isso melhor, consulte [usar o emulador de armazenamento do Azure Olá para desenvolvimento e teste](storage/common/storage-use-emulator.md).

Observe que você deve ter o PHP instalado localmente emulador de computação toouse hello. o emulador de computação Olá usará em seu local toorun de instalação do PHP seu aplicativo.

toorun seu projeto no emuladores hello, execute Olá seguinte comando do diretório raiz do projeto:

    PS C:\MyProject> Start-AzureEmulator

Você verá toothis semelhante de saída:

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

Você pode ver o aplicativo em execução no emulador Olá abrindo um navegador da web e navegação toohello endereço local mostrado na saída de hello (`http://127.0.0.1:81` na saída de exemplo hello acima).

emuladores de saudação toostop, execute este comando:

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a>Publicar seu aplicativo
toopublish seu aplicativo, é necessário importar toofirst suas configurações de publicação usando Olá [AzurePublishSettingsFile de importação](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet. Em seguida, você pode publicar seu aplicativo usando Olá [AzureServiceProject publicar](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet. Para obter informações sobre como entrar em, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá [Centro de desenvolvedores PHP](/develop/php/).

[Azure SDK para PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[(. csdef) de definição de serviço]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[a configuração de serviço (. cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 instalador]: http://go.microsoft.com/fwlink/?LinkID=239648
