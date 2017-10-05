---
title: "Instalar o .NET em funções dos Serviços de Nuvem do Azure | Microsoft Docs"
description: "Este artigo descreve como instalar manualmente o .NET Framework em funções de trabalho e web de seu serviço de nuvem"
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
ms.openlocfilehash: a9cffa275ae6b9315b821d3160b17a997a1523f7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="b4085-103">Instalar o .NET em funções dos Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="b4085-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="b4085-104">Este artigo descreve como instalar versões do .NET Framework que não são fornecidas com o SO convidado do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4085-104">This article describes how to install versions of .NET Framework that don't come with the Azure Guest OS.</span></span> <span data-ttu-id="b4085-105">Você pode usar o .NET no SO convidado para configurar as funções Web e de trabalho de seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="b4085-105">You can use .NET on the Guest OS to configure your cloud service web and worker roles.</span></span>

<span data-ttu-id="b4085-106">Por exemplo, você pode instalar o .NET 4.6.1 na família de SOs convidados 4, que não é fornecida com nenhuma versão do .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="b4085-106">For example, you can install .NET 4.6.1 on the Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="b4085-107">(A família de SOs convidados 5 é fornecida com o .NET 4.6.) Para obter as informações mais recentes sobre as versões do SO convidado do Azure, consulte [Notícias de versão do SO Convidado do Azure](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="b4085-107">(The Guest OS family 5 does come with .NET 4.6.) For the latest information on the Azure Guest OS releases, see the [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="b4085-108">O SDK 2.9 do Azure contém uma restrição da implantação do .NET 4.6 na família de SOs convidados 4 ou inferior.</span><span class="sxs-lookup"><span data-stu-id="b4085-108">The Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on the Guest OS family 4 or earlier.</span></span> <span data-ttu-id="b4085-109">Uma correção para essa restrição está disponível no site [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="b4085-109">A fix for the restriction is available on the [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="b4085-110">Para instalar o .NET em suas funções web e de trabalho, inclua o instalador Web do .NET como parte de seu projeto de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="b4085-110">To install .NET on your web and worker roles, include the .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="b4085-111">Inicie o instalador como parte das tarefas de inicialização da função.</span><span class="sxs-lookup"><span data-stu-id="b4085-111">Start the installer as part of the role's startup tasks.</span></span> 

## <a name="add-the-net-installer-to-your-project"></a><span data-ttu-id="b4085-112">Adicione o instalador do .NET ao seu projeto</span><span class="sxs-lookup"><span data-stu-id="b4085-112">Add the .NET installer to your project</span></span>
<span data-ttu-id="b4085-113">Para baixar o instalador da Web para o .NET Framework, escolha a versão que você deseja instalar:</span><span class="sxs-lookup"><span data-stu-id="b4085-113">To download the web installer for the .NET Framework, choose the version that you want to install:</span></span>

* [<span data-ttu-id="b4085-114">Instalador da Web do .NET 4.7</span><span class="sxs-lookup"><span data-stu-id="b4085-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="b4085-115">Instalador da Web do .NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="b4085-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="b4085-116">Para adicionar o instalador para uma função *web*:</span><span class="sxs-lookup"><span data-stu-id="b4085-116">To add the installer for a *web* role:</span></span>
  1. <span data-ttu-id="b4085-117">No **Gerenciador de Soluções**, em **Funções** no projeto do serviço de nuvem, clique com o botão direito do mouse em sua função *web* e selecione **Adicionar** > **Nova Pasta**.</span><span class="sxs-lookup"><span data-stu-id="b4085-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="b4085-118">Crie uma pasta chamada **bin**.</span><span class="sxs-lookup"><span data-stu-id="b4085-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="b4085-119">Clique com o botão direito do mouse na pasta bin e selecione **Adicionar** > **Item Existente**.</span><span class="sxs-lookup"><span data-stu-id="b4085-119">Right-click the bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="b4085-120">Selecione o instalador do .NET e adicione-o à pasta bin.</span><span class="sxs-lookup"><span data-stu-id="b4085-120">Select the .NET installer and add it to the bin folder.</span></span>
  
<span data-ttu-id="b4085-121">Para adicionar o instalador para uma função de *trabalho*:</span><span class="sxs-lookup"><span data-stu-id="b4085-121">To add the installer for a *worker* role:</span></span>
* <span data-ttu-id="b4085-122">Clique com o botão direito do mouse na função de *trabalho* e selecione **Adicionar** > **Item Existente**.</span><span class="sxs-lookup"><span data-stu-id="b4085-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="b4085-123">Selecione o instalador do .NET e adicione-o à função.</span><span class="sxs-lookup"><span data-stu-id="b4085-123">Select the .NET installer and add it to the role.</span></span> 

<span data-ttu-id="b4085-124">Quando arquivos são adicionados dessa forma à pasta de conteúdo da função, eles são adicionados automaticamente ao seu pacote de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="b4085-124">When files are added in this way to the role content folder, they're automatically added to your cloud service package.</span></span> <span data-ttu-id="b4085-125">Em seguida, os arquivos são implantados em um local consistente na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b4085-125">The files are then deployed to a consistent location on the virtual machine.</span></span> <span data-ttu-id="b4085-126">Repita esse processo para cada função Web e de trabalho em seu serviço de nuvem para que todas as funções tenham uma cópia do instalador.</span><span class="sxs-lookup"><span data-stu-id="b4085-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of the installer.</span></span>

> [!NOTE]
> <span data-ttu-id="b4085-127">Você deve instalar o .NET 4.6.1 em sua função de serviço de nuvem mesmo que o aplicativo seja voltado ao .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="b4085-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="b4085-128">O SO convidado inclui a [atualização 3098779](https://support.microsoft.com/kb/3098779) e a [atualização 3097997](https://support.microsoft.com/kb/3097997) da Base de Dados de Conhecimento.</span><span class="sxs-lookup"><span data-stu-id="b4085-128">The Guest OS includes the Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="b4085-129">Problemas podem ocorrer quando você executar aplicativos .NET se o .NET 4.6 estiver instalado sobre as atualizações da Base de Dados de Conhecimento.</span><span class="sxs-lookup"><span data-stu-id="b4085-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of the Knowledge Base updates.</span></span> <span data-ttu-id="b4085-130">Para evitar esses problemas, instale o .NET 4.6.1 em vez da versão 4.6.</span><span class="sxs-lookup"><span data-stu-id="b4085-130">To avoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="b4085-131">Para obter mais informações, consulte o [Artigo 3118750 da Base de Dados de Conhecimento](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="b4085-131">For more information, see the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Conteúdos de função com arquivos do instalador][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="b4085-133">Defina tarefas de inicialização para suas funções</span><span class="sxs-lookup"><span data-stu-id="b4085-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="b4085-134">Você pode usar as tarefas de inicialização para executar operações antes do início de uma função.</span><span class="sxs-lookup"><span data-stu-id="b4085-134">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="b4085-135">Instalar o .NET Framework como parte da tarefa de inicialização garante que ele seja instalado antes que qualquer código de aplicativo seja executado.</span><span class="sxs-lookup"><span data-stu-id="b4085-135">Installing the .NET Framework as part of the startup task ensures that the framework is installed before any application code is run.</span></span> <span data-ttu-id="b4085-136">Para obter mais informações sobre as tarefas de inicialização, consulte [Execução de tarefas de inicialização no Azure](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="b4085-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="b4085-137">Adicione o seguinte conteúdo ao arquivo ServiceDefinition.sdef sob o nó **WebRole** ou **WorkerRole** para todas as funções:</span><span class="sxs-lookup"><span data-stu-id="b4085-137">Add the following content to the ServiceDefinition.csdef file under the **WebRole** or **WorkerRole** node for all roles:</span></span>
   
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
   
    <span data-ttu-id="b4085-138">A configuração anterior executa o comando do console `install.cmd` com privilégios de administrador a fim de instalar o .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="b4085-138">The preceding configuration runs the console command `install.cmd` with administrator privileges to install the .NET Framework.</span></span> <span data-ttu-id="b4085-139">A configuração também cria um elemento **LocalStorage** com o nome **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="b4085-139">The configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="b4085-140">O script de inicialização define a pasta temporária para usar esse recurso de armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="b4085-140">The startup script sets the temp folder to use this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="b4085-141">Para garantir a instalação correta do Framework, defina o tamanho desse recurso como, pelo menos, 1.024 MB.</span><span class="sxs-lookup"><span data-stu-id="b4085-141">To ensure correct installation of the framework, set the size of this resource to at least 1,024 MB.</span></span>
    
    <span data-ttu-id="b4085-142">Para saber mais sobre as tarefas de inicialização, consulte [Tarefas de inicialização comuns dos Serviço de Nuvem do Azure](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="b4085-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="b4085-143">Crie um arquivo chamado **install.cmd** e adicione o seguinte script de instalação a ele.</span><span class="sxs-lookup"><span data-stu-id="b4085-143">Create a file named **install.cmd** and add the following install script to the file.</span></span>

    <span data-ttu-id="b4085-144">O script verifica se a versão especificada do .NET Framework já está instalada no computador consultando o registro.</span><span class="sxs-lookup"><span data-stu-id="b4085-144">The script checks whether the specified version of the .NET Framework is already installed on the machine by querying the registry.</span></span> <span data-ttu-id="b4085-145">Se a versão do .NET não estiver instalada, o instalador da Web do .NET será aberto.</span><span class="sxs-lookup"><span data-stu-id="b4085-145">If the .NET version is not installed, then the .NET web installer is opened.</span></span> <span data-ttu-id="b4085-146">Para ajudar com a solução de problemas, o script registra todas as atividades no arquivo startuptasklog-(data e hora atual).txt colocado no armazenamento local **InstallLogs**.</span><span class="sxs-lookup"><span data-stu-id="b4085-146">To help troubleshoot any issues, the script logs all activity to the file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b4085-147">Use um editor de texto básico, como o Bloco de Notas do Windows, para criar o arquivo install.cmd.</span><span class="sxs-lookup"><span data-stu-id="b4085-147">Use a basic text editor like Windows Notepad to create the install.cmd file.</span></span> <span data-ttu-id="b4085-148">Se você usar o Visual Studio para criar um arquivo de texto e alterar a extensão para .cmd, o arquivo ainda poderá conter uma marca de ordem de byte de UTF-8.</span><span class="sxs-lookup"><span data-stu-id="b4085-148">If you use Visual Studio to create a text file and change the extension to .cmd, the file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="b4085-149">Essa marca pode causar um erro quando a primeira linha do script for executada.</span><span class="sxs-lookup"><span data-stu-id="b4085-149">This mark can cause an error when the first line of the script is run.</span></span> <span data-ttu-id="b4085-150">Para evitar esse erro, faça com que a primeira linha do script seja uma instrução REM, que pode ser ignorada pelo processamento de ordem de byte.</span><span class="sxs-lookup"><span data-stu-id="b4085-150">To avoid this error, make the first line of the script a REM statement that can be skipped by the byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set the value of netfx to install appropriate .NET Framework. 
    REM ***** To install .NET 4.5.2 set the variable netfx to "NDP452" *****
    REM ***** To install .NET 4.6 set the variable netfx to "NDP46" *****
    REM ***** To install .NET 4.6.1 set the variable netfx to "NDP461" *****
    REM ***** To install .NET 4.6.2 set the variable netfx to "NDP462" *****
    REM ***** To install .NET 4.7 set the variable netfx to "NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed to correctly install .NET 4.6.1, otherwise you may see an out of disk space error *****
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
    echo Restarting to complete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="b4085-151">Esse script mostra como instalar o .NET 4.5.2 ou a versão 4.6 para continuidade, mesmo que o .NET 4.5.2 já esteja disponível no SO convidado do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4085-151">This script shows how to install .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on the Azure Guest OS.</span></span> <span data-ttu-id="b4085-152">Você deve instalar diretamente o .NET 4.6.1 em vez da versão 4.6, conforme descrito no [Artigo 3118750 da Base de Dados de Conhecimento](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="b4085-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="b4085-153">Adicione o arquivo install.cmd a cada função usando **Adicionar** > **Item Existente** no **Gerenciador de Soluções**, conforme descrito anteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="b4085-153">Add the install.cmd file to each role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="b4085-154">Após a conclusão desta etapa, todas as funções devem ter o arquivo do instalador do .NET, assim como o arquivo install.cmd.</span><span class="sxs-lookup"><span data-stu-id="b4085-154">After this step is complete, all roles should have the .NET installer file and the install.cmd file.</span></span>

   ![Conteúdo da função com todos os arquivos][2]

## <a name="configure-diagnostics-to-transfer-startup-logs-to-blob-storage"></a><span data-ttu-id="b4085-156">Configurar o Diagnóstico para transferir logs de inicialização para o Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="b4085-156">Configure Diagnostics to transfer startup logs to Blob storage</span></span>
<span data-ttu-id="b4085-157">Para simplificar a solução de problemas de instalação, você pode configurar o Diagnóstico do Azure para transferir os arquivos de log gerados pelo script de inicialização ou pelo instalador do .NET para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4085-157">To simplify troubleshooting installation issues, you can configure Azure Diagnostics to transfer any log files generated by the startup script or the .NET installer to Azure Blob storage.</span></span> <span data-ttu-id="b4085-158">Usando essa abordagem, você pode exibir os logs baixando os arquivos de log do Armazenamento de Blobs em vez de usar a área de trabalho remota na função.</span><span class="sxs-lookup"><span data-stu-id="b4085-158">By using this approach, you can view the logs by downloading the log files from Blob storage rather than having to remote desktop into the role.</span></span>

<span data-ttu-id="b4085-159">Para configurar o Diagnóstico, abra o arquivo diagnostics.wadcfgx e adicione o seguinte conteúdo abaixo do nó **Diretórios**:</span><span class="sxs-lookup"><span data-stu-id="b4085-159">To configure Diagnostics, open the diagnostics.wadcfgx file and add the following content under the **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="b4085-160">Esse XML configura o Diagnóstico para transferir os arquivos no diretório do log no recurso **NETFXInstall** para a conta de armazenamento do Diagnóstico no contêiner de blobs **netfx-install**.</span><span class="sxs-lookup"><span data-stu-id="b4085-160">This XML configures Diagnostics to transfer the files in the log directory in the **NETFXInstall** resource to the Diagnostics storage account in the **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="b4085-161">Implantar o serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="b4085-161">Deploy your cloud service</span></span>
<span data-ttu-id="b4085-162">Quando você implanta o serviço de nuvem, as tarefas de inicialização instalam o .NET Framework se ele ainda não estiver instalado.</span><span class="sxs-lookup"><span data-stu-id="b4085-162">When you deploy your cloud service, the startup tasks install the .NET Framework if it's not already installed.</span></span> <span data-ttu-id="b4085-163">As funções do serviço de nuvem ficam no estado *ocupado* enquanto o Framework está sendo instalado.</span><span class="sxs-lookup"><span data-stu-id="b4085-163">Your cloud service roles are in the *busy* state while the framework is being installed.</span></span> <span data-ttu-id="b4085-164">Se a instalação do Framework exigir uma reinicialização, as funções do serviço também poderão ser reiniciadas.</span><span class="sxs-lookup"><span data-stu-id="b4085-164">If the framework installation requires a restart, the service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b4085-165">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b4085-165">Additional resources</span></span>
* <span data-ttu-id="b4085-166">[Instalação do .NET Framework][Installing the .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="b4085-166">[Installing the .NET Framework][Installing the .NET Framework]</span></span>
* <span data-ttu-id="b4085-167">[Determinar quais versões do .NET Framework estão instaladas][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="b4085-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="b4085-168">[Solução de problemas de instalações do .NET Framework][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="b4085-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing the .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
