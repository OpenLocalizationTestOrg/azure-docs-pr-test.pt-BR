---
title: "aaaInstall .NET em funções de serviços de nuvem do Azure | Microsoft Docs"
description: "Este artigo descreve como toomanually instalar saudação do .NET Framework em suas funções web e de trabalho do serviço de nuvem"
services: cloud-services
documentationcenter: .net
author: thraka
manager: timlt
editor: 
ms.assetid: 8d1243dc-879c-4d1f-9ed0-eecd1f6a6653
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: adegeo
ms.openlocfilehash: 45f0f30221292f98c591511b091b02ebe1c1272c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a>Instalar o .NET em funções dos Serviços de Nuvem do Azure
Este artigo descreve como tooinstall versões do .NET Framework que não vêm com hello sistema operacional de convidado do Azure. Você pode usar o .NET em tooconfigure de sistema operacional convidado Olá as funções web e de trabalho do serviço de nuvem.

Por exemplo, você pode instalar o .NET 4.6.1 em Olá família do SO convidado 4, que não é fornecido com qualquer outra versão do .NET 4.6. (Olá família do SO convidado 5 vêm com o .NET 4.6.) Para obter informações mais recentes em Olá Olá versões do sistema operacional de convidado do Azure, consulte Olá [notícias de versão do sistema operacional de convidado do Azure](cloud-services-guestos-update-matrix.md). 

