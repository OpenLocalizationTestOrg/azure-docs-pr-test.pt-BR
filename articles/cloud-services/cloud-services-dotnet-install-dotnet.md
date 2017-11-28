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
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="edfd0-103">Instalar o .NET em funções dos Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="edfd0-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="edfd0-104">Este artigo descreve como tooinstall versões do .NET Framework que não vêm com hello sistema operacional de convidado do Azure.</span><span class="sxs-lookup"><span data-stu-id="edfd0-104">This article describes how tooinstall versions of .NET Framework that don't come with hello Azure Guest OS.</span></span> <span data-ttu-id="edfd0-105">Você pode usar o .NET em tooconfigure de sistema operacional convidado Olá as funções web e de trabalho do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="edfd0-105">You can use .NET on hello Guest OS tooconfigure your cloud service web and worker roles.</span></span>

<span data-ttu-id="edfd0-106">Por exemplo, você pode instalar o .NET 4.6.1 em Olá família do SO convidado 4, que não é fornecido com qualquer outra versão do .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="edfd0-106">For example, you can install .NET 4.6.1 on hello Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="edfd0-107">(Olá família do SO convidado 5 vêm com o .NET 4.6.) Para obter informações mais recentes em Olá Olá versões do sistema operacional de convidado do Azure, consulte Olá [notícias de versão do sistema operacional de convidado do Azure](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="edfd0-107">(hello Guest OS family 5 does come with .NET 4.6.) For hello latest information on hello Azure Guest OS releases, see hello [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="edfd0-108">Hello Azure SDK 2.9 contém uma restrição na implantação do .NET 4.6 na família de sistemas operacionais convidados Olá 4 ou anterior.</span><span class="sxs-lookup"><span data-stu-id="edfd0-108">hello Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on hello Guest OS family 4 or earlier.</span></span> <span data-ttu-id="edfd0-109">Uma correção para restrição de saudação está disponível em Olá [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span><span class="sxs-lookup"><span data-stu-id="edfd0-109">A fix for hello restriction is available on hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="edfd0-110">tooinstall .NET em suas funções web e de trabalho, incluem o instalador do web hello .NET como parte de seu projeto de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="edfd0-110">tooinstall .NET on your web and worker roles, include hello .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="edfd0-111">Inicie o instalador de saudação como parte das tarefas de inicialização da função hello.</span><span class="sxs-lookup"><span data-stu-id="edfd0-111">Start hello installer as part of hello role's startup tasks.</span></span> 

## <a name="add-hello-net-installer-tooyour-project"></a><span data-ttu-id="edfd0-112">Adicionar Olá .NET instalador tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="edfd0-112">Add hello .NET installer tooyour project</span></span>
<span data-ttu-id="edfd0-113">instalador da web do toodownload Olá para saudação do .NET Framework, escolha a versão de saudação que você deseja tooinstall:</span><span class="sxs-lookup"><span data-stu-id="edfd0-113">toodownload hello web installer for hello .NET Framework, choose hello version that you want tooinstall:</span></span>

* [<span data-ttu-id="edfd0-114">Instalador da Web do .NET 4.7</span><span class="sxs-lookup"><span data-stu-id="edfd0-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="edfd0-115">Instalador da Web do .NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="edfd0-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="edfd0-116">instalador de saudação tooadd para um *web* função:</span><span class="sxs-lookup"><span data-stu-id="edfd0-116">tooadd hello installer for a *web* role:</span></span>
  1. <span data-ttu-id="edfd0-117">No **Gerenciador de Soluções**, em **Funções** no projeto do serviço de nuvem, clique com o botão direito do mouse em sua função *web* e selecione **Adicionar** > **Nova Pasta**.</span><span class="sxs-lookup"><span data-stu-id="edfd0-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="edfd0-118">Crie uma pasta chamada **bin**.</span><span class="sxs-lookup"><span data-stu-id="edfd0-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="edfd0-119">Pasta bin do hello e selecione **adicionar** > **Item existente**.</span><span class="sxs-lookup"><span data-stu-id="edfd0-119">Right-click hello bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="edfd0-120">Selecione o instalador do .NET hello e adicioná-lo a pasta bin do toohello.</span><span class="sxs-lookup"><span data-stu-id="edfd0-120">Select hello .NET installer and add it toohello bin folder.</span></span>
  
<span data-ttu-id="edfd0-121">instalador de saudação tooadd para um *trabalho* função:</span><span class="sxs-lookup"><span data-stu-id="edfd0-121">tooadd hello installer for a *worker* role:</span></span>
* <span data-ttu-id="edfd0-122">Clique com o botão direito do mouse na função de *trabalho* e selecione **Adicionar** > **Item Existente**.</span><span class="sxs-lookup"><span data-stu-id="edfd0-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="edfd0-123">Selecione o instalador do .NET hello e adicioná-lo a função toohello.</span><span class="sxs-lookup"><span data-stu-id="edfd0-123">Select hello .NET installer and add it toohello role.</span></span> 

<span data-ttu-id="edfd0-124">Quando arquivos são adicionados nesta pasta de conteúdo de função do modo toohello, elas são adicionadas automaticamente tooyour pacote de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="edfd0-124">When files are added in this way toohello role content folder, they're automatically added tooyour cloud service package.</span></span> <span data-ttu-id="edfd0-125">Olá arquivos são então local consistente de tooa implantado na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="edfd0-125">hello files are then deployed tooa consistent location on hello virtual machine.</span></span> <span data-ttu-id="edfd0-126">Repita esse processo para cada função da web e de trabalho em seu serviço de nuvem para que todas as funções tem uma cópia do instalador de saudação.</span><span class="sxs-lookup"><span data-stu-id="edfd0-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of hello installer.</span></span>

> [!NOTE]
> <span data-ttu-id="edfd0-127">Você deve instalar o .NET 4.6.1 em sua função de serviço de nuvem mesmo que o aplicativo seja voltado ao .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="edfd0-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="edfd0-128">saudação de sistema operacional convidado inclui Olá da Base de dados de Conhecimento [atualizar 3098779](https://support.microsoft.com/kb/3098779) e [atualizar 3097997](https://support.microsoft.com/kb/3097997).</span><span class="sxs-lookup"><span data-stu-id="edfd0-128">hello Guest OS includes hello Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="edfd0-129">Problemas podem ocorrer quando você executar os aplicativos .NET se .NET 4.6 é instalado sobre atualizações do hello da Base de Conhecimento.</span><span class="sxs-lookup"><span data-stu-id="edfd0-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of hello Knowledge Base updates.</span></span> <span data-ttu-id="edfd0-130">tooavoid esses problemas, instale o .NET 4.6.1 em vez da versão 4.6.</span><span class="sxs-lookup"><span data-stu-id="edfd0-130">tooavoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="edfd0-131">Para obter mais informações, consulte Olá [artigo da Base de dados de Conhecimento 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="edfd0-131">For more information, see hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Conteúdos de função com arquivos do instalador][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="edfd0-133">Defina tarefas de inicialização para suas funções</span><span class="sxs-lookup"><span data-stu-id="edfd0-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="edfd0-134">Você pode usar operações de tooperform de tarefas de inicialização antes do início de uma função.</span><span class="sxs-lookup"><span data-stu-id="edfd0-134">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="edfd0-135">Instalar saudação do .NET Framework como parte da tarefa de inicialização Olá garante framework hello está instalado antes de qualquer código de aplicativo é executado.</span><span class="sxs-lookup"><span data-stu-id="edfd0-135">Installing hello .NET Framework as part of hello startup task ensures that hello framework is installed before any application code is run.</span></span> <span data-ttu-id="edfd0-136">Para obter mais informações sobre as tarefas de inicialização, consulte [Execução de tarefas de inicialização no Azure](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="edfd0-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="edfd0-137">Adicionar Olá seguir o arquivo servicedefinition. Csdef toohello conteúdo em Olá **WebRole** ou **WorkerRole** nó para todas as funções:</span><span class="sxs-lookup"><span data-stu-id="edfd0-137">Add hello following content toohello ServiceDefinition.csdef file under hello **WebRole** or **WorkerRole** node for all roles:</span></span>
   
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
   
    <span data-ttu-id="edfd0-138">configuração anterior Hello executa o comando do console Olá `install.cmd` com tooinstall de privilégios de administrador Olá do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="edfd0-138">hello preceding configuration runs hello console command `install.cmd` with administrator privileges tooinstall hello .NET Framework.</span></span> <span data-ttu-id="edfd0-139">configuração de saudação também cria um **LocalStorage** elemento chamado **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="edfd0-139">hello configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="edfd0-140">script de inicialização de saudação define Olá pasta temp toouse esse recurso de armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="edfd0-140">hello startup script sets hello temp folder toouse this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="edfd0-141">tooensure corrigir a instalação do framework hello, tamanho de saudação do conjunto de tooat esse recurso menos 1.024 MB.</span><span class="sxs-lookup"><span data-stu-id="edfd0-141">tooensure correct installation of hello framework, set hello size of this resource tooat least 1,024 MB.</span></span>
    
    <span data-ttu-id="edfd0-142">Para saber mais sobre as tarefas de inicialização, consulte [Tarefas de inicialização comuns dos Serviço de Nuvem do Azure](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="edfd0-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="edfd0-143">Crie um arquivo chamado **cmd** e adicione a seguinte Olá instala arquivo de script de toohello.</span><span class="sxs-lookup"><span data-stu-id="edfd0-143">Create a file named **install.cmd** and add hello following install script toohello file.</span></span>

    <span data-ttu-id="edfd0-144">script Hello verifica se a versão especificada Olá de saudação do .NET Framework já está instalado na máquina de saudação consultando o registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="edfd0-144">hello script checks whether hello specified version of hello .NET Framework is already installed on hello machine by querying hello registry.</span></span> <span data-ttu-id="edfd0-145">Se a versão do .NET Olá não estiver instalado, instalador do hello .NET da web é aberto.</span><span class="sxs-lookup"><span data-stu-id="edfd0-145">If hello .NET version is not installed, then hello .NET web installer is opened.</span></span> <span data-ttu-id="edfd0-146">toohelp solucionar problemas, script hello registra todas as atividades toohello arquivo startuptasklog-(data e hora atuais). txt que é armazenado em **InstallLogs** armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="edfd0-146">toohelp troubleshoot any issues, hello script logs all activity toohello file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="edfd0-147">Use um editor de texto básico como o bloco de notas do Windows toocreate Olá cmd.</span><span class="sxs-lookup"><span data-stu-id="edfd0-147">Use a basic text editor like Windows Notepad toocreate hello install.cmd file.</span></span> <span data-ttu-id="edfd0-148">Se você usar o Visual Studio toocreate um arquivo de texto e alterar Olá too.cmd de extensão, o arquivo hello ainda pode conter uma marca de ordem de byte de UTF-8.</span><span class="sxs-lookup"><span data-stu-id="edfd0-148">If you use Visual Studio toocreate a text file and change hello extension too.cmd, hello file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="edfd0-149">Essa marca pode causar um erro quando a primeira linha de saudação do script hello é executada.</span><span class="sxs-lookup"><span data-stu-id="edfd0-149">This mark can cause an error when hello first line of hello script is run.</span></span> <span data-ttu-id="edfd0-150">tooavoid esse erro, verifique a primeira linha hello de saudação uma instrução REM que pode ser ignorada pelo processamento de ordem de byte de saudação do script.</span><span class="sxs-lookup"><span data-stu-id="edfd0-150">tooavoid this error, make hello first line of hello script a REM statement that can be skipped by hello byte order processing.</span></span> 
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
   > <span data-ttu-id="edfd0-151">Esse script mostra como tooinstall .NET 4.5.2 ou versão 4.6 para continuidade, mesmo que o .NET 4.5.2 já está disponível em Olá sistema operacional de convidado do Azure.</span><span class="sxs-lookup"><span data-stu-id="edfd0-151">This script shows how tooinstall .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on hello Azure Guest OS.</span></span> <span data-ttu-id="edfd0-152">Diretamente você deve instalar o .NET 4.6.1 em vez da versão 4.6, conforme descrito em Olá [artigo da Base de dados de Conhecimento 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="edfd0-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="edfd0-153">Função de tooeach adicionar Olá cmd arquivos usando **adicionar** > **Item existente** na **Solution Explorer** conforme descrito anteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="edfd0-153">Add hello install.cmd file tooeach role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="edfd0-154">Após essa etapa for concluída, todas as funções devem ter Olá arquivo de instalador de .NET e Olá cmd.</span><span class="sxs-lookup"><span data-stu-id="edfd0-154">After this step is complete, all roles should have hello .NET installer file and hello install.cmd file.</span></span>

   ![Conteúdo da função com todos os arquivos][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a><span data-ttu-id="edfd0-156">Configurar o diagnóstico tootransfer inicialização logs tooBlob armazenamento</span><span class="sxs-lookup"><span data-stu-id="edfd0-156">Configure Diagnostics tootransfer startup logs tooBlob storage</span></span>
<span data-ttu-id="edfd0-157">toosimplify Solucionando problemas de instalação, você pode configurar o diagnóstico do Azure tootransfer os arquivos de log gerados por inicialização de saudação do script ou Olá armazenamento de Blob de tooAzure de instalador do .NET.</span><span class="sxs-lookup"><span data-stu-id="edfd0-157">toosimplify troubleshooting installation issues, you can configure Azure Diagnostics tootransfer any log files generated by hello startup script or hello .NET installer tooAzure Blob storage.</span></span> <span data-ttu-id="edfd0-158">Usando essa abordagem, você pode exibir os logs de saudação pelo download de arquivos de log de saudação do armazenamento de Blob em vez de ter tooremote a área de trabalho em função hello.</span><span class="sxs-lookup"><span data-stu-id="edfd0-158">By using this approach, you can view hello logs by downloading hello log files from Blob storage rather than having tooremote desktop into hello role.</span></span>

<span data-ttu-id="edfd0-159">Diagnóstico tooconfigure, abrir o arquivo de wadcfgx hello e adicione Olá Olá o conteúdo a seguir **diretórios** nó:</span><span class="sxs-lookup"><span data-stu-id="edfd0-159">tooconfigure Diagnostics, open hello diagnostics.wadcfgx file and add hello following content under hello **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="edfd0-160">Esse XML configura arquivos de saudação do diagnóstico tootransfer no diretório de log Olá no hello **NETFXInstall** toohello do recurso conta de armazenamento de diagnóstico no hello **netfx-instalar** contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="edfd0-160">This XML configures Diagnostics tootransfer hello files in hello log directory in hello **NETFXInstall** resource toohello Diagnostics storage account in hello **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="edfd0-161">Implantar o serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="edfd0-161">Deploy your cloud service</span></span>
<span data-ttu-id="edfd0-162">Quando você implanta o serviço de nuvem, as tarefas de inicialização Olá instalar saudação do .NET Framework se ele ainda não estiver instalado.</span><span class="sxs-lookup"><span data-stu-id="edfd0-162">When you deploy your cloud service, hello startup tasks install hello .NET Framework if it's not already installed.</span></span> <span data-ttu-id="edfd0-163">As funções do serviço de nuvem estão em Olá *ocupado* estado enquanto o framework hello está sendo instalado.</span><span class="sxs-lookup"><span data-stu-id="edfd0-163">Your cloud service roles are in hello *busy* state while hello framework is being installed.</span></span> <span data-ttu-id="edfd0-164">Se a instalação do framework Olá exigir uma reinicialização, as funções de serviço de saudação também podem ser reiniciado.</span><span class="sxs-lookup"><span data-stu-id="edfd0-164">If hello framework installation requires a restart, hello service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="edfd0-165">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="edfd0-165">Additional resources</span></span>
* <span data-ttu-id="edfd0-166">[Saudação de instalação do .NET Framework][Installing hello .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="edfd0-166">[Installing hello .NET Framework][Installing hello .NET Framework]</span></span>
* <span data-ttu-id="edfd0-167">[Determinar quais versões do .NET Framework estão instaladas][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="edfd0-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="edfd0-168">[Solução de problemas de instalações do .NET Framework][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="edfd0-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
