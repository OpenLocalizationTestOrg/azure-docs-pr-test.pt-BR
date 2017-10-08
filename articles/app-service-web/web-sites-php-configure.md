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
# <a name="configure-php-in-azure-app-service-web-apps"></a>Configurar o PHP em aplicativos Web do Serviço de Aplicativo do Azure
## <a name="introduction"></a>Introdução
Este guia mostrará como tooconfigure Olá interno em tempo de execução do PHP para aplicativos Web no [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714), forneça um tempo de execução do PHP personalizado e habilitar extensões. toouse do serviço de aplicativo, inscreva-se para Olá [avaliação gratuita]. Olá tooget mais deste guia, você deve primeiro criar um aplicativo web do PHP no serviço de aplicativo.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a>Como: versão do PHP alteração Olá interno
Por padrão, quando você cria um aplicativo Web do Serviço de Aplicativo, o PHP 5.5 é instalado e fica imediatamente disponível para uso. Olá melhor maneira toosee Olá disponível revisão, sua configuração padrão, e extensões habilitadas hello é toodeploy um script que chama Olá [phpinfo ()] função.

As versões 5.6 e 7.0 do PHP também estão disponíveis, mas não são habilitadas por padrão. Olá tooupdate versão do PHP, siga um destes métodos:

### <a name="azure-portal"></a>Portal do Azure
1. Procurar o aplicativo web de tooyour Olá [Portal do Azure](https://portal.azure.com) e clique em Olá **configurações** botão.
   
    ![Configurações do aplicativo Web][settings-button]
2. De saudação **configurações** selecione folha **configurações de aplicativo** e escolha a nova versão do PHP hello.
   
    ![Configurações do aplicativo][application-settings]
3. Clique em Olá **salvar** botão na parte superior de saudação do hello **configurações de aplicativo da Web** folha.
   
    ![Salvar definições de configuração][save-button]

### <a name="azure-powershell-windows"></a>PowerShell do Azure (Windows)
1. Abra o PowerShell do Azure e a conta de logon do tooyour:
   
        PS C:\> Login-AzureRmAccount
2. Defina a versão do PHP Olá para o aplicativo web de saudação.
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. versão do PHP Olá agora está definido. Você pode confirmar essas configurações:
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a>Interface de linha de comando do Azure (Linux, Mac, Windows)
toouse Olá Interface de linha de comando do Azure, você deve ter **Node.js** instalado em seu computador.

1. Abra o Terminal e conta de logon do tooyour.
   
        azure login
2. Defina a versão do PHP Olá para o aplicativo web de saudação.
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. versão do PHP Olá agora está definido. Você pode confirmar essas configurações:
   
        azure site show {app-name}

> [!NOTE] 
> Olá [2.0 do CLI do Azure](https://github.com/Azure/azure-cli) comandos são equivalente toohello acima são:
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a>Como: alterar as configurações de PHP internas Olá
Para qualquer tempo de execução do PHP interno, você pode alterar qualquer uma das opções de configuração de saudação seguindo as etapas de saudação abaixo. (Para obter informações sobre diretrizes de php. ini, consulte [Lista de diretrizes de php. ini].)

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a>Alterando as configurações de PHP\_INI\_USER, PHP\_INI\_PERDIR e PHP\_INI\_ALL
1. Adicionar um [. user.ini] diretório raiz do arquivo tooyour.
2. Adicionar configuração configurações toohello `.user.ini` arquivo usando Olá a mesma sintaxe que você usaria em um `php.ini` arquivo. Por exemplo, se você quisesse Olá tooturn `display_errors` configuração e defina `upload_max_filesize` configuração too10M, o `.user.ini` arquivo deve conter este texto:
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. Implante seu aplicativo Web.
4. Reinicie o aplicativo da web de saudação. (Reinicialização é necessária porque frequência Olá com o PHP lê `.user.ini` arquivos é controlado por Olá `user_ini.cache_ttl` configuração, que é uma configuração de nível de sistema e é de 300 segundos (5 minutos) por padrão. Reiniciar aplicativo web de saudação força PHP tooread Olá novas configurações na Olá `.user.ini` arquivo.)

Como uma alternativa toousing um `.user.ini` arquivo, você pode usar o hello [ini_set()] função nas opções de configuração de tooset de scripts que não são diretivas de nível de sistema.

### <a name="changing-phpinisystem-configuration-settings"></a>Alterando as configurações de PHP\_INI\_SYSTEM
1. Adicionar um tooyour de configuração do aplicativo Web App com chave Olá `PHP_INI_SCAN_DIR` e valor`d:\home\site\ini`
2. Criar um `settings.ini` arquivo usando o Console do Kudu (http://&lt;nome do site&gt;. scm.azurewebsite.net) no hello `d:\home\site\ini` directory.
3. Adicionar configuração configurações toohello `settings.ini` arquivo usando Olá a mesma sintaxe que você usaria em um arquivo php.ini. Por exemplo, se você quisesse Olá toopoint `curl.cainfo` configuração tooa `*.crt` arquivo e defina 'wincache.maxfilesize' configuração too512K, o `settings.ini` arquivo deve conter este texto:
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. Reinicie as alterações do aplicativo Web tooload hello.

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a>Como: habilitar extensões em tempo de execução do PHP saudação padrão
Conforme observado na seção anterior hello, Olá melhor maneira toosee Olá versão padrão do PHP, sua configuração padrão e Olá habilitado extensões é toodeploy um script que chama [phpinfo ()]. extensões adicionais de tooenable, siga as etapas de saudação abaixo:

### <a name="configure-via-ini-settings"></a>Configurar por meio de configurações ini
1. Adicionar um `ext` toohello diretório `d:\home\site` directory.
2. Colocar `.dll` arquivos de extensão no hello `ext` diretório (por exemplo, `php_xdebug.dll`). Certifique-se de que as extensões de hello são compatíveis com a versão padrão do PHP e são VC9 e compatível com o non-thread-safe (ntes).
3. Adicionar um tooyour de configuração do aplicativo Web App com chave Olá `PHP_INI_SCAN_DIR` e valor`d:\home\site\ini`
4. Crie um arquivo `ini` em `d:\home\site\ini` chamado `extensions.ini`.
5. Adicionar configuração configurações toohello `extensions.ini` arquivo usando Olá a mesma sintaxe que você usaria em um arquivo php.ini. Por exemplo, se você quisesse tooenable Olá MongoDB e XDebug extensões, seu `extensions.ini` arquivo deve conter este texto:
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. Reinicie as alterações do aplicativo Web tooload hello.

### <a name="configure-via-app-setting"></a>Configurar por meio de Configuração de Aplicativo
1. Adicionar um `bin` diretório raiz do diretório toohello.
2. Colocar `.dll` arquivos de extensão no hello `bin` diretório (por exemplo, `php_xdebug.dll`). Certifique-se de que as extensões de hello são compatíveis com a versão padrão do PHP e são VC9 e compatível com o non-thread-safe (ntes).
3. Implante seu aplicativo Web.
4. Procurar o aplicativo web de tooyour Olá Portal do Azure e clique em Olá **configurações** botão.
   
    ![Configurações do aplicativo Web][settings-button]
5. De saudação **configurações** selecione folha **configurações do aplicativo** e role toohello **configurações do aplicativo** seção.
6. Em Olá **configurações do aplicativo** seção, crie um **PHP_EXTENSIONS** chave. valor de saudação para essa chave seria uma raiz do caminho relativo toowebsite: **bin\your-ext-arquivo**.
   
    ![Habilitar extensões em configurações do aplicativo][php-extensions]
7. Clique em Olá **salvar** botão na parte superior de saudação do hello **configurações de aplicativo da Web** folha.
   
    ![Salvar definições de configuração][save-button]

Também há suporte para extensões Zend usando uma chave **PHP_ZENDEXTENSIONS**. tooenable várias extensões, incluir uma lista separada por vírgulas de `.dll` arquivos para o valor de configuração de aplicativo hello.

## <a name="how-to-use-a-custom-php-runtime"></a>Como: usar um tempo de execução personalizado do PHP
Em vez de tempo de execução de saudação padrão PHP, aplicativos de Web do serviço de aplicativo pode usar um tempo de execução do PHP que você forneça tooexecute scripts PHP. Olá em tempo de execução que você fornece pode ser configurado por um `php.ini` arquivo que você fornecer também. toouse um tempo de execução do PHP personalizado com aplicativos da Web, siga as etapas de saudação abaixo.

1. Obtenha uma versão do PHP ou VC11 para Windows que seja não thread safe e compatível com a versão VC9. Versões recentes do PHP para Windows podem ser encontradas aqui: [http://windows.php.net/download/]. Versões mais antigas podem ser encontrados no arquivo de saudação aqui: [http://windows.php.net/downloads/releases/archives/].
2. Modificar Olá `php.ini` arquivo para o tempo de execução. Observe que quaisquer definições de configuração que forem diretrizes exclusivamente de nível de sistema serão ignoradas por Aplicativos Web. (Para informações sobre diretrizes de nível de sistema apenas, consulte [Lista de diretrizes de php. ini].)
3. Opcionalmente, adicione o tempo de execução do PHP extensões tooyour e habilitá-las no hello `php.ini` arquivo.
4. Adicionar um `bin` diretório raiz do diretório tooyour e diretório de saudação put que contém o tempo de execução do PHP nele (por exemplo, `bin\php`).
5. Implante seu aplicativo Web.
6. Procurar o aplicativo web de tooyour Olá Portal do Azure e clique em Olá **configurações** botão.
   
    ![Configurações do aplicativo Web][settings-button]
7. De saudação **configurações** selecione folha **configurações do aplicativo** e role toohello **mapeamentos de manipulador** seção. Adicionar `*.php` toohello extensão de campo e adicionar Olá caminho toohello `php-cgi.exe` executável. Se você colocar o tempo de execução do PHP no hello `bin` diretório na raiz de saudação do seu aplicativo, o caminho de saudação será `D:\home\site\wwwroot\bin\php\php-cgi.exe`.
   
    ![Especificar o manipulador em mapeamentos de manipulador][handler-mappings]
8. Clique em Olá **salvar** botão na parte superior de saudação do hello **configurações de aplicativo da Web** folha.
   
    ![Salvar definições de configuração][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a>Como habilitar a automação do Criador no Azure
Por padrão, o Serviço de Aplicativo não fará nada com o composer.json se você tiver um em seu projeto PHP. Se você usar [Git implantação](app-service-deploy-local-git.md), você pode habilitar composer.json processamento durante `git push` habilitando a extensão do criador de saudação.

> [!NOTE]
> Você pode [votar para obter o suporte de primeira classe do Criador no Serviço de Aplicativo aqui](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip).
> 
> 

1. No seu PHP web folha do aplicativo no hello [portal do Azure](https://portal.azure.com), clique em **ferramentas** > **extensões**.
   
    ![Tooenable de folha de configurações de Portal do Azure automação criador no Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. Clique em **Adicionar** e em **Criador**.
   
    ![Adicionar a automação do criador extensão tooenable criador no Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. Clique em **Okey** tooaccept os termos legais. Clique em **Okey** extensão de saudação tooadd novamente.
   
    Olá **extensões instaladas** folha agora mostrará a extensão do criador de saudação.  
    ![Aceitar a automação de criador termos legais tooenable no Azure](./media/web-sites-php-configure/composer-extension-view.png)
4. Agora, execute `git add`, `git commit`, e `git push` , como na seção anterior hello. Agora, você verá que o Compositor está instalando dependências definidas no composer.json.
   
    ![Implantação do Git com a automação do Criador no Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá [Centro de desenvolvedores PHP](/develop/php/).

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
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