>[!IMPORTANT]
>Hello Azure SDK 2.9 contém uma restrição na implantação do .NET 4.6 na família de sistemas operacionais convidados Olá 4 ou anterior. Uma correção para restrição de saudação está disponível em Olá [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.

tooinstall .NET em suas funções web e de trabalho, incluem o instalador do web hello .NET como parte de seu projeto de serviço de nuvem. Inicie o instalador de saudação como parte das tarefas de inicialização da função hello. 

## <a name="add-hello-net-installer-tooyour-project"></a>Adicionar Olá .NET instalador tooyour projeto
instalador da web do toodownload Olá para saudação do .NET Framework, escolha a versão de saudação que você deseja tooinstall:

* [Instalador da Web do .NET 4.7](http://go.microsoft.com/fwlink/?LinkId=825298)
* [Instalador da Web do .NET 4.6.1](http://go.microsoft.com/fwlink/?LinkId=671729)

instalador de saudação tooadd para um *web* função:
  1. No **Gerenciador de Soluções**, em **Funções** no projeto do serviço de nuvem, clique com o botão direito do mouse em sua função *web* e selecione **Adicionar** > **Nova Pasta**. Crie uma pasta chamada **bin**.
  2. Pasta bin do hello e selecione **adicionar** > **Item existente**. Selecione o instalador do .NET hello e adicioná-lo a pasta bin do toohello.
  
instalador de saudação tooadd para um *trabalho* função:
* Clique com o botão direito do mouse na função de *trabalho* e selecione **Adicionar** > **Item Existente**. Selecione o instalador do .NET hello e adicioná-lo a função toohello. 

Quando arquivos são adicionados nesta pasta de conteúdo de função do modo toohello, elas são adicionadas automaticamente tooyour pacote de serviço de nuvem. Olá arquivos são então local consistente de tooa implantado na máquina virtual de saudação. Repita esse processo para cada função da web e de trabalho em seu serviço de nuvem para que todas as funções tem uma cópia do instalador de saudação.

> [!NOTE]
> Você deve instalar o .NET 4.6.1 em sua função de serviço de nuvem mesmo que o aplicativo seja voltado ao .NET 4.6. saudação de sistema operacional convidado inclui Olá da Base de dados de Conhecimento [atualizar 3098779](https://support.microsoft.com/kb/3098779) e [atualizar 3097997](https://support.microsoft.com/kb/3097997). Problemas podem ocorrer quando você executar os aplicativos .NET se .NET 4.6 é instalado sobre atualizações do hello da Base de Conhecimento. tooavoid esses problemas, instale o .NET 4.6.1 em vez da versão 4.6. Para obter mais informações, consulte Olá [artigo da Base de dados de Conhecimento 3118750](https://support.microsoft.com/kb/3118750).
> 
> 

![Conteúdos de função com arquivos do instalador][1]

## <a name="define-startup-tasks-for-your-roles"></a>Defina tarefas de inicialização para suas funções
Você pode usar operações de tooperform de tarefas de inicialização antes do início de uma função. Instalar saudação do .NET Framework como parte da tarefa de inicialização Olá garante framework hello está instalado antes de qualquer código de aplicativo é executado. Para obter mais informações sobre as tarefas de inicialização, consulte [Execução de tarefas de inicialização no Azure](cloud-services-startup-tasks.md). 

1. Adicionar Olá seguir o arquivo servicedefinition. Csdef toohello conteúdo em Olá **WebRole** ou **WorkerRole** nó para todas as funções:
   
    ```xml
    <LocalResources>
      <LocalStorage name="NETFXInstall" sizeInMB="1024" cleanOnRoleRecycle="false" />
    </LocalResources>    
    <Startup>
      <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
        <Environment>
          <Variable name="PathToNETFXInstall">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='NETFXInstall']/@path" />
          </Variable>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
    ```
   
    configuração anterior Hello executa o comando do console Olá `install.cmd` com tooinstall de privilégios de administrador Olá do .NET Framework. configuração de saudação também cria um **LocalStorage** elemento chamado **NETFXInstall**. script de inicialização de saudação define Olá pasta temp toouse esse recurso de armazenamento local. 
    
    > [!IMPORTANT]
    > tooensure corrigir a instalação do framework hello, tamanho de saudação do conjunto de tooat esse recurso menos 1.024 MB.
    
    Para saber mais sobre as tarefas de inicialização, consulte [Tarefas de inicialização comuns dos Serviço de Nuvem do Azure](cloud-services-startup-tasks-common.md).

2. Crie um arquivo chamado **cmd** e adicione a seguinte Olá instala arquivo de script de toohello.

    script Hello verifica se a versão especificada Olá de saudação do .NET Framework já está instalado na máquina de saudação consultando o registro de saudação. Se a versão do .NET Olá não estiver instalado, instalador do hello .NET da web é aberto. toohelp solucionar problemas, script hello registra todas as atividades toohello arquivo startuptasklog-(data e hora atuais). txt que é armazenado em **InstallLogs** armazenamento local.

    > [!IMPORTANT]
    > Use um editor de texto básico como o bloco de notas do Windows toocreate Olá cmd. Se você usar o Visual Studio toocreate um arquivo de texto e alterar Olá too.cmd de extensão, o arquivo hello ainda pode conter uma marca de ordem de byte de UTF-8. Essa marca pode causar um erro quando a primeira linha de saudação do script hello é executada. tooavoid esse erro, verifique a primeira linha hello de saudação uma instrução REM que pode ser ignorada pelo processamento de ordem de byte de saudação do script. 
    > 
    >
   
    ```cmd
    REM Set hello value of netfx tooinstall appropriate .NET Framework. 
    REM ***** tooinstall .NET 4.5.2 set hello variable netfx too"NDP452" *****
    REM ***** tooinstall .NET 4.6 set hello variable netfx too"NDP46" *****
    REM ***** tooinstall .NET 4.6.1 set hello variable netfx too"NDP461" *****
    REM ***** tooinstall .NET 4.6.2 set hello variable netfx too"NDP462" *****
    REM ***** tooinstall .NET 4.7 set hello variable netfx too"NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed toocorrectly install .NET 4.6.1, otherwise you may see an out of disk space error *****
    set TMP=%PathToNETFXInstall%
    set TEMP=%PathToNETFXInstall%

    REM ***** Setup .NET filenames and registry keys *****
    if %netfx%=="NDP47" goto NDP47
    if %netfx%=="NDP462" goto NDP462
    if %netfx%=="NDP461" goto NDP461
    if %netfx%=="NDP46" goto NDP46
        set "netfxinstallfile=NDP452-KB2901954-Web.exe"
        set netfxregkey="0x5cbf5"
        goto logtimestamp

    :NDP46
    set "netfxinstallfile=NDP46-KB3045560-Web.exe"
    set netfxregkey="0x6004f"
    goto logtimestamp

    :NDP461
    set "netfxinstallfile=NDP461-KB3102438-Web.exe"
    set netfxregkey="0x6040e"
    goto logtimestamp

    :NDP462
    set "netfxinstallfile=NDP462-KB3151802-Web.exe"
    set netfxregkey="0x60632"

    :NDP47
    set "netfxinstallfile=NDP47-KB3186500-Web.exe"
    set netfxregkey="0x707FE"

    :logtimestamp
    REM ***** Setup LogFile with timestamp *****
    md "%PathToNETFXInstall%\log"
    set startuptasklog="%PathToNETFXInstall%log\startuptasklog-%timestamp%.txt"
    set netfxinstallerlog="%PathToNETFXInstall%log\NetFXInstallerLog-%timestamp%"
    echo %log% >> %startuptasklog%
    echo Logfile generated at: %startuptasklog% >> %startuptasklog%
    echo TMP set to: %TMP% >> %startuptasklog%
    echo TEMP set to: %TEMP% >> %startuptasklog%

    REM ***** Check if .NET is installed *****
    echo Checking if .NET (%netfx%) is installed >> %startuptasklog%
    set /A netfxregkeydecimal=%netfxregkey%
    set foundkey=0
    FOR /F "usebackq skip=2 tokens=1,2*" %%A in (`reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full" /v Release 2^>nul`) do @set /A foundkey=%%C
    echo Minimum required key: %netfxregkeydecimal% -- found key: %foundkey% >> %startuptasklog%
    if %foundkey% GEQ %netfxregkeydecimal% goto installed

    REM ***** Installing .NET *****
    echo Installing .NET with commandline: start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog%  /chainingpackage "CloudService Startup Task" >> %startuptasklog%
    start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog% /chainingpackage "CloudService Startup Task" >> %startuptasklog% 2>>&1
    if %ERRORLEVEL%== 0 goto installed
        echo .NET installer exited with code %ERRORLEVEL% >> %startuptasklog%    
        if %ERRORLEVEL%== 3010 goto restart
        if %ERRORLEVEL%== 1641 goto restart
        echo .NET (%netfx%) install failed with Error Code %ERRORLEVEL%. Further logs can be found in %netfxinstallerlog% >> %startuptasklog%

    :restart
    echo Restarting toocomplete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > Esse script mostra como tooinstall .NET 4.5.2 ou versão 4.6 para continuidade, mesmo que o .NET 4.5.2 já está disponível em Olá sistema operacional de convidado do Azure. Diretamente você deve instalar o .NET 4.6.1 em vez da versão 4.6, conforme descrito em Olá [artigo da Base de dados de Conhecimento 3118750](https://support.microsoft.com/kb/3118750).
   > 
   > 

3. Função de tooeach adicionar Olá cmd arquivos usando **adicionar** > **Item existente** na **Solution Explorer** conforme descrito anteriormente neste tópico. 

    Após essa etapa for concluída, todas as funções devem ter Olá arquivo de instalador de .NET e Olá cmd.

   ![Conteúdo da função com todos os arquivos][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a>Configurar o diagnóstico tootransfer inicialização logs tooBlob armazenamento
toosimplify Solucionando problemas de instalação, você pode configurar o diagnóstico do Azure tootransfer os arquivos de log gerados por inicialização de saudação do script ou Olá armazenamento de Blob de tooAzure de instalador do .NET. Usando essa abordagem, você pode exibir os logs de saudação pelo download de arquivos de log de saudação do armazenamento de Blob em vez de ter tooremote a área de trabalho em função hello.

Diagnóstico tooconfigure, abrir o arquivo de wadcfgx hello e adicione Olá Olá o conteúdo a seguir **diretórios** nó: 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

Esse XML configura arquivos de saudação do diagnóstico tootransfer no diretório de log Olá no hello **NETFXInstall** toohello do recurso conta de armazenamento de diagnóstico no hello **netfx-instalar** contêiner de blob.

## <a name="deploy-your-cloud-service"></a>Implantar o serviço de nuvem
Quando você implanta o serviço de nuvem, as tarefas de inicialização Olá instalar saudação do .NET Framework se ele ainda não estiver instalado. As funções do serviço de nuvem estão em Olá *ocupado* estado enquanto o framework hello está sendo instalado. Se a instalação do framework Olá exigir uma reinicialização, as funções de serviço de saudação também podem ser reiniciado. 

## <a name="additional-resources"></a>Recursos adicionais
* [Saudação de instalação do .NET Framework][Installing hello .NET Framework]
* [Determinar quais versões do .NET Framework estão instaladas][How to: Determine Which .NET Framework Versions Are Installed]
* [Solução de problemas de instalações do .NET Framework][Troubleshooting .NET Framework Installations]

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
