---
title: "aaaGet de Introdução ao Python e serviços de nuvem do Azure | Microsoft Docs"
description: "Visão geral de como usar as ferramentas Python para serviços de nuvem do Azure do Visual Studio toocreate incluindo funções web e funções de trabalho."
services: cloud-services
documentationcenter: python
author: thraka
manager: timlt
editor: 
ms.assetid: 5489405d-6fa9-4b11-a161-609103cbdc18
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: f5fd85e754839f146abe912351c59dc4a148c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="3b9a5-103">Funções Web e de trabalho do Python com Ferramentas Python para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3b9a5-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="3b9a5-104">Este artigo oferece uma visão geral do uso das funções Web e de trabalho do Python por meio das [Ferramentas do Python para Visual Studio][Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="3b9a5-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="3b9a5-105">Saiba como toouse Visual Studio toocreate e implantar um serviço de nuvem básico que usa o Python.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-105">Learn how toouse Visual Studio toocreate and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b9a5-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3b9a5-106">Prerequisites</span></span>
* [<span data-ttu-id="3b9a5-107">Visual Studio 2013, 2015 ou 2017</span><span class="sxs-lookup"><span data-stu-id="3b9a5-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="3b9a5-108">[Ferramentas do Python para Visual Studio][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="3b9a5-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="3b9a5-109">[Ferramentas do SDK do Azure para VS 2013][Azure SDK Tools for VS 2013] ou</span><span class="sxs-lookup"><span data-stu-id="3b9a5-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="3b9a5-110">[Ferramentas do SDK do Azure para VS 2015][Azure SDK Tools for VS 2015] ou</span><span class="sxs-lookup"><span data-stu-id="3b9a5-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="3b9a5-111">[Ferramentas do SDK do Azure para VS 2017][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="3b9a5-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="3b9a5-112">[Python 2.7 de 32 bits][Python 2.7 32-bit] ou [Python 3.5 de 32 bits][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="3b9a5-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="3b9a5-113">O que são funções Web e de Trabalho do Python?</span><span class="sxs-lookup"><span data-stu-id="3b9a5-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="3b9a5-114">O Azure fornece três modelos de computação para a execução de aplicativos: [Recurso de Aplicativos Web no Serviço de Aplicativo do Azure][execution model-web sites], [Máquinas Virtuais do Azure][execution model-vms] e [Serviços de Nuvem do Azure][execution model-cloud services].</span><span class="sxs-lookup"><span data-stu-id="3b9a5-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="3b9a5-115">Todos os três modelos oferecem suporte ao Python.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-115">All three models support Python.</span></span> <span data-ttu-id="3b9a5-116">Os Serviços de Nuvem, que incluem as funções Web e de trabalho, fornecem a *PaaS (plataforma como serviço)*.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="3b9a5-117">Em um serviço de nuvem, uma função web fornece dos serviços de informações da Internet (IIS) web server toohost front-end da web dedicado aplicativos, enquanto uma função de trabalho pode executar assíncronas, demoradas ou permanentes tarefas independentes da interação do usuário ou entrada.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="3b9a5-118">Para saber mais, confira [O que é um Serviço de Nuvem?].</span><span class="sxs-lookup"><span data-stu-id="3b9a5-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="3b9a5-119">*Procurando toobuild um site simples?*</span><span class="sxs-lookup"><span data-stu-id="3b9a5-119">*Looking toobuild a simple website?*</span></span>
> <span data-ttu-id="3b9a5-120">Se seu cenário envolve apenas um site simples front-end, considere o uso de recursos de aplicativos Web leves Olá no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-120">If your scenario involves just a simple website front end, consider using hello lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="3b9a5-121">É possível atualizar facilmente tooa serviço de nuvem que seu site cresce e suas necessidades mudam.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-121">You can easily upgrade tooa Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="3b9a5-122">Consulte Olá <a href="/develop/python/">Central de desenvolvedores de Python</a> para artigos que abordam o desenvolvimento de recursos de aplicativos Web Olá no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-122">See hello <a href="/develop/python/">Python Developer Center</a> for articles that cover development of hello Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="3b9a5-123">Criação do projeto</span><span class="sxs-lookup"><span data-stu-id="3b9a5-123">Project creation</span></span>
<span data-ttu-id="3b9a5-124">No Visual Studio, você pode selecionar **serviço de nuvem do Azure** em Olá **novo projeto** caixa de diálogo **Python**.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-124">In Visual Studio, you can select **Azure Cloud Service** in hello **New Project** dialog box, under **Python**.</span></span>

![Caixa de diálogo Novo Projeto](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="3b9a5-126">No Assistente de serviço de nuvem do Azure hello, você pode criar uma nova web e funções de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-126">In hello Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Caixa de diálogo de serviço de nuvem do Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="3b9a5-128">modelo de função de trabalho Olá vem com clichê código tooconnect tooan conta de armazenamento do Azure ou Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-128">hello worker role template comes with boilerplate code tooconnect tooan Azure storage account or Azure Service Bus.</span></span>

![Solução de serviço de nuvem](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="3b9a5-130">Você pode adicionar a web ou trabalho funções tooan serviço de nuvem existente a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-130">You can add web or worker roles tooan existing cloud service at any time.</span></span>  <span data-ttu-id="3b9a5-131">Você pode escolher tooadd os projetos existentes de sua solução, ou criar novos.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-131">You can choose tooadd existing projects in your solution, or create new ones.</span></span>

![Adicionar comando de função](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="3b9a5-133">Seu serviço de nuvem pode conter funções implementadas em diferentes idiomas.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="3b9a5-134">Por exemplo, uma função Web do Python pode ser implementada usando o Django, com funções de trabalho do Python ou do C#.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="3b9a5-135">Você pode se comunicar facilmente entre as funções usando filas do Barramento de Serviço ou filas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-hello-cloud-service"></a><span data-ttu-id="3b9a5-136">Instalar o Python no serviço de nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="3b9a5-136">Install Python on hello cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="3b9a5-137">Olá scripts de instalação que são instalados com o Visual Studio (em tempo de saudação que este artigo foi atualizado pela última) não funcionam.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-137">hello setup scripts that are installed with Visual Studio (at hello time this article was last updated) do not work.</span></span> <span data-ttu-id="3b9a5-138">Esta seção descreve uma solução alternativa.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="3b9a5-139">Olá principal problema com scripts de instalação Olá é que eles não instale python.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-139">hello main problem with hello setup scripts is that they do not install python.</span></span> <span data-ttu-id="3b9a5-140">Primeiro, definir dois [tarefas de inicialização](cloud-services-startup-tasks.md) em Olá [servicedefinition. Csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) arquivo.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="3b9a5-141">primeira tarefa de saudação (**PrepPython.ps1**) baixa e instala o tempo de execução do Python hello.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-141">hello first task (**PrepPython.ps1**) downloads and installs hello Python runtime.</span></span> <span data-ttu-id="3b9a5-142">tarefa de segundo Hello (**PipInstaller.ps1**) executa pip tooinstall quaisquer dependências, você pode ter.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-142">hello second task (**PipInstaller.ps1**) runs pip tooinstall any dependencies you may have.</span></span>

<span data-ttu-id="3b9a5-143">Olá scripts a seguir foram escrita destinados Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-143">hello following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="3b9a5-144">Se você quiser toouse Olá versão 2. x do python, Olá conjunto **PYTHON2** variável arquivo muito**na** para tarefas de inicialização Olá dois e tarefas de tempo de execução Olá: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-144">If you want toouse hello version 2.x of python, set hello **PYTHON2** variable file too**on** for hello two startup tasks and hello runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

```xml
<Startup>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>
  </Task>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>

  </Task>

</Startup>
```

<span data-ttu-id="3b9a5-145">Olá **PYTHON2** e **PYPATH** variáveis devem ser adicionadas a tarefa de inicialização de trabalho toohello.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-145">hello **PYTHON2** and **PYPATH** variables must be added toohello worker startup task.</span></span> <span data-ttu-id="3b9a5-146">Olá **PYPATH** variável só é usada se hello **PYTHON2** variável for definida muito**em**.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-146">hello **PYPATH** variable is only used if hello **PYTHON2** variable is set too**on**.</span></span>

```xml
<Runtime>
  <Environment>
    <Variable name="EMULATED">
      <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
    </Variable>
    <Variable name="PYTHON2" value="off" />
    <Variable name="PYPATH" value="%SystemDrive%\Python27" />
  </Environment>
  <EntryPoint>
    <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
  </EntryPoint>
</Runtime>
```

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="3b9a5-147">ServiceDefinition.csdef de exemplo</span><span class="sxs-lookup"><span data-stu-id="3b9a5-147">Sample ServiceDefinition.csdef</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="AzureCloudServicePython" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
      <Setting name="Python2" />
    </ConfigurationSettings>
    <Startup>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="EMULATED">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
        </Variable>
        <Variable name="PYTHON2" value="off" />
        <Variable name="PYPATH" value="%SystemDrive%\Python27" />
      </Environment>
      <EntryPoint>
        <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
      </EntryPoint>
    </Runtime>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
  </WorkerRole>
</ServiceDefinition>
```



<span data-ttu-id="3b9a5-148">Em seguida, crie Olá **PrepPython.ps1** e **PipInstaller.ps1** arquivos Olá **. / bin** pasta de sua função.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-148">Next, create hello **PrepPython.ps1** and **PipInstaller.ps1** files in hello **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="3b9a5-149">PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="3b9a5-149">PrepPython.ps1</span></span>
<span data-ttu-id="3b9a5-150">Esse script instala o python.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-150">This script installs python.</span></span> <span data-ttu-id="3b9a5-151">Se hello **PYTHON2** variável de ambiente é definida muito**em**, Python 2.7 é instalado, caso contrário, o Python 3.5 está instalado.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-151">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if python is installed...$nl"
    if ($is_python2) {
        & "${env:SystemDrive}\Python27\python.exe"  -V | Out-Null
    }
    else {
        py -V | Out-Null
    }

    if (-not $?) {

        $url = "https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe"
        $outFile = "${env:TEMP}\python-3.5.2-amd64.exe"

        if ($is_python2) {
            $url = "https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64.msi"
            $outFile = "${env:TEMP}\python-2.7.12.amd64.msi"
        }

        Write-Output "Not found, downloading $url too$outFile$nl"
        Invoke-WebRequest $url -OutFile $outFile
        Write-Output "Installing$nl"

        if ($is_python2) {
            Start-Process msiexec.exe -ArgumentList "/q", "/i", "$outFile", "ALLUSERS=1" -Wait
        }
        else {
            Start-Process "$outFile" -ArgumentList "/quiet", "InstallAllUsers=1" -Wait
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Already installed"
    }
}
```

#### <a name="pipinstallerps1"></a><span data-ttu-id="3b9a5-152">PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="3b9a5-152">PipInstaller.ps1</span></span>
<span data-ttu-id="3b9a5-153">Esse script chama o pip e instala todas as dependências de saudação em Olá **requirements.txt** arquivo.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-153">This script calls up pip and installs all of hello dependencies in hello **requirements.txt** file.</span></span> <span data-ttu-id="3b9a5-154">Se hello **PYTHON2** variável de ambiente é definida muito**em**, Python 2.7 é usado, caso contrário, o Python 3.5 é usado.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-154">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if requirements.txt exists$nl"
    if (Test-Path ..\requirements.txt) {
        Write-Output "Found. Processing pip$nl"

        if ($is_python2) {
            & "${env:SystemDrive}\Python27\python.exe" -m pip install -r ..\requirements.txt
        }
        else {
            py -m pip install -r ..\requirements.txt
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Not found$nl"
    }
}
```

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="3b9a5-155">Modificar LaunchWorker.ps1</span><span class="sxs-lookup"><span data-stu-id="3b9a5-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="3b9a5-156">No caso de saudação de um **função de trabalho** projeto, **LauncherWorker.ps1** é arquivo de inicialização de saudação tooexecute necessária.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-156">In hello case of a **worker role** project, **LauncherWorker.ps1** file is required tooexecute hello startup file.</span></span> <span data-ttu-id="3b9a5-157">Em um **função web** projeto, hello arquivo de inicialização será em vez disso, definido nas propriedades do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-157">In a **web role** project, hello startup file is instead defined in hello project properties.</span></span>
> 
> 

<span data-ttu-id="3b9a5-158">Olá **bin\LaunchWorker.ps1** toodo muito trabalho de preparação, mas ele não funciona realmente foi criado.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-158">hello **bin\LaunchWorker.ps1** was originally created toodo a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="3b9a5-159">Substitua o conteúdo de saudação nesse arquivo com hello script a seguir.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-159">Replace hello contents in that file with hello following script.</span></span>

<span data-ttu-id="3b9a5-160">Esse script chama Olá **worker.py** arquivo do seu projeto de python.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-160">This script calls hello **worker.py** file from your python project.</span></span> <span data-ttu-id="3b9a5-161">Se hello **PYTHON2** variável de ambiente é definida muito**em**, Python 2.7 é usado, caso contrário, o Python 3.5 é usado.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-161">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated)
{
    Write-Output "Running worker.py$nl"

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
else
{
    Write-Output "Running (EMULATED) worker.py$nl"

    # Customize tooyour local dev environment

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
```

#### <a name="pscmd"></a><span data-ttu-id="3b9a5-162">ps.cmd</span><span class="sxs-lookup"><span data-stu-id="3b9a5-162">ps.cmd</span></span>
<span data-ttu-id="3b9a5-163">modelos do Visual Studio Olá devem ter criado um **ps.cmd** arquivo hello **. / bin** pasta.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-163">hello Visual Studio templates should have created a **ps.cmd** file in hello **./bin** folder.</span></span> <span data-ttu-id="3b9a5-164">Esse script de shell chama Olá PowerShell scripts de wrapper acima e fornece registro em log com base no nome de saudação do wrapper do PowerShell Olá chamado.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-164">This shell script calls out hello PowerShell wrapper scripts above and provides logging based on hello name of hello PowerShell wrapper called.</span></span> <span data-ttu-id="3b9a5-165">Se esse arquivo não tiver sido criado, veja qual deve ser seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="3b9a5-166">Executar localmente</span><span class="sxs-lookup"><span data-stu-id="3b9a5-166">Run locally</span></span>
<span data-ttu-id="3b9a5-167">Se você definir o seu projeto de serviço de nuvem como projeto de inicialização hello e pressione F5, o serviço de nuvem Olá é executado no emulador do Azure local hello.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-167">If you set your cloud service project as hello startup project and press F5, hello cloud service runs in hello local Azure emulator.</span></span>

<span data-ttu-id="3b9a5-168">Embora PTVS dá suporte ao iniciar no emulador hello, depuração (por exemplo, pontos de interrupção) não funciona.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-168">Although PTVS supports launching in hello emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="3b9a5-169">toodebug suas funções web e de trabalho, você pode definir o projeto de função hello como projeto de inicialização hello e que, em vez de depuração.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-169">toodebug your web and worker roles, you can set hello role project as hello startup project and debug that instead.</span></span>  <span data-ttu-id="3b9a5-170">Você também pode definir vários projetos de inicialização.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="3b9a5-171">Solução de saudação e, em seguida, selecione **definir projetos de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-171">Right-click hello solution and then select **Set StartUp Projects**.</span></span>

![Propriedades do projeto de inicialização da solução](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a><span data-ttu-id="3b9a5-173">Publicar tooAzure</span><span class="sxs-lookup"><span data-stu-id="3b9a5-173">Publish tooAzure</span></span>
<span data-ttu-id="3b9a5-174">toopublish, projeto de serviço de nuvem Olá na solução hello e, em seguida, selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-174">toopublish, right-click hello cloud service project in hello solution and then select **Publish**.</span></span>

![Conexão de publicação no Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="3b9a5-176">Siga o Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-176">Follow hello wizard.</span></span> <span data-ttu-id="3b9a5-177">Se for necessário, habilite a área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="3b9a5-178">Área de trabalho remota é útil quando você precisa toodebug algo.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-178">Remote desktop is helpful when you need toodebug something.</span></span>

<span data-ttu-id="3b9a5-179">Quando tiver concluído os ajustes de configurações, clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="3b9a5-180">Algum progresso é exibido na janela de saída de hello, em seguida, você verá a janela de Log de atividades do Microsoft Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-180">Some progress appears in hello output window, then you'll see hello Microsoft Azure Activity Log window.</span></span>

![Janela Log de atividade do Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="3b9a5-182">Implantação usa toocomplete de vários minutos, em seguida, web e/ou funções de trabalho são executadas no Azure!</span><span class="sxs-lookup"><span data-stu-id="3b9a5-182">Deployment takes several minutes toocomplete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="3b9a5-183">Investigar os logs</span><span class="sxs-lookup"><span data-stu-id="3b9a5-183">Investigate logs</span></span>
<span data-ttu-id="3b9a5-184">Depois de máquina virtual na nuvem Olá serviço é iniciado e instala Python, você pode examinar Olá logs toofind quaisquer mensagens de falha.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-184">After hello cloud service virtual machine starts up and installs Python, you can look at hello logs toofind any failure messages.</span></span> <span data-ttu-id="3b9a5-185">Esses logs estão localizados em Olá **C:\Resources\Directory\\\LogFiles {função}** pasta.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-185">These logs are located in hello **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="3b9a5-186">**PrepPython.err.txt** exibe pelo menos um erro de quando o script hello tenta toodetect se Python é instalado e **PipInstaller.err.txt** pode reclamar sobre uma versão desatualizada de pip.</span><span class="sxs-lookup"><span data-stu-id="3b9a5-186">**PrepPython.err.txt** has at least one error in it from when hello script tries toodetect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b9a5-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b9a5-187">Next steps</span></span>
<span data-ttu-id="3b9a5-188">Para obter mais informações sobre como trabalhar com funções web e de trabalho em ferramentas Python para Visual Studio, consulte a documentação de PTVS de saudação:</span><span class="sxs-lookup"><span data-stu-id="3b9a5-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see hello PTVS documentation:</span></span>

* <span data-ttu-id="3b9a5-189">[Projetos do Serviço de Nuvem][Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="3b9a5-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="3b9a5-190">Para obter mais detalhes sobre como usar os serviços do Azure em suas funções web e de trabalho, como o uso do armazenamento do Azure ou barramento de serviço, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3b9a5-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see hello following articles:</span></span>

* <span data-ttu-id="3b9a5-191">[Serviço Blob][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="3b9a5-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="3b9a5-192">[Serviço Tabela][Table Service]</span><span class="sxs-lookup"><span data-stu-id="3b9a5-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="3b9a5-193">[Serviço Fila][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="3b9a5-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="3b9a5-194">[Filas de Barramento de Serviço][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="3b9a5-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="3b9a5-195">[Tópicos do Barramento de Serviço][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="3b9a5-195">[Service Bus Topics][Service Bus Topics]</span></span>

<!--Link references-->

[O que é um Serviço de Nuvem?]: cloud-services-choose-me.md
[execution model-web sites]: ../app-service-web/app-service-web-overview.md
[execution model-vms]:../virtual-machines/windows/overview.md
[execution model-cloud services]: cloud-services-choose-me.md
[Python Developer Center]: /develop/python/

[Blob Service]:../storage/blobs/storage-python-how-to-use-blob-storage.md
[Queue Service]: ../storage/queues/storage-python-how-to-use-queue-storage.md
[Table Service]:../cosmos-db/table-storage-how-to-use-python.md
[Service Bus Queues]: ../service-bus-messaging/service-bus-python-how-to-use-queues.md
[Service Bus Topics]: ../service-bus-messaging/service-bus-python-how-to-use-topics-subscriptions.md


<!--External Link references-->

[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure SDK Tools for VS 2013]: http://go.microsoft.com/fwlink/?LinkId=746482
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=746481
[Azure SDK Tools for VS 2017]: http://go.microsoft.com/fwlink/?LinkId=746483
[Python 2.7 32-bit]: https://www.python.org/downloads/
[Python 3.5 32-bit]: https://www.python.org/downloads/
