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
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a>Funções Web e de trabalho do Python com Ferramentas Python para Visual Studio

Este artigo oferece uma visão geral do uso das funções Web e de trabalho do Python por meio das [Ferramentas do Python para Visual Studio][Python Tools for Visual Studio]. Saiba como toouse Visual Studio toocreate e implantar um serviço de nuvem básico que usa o Python.

## <a name="prerequisites"></a>Pré-requisitos
* [Visual Studio 2013, 2015 ou 2017](https://www.visualstudio.com/)
* [Ferramentas do Python para Visual Studio][Python Tools for Visual Studio] (PTVS)
* [Ferramentas do SDK do Azure para VS 2013][Azure SDK Tools for VS 2013] ou  
[Ferramentas do SDK do Azure para VS 2015][Azure SDK Tools for VS 2015] ou  
[Ferramentas do SDK do Azure para VS 2017][Azure SDK Tools for VS 2017]
* [Python 2.7 de 32 bits][Python 2.7 32-bit] ou [Python 3.5 de 32 bits][Python 3.5 32-bit]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a>O que são funções Web e de Trabalho do Python?
O Azure fornece três modelos de computação para a execução de aplicativos: [Recurso de Aplicativos Web no Serviço de Aplicativo do Azure][execution model-web sites], [Máquinas Virtuais do Azure][execution model-vms] e [Serviços de Nuvem do Azure][execution model-cloud services]. Todos os três modelos oferecem suporte ao Python. Os Serviços de Nuvem, que incluem as funções Web e de trabalho, fornecem a *PaaS (plataforma como serviço)*. Em um serviço de nuvem, uma função web fornece dos serviços de informações da Internet (IIS) web server toohost front-end da web dedicado aplicativos, enquanto uma função de trabalho pode executar assíncronas, demoradas ou permanentes tarefas independentes da interação do usuário ou entrada.

Para saber mais, confira [O que é um Serviço de Nuvem?].

> [!NOTE]
> *Procurando toobuild um site simples?*
> Se seu cenário envolve apenas um site simples front-end, considere o uso de recursos de aplicativos Web leves Olá no serviço de aplicativo do Azure. É possível atualizar facilmente tooa serviço de nuvem que seu site cresce e suas necessidades mudam. Consulte Olá <a href="/develop/python/">Central de desenvolvedores de Python</a> para artigos que abordam o desenvolvimento de recursos de aplicativos Web Olá no serviço de aplicativo do Azure.
> <br />
> 
> 

## <a name="project-creation"></a>Criação do projeto
No Visual Studio, você pode selecionar **serviço de nuvem do Azure** em Olá **novo projeto** caixa de diálogo **Python**.

![Caixa de diálogo Novo Projeto](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

No Assistente de serviço de nuvem do Azure hello, você pode criar uma nova web e funções de trabalho.

![Caixa de diálogo de serviço de nuvem do Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

modelo de função de trabalho Olá vem com clichê código tooconnect tooan conta de armazenamento do Azure ou Azure Service Bus.

![Solução de serviço de nuvem](./media/cloud-services-python-ptvs/worker.png)

Você pode adicionar a web ou trabalho funções tooan serviço de nuvem existente a qualquer momento.  Você pode escolher tooadd os projetos existentes de sua solução, ou criar novos.

![Adicionar comando de função](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

Seu serviço de nuvem pode conter funções implementadas em diferentes idiomas.  Por exemplo, uma função Web do Python pode ser implementada usando o Django, com funções de trabalho do Python ou do C#.  Você pode se comunicar facilmente entre as funções usando filas do Barramento de Serviço ou filas de armazenamento.

## <a name="install-python-on-hello-cloud-service"></a>Instalar o Python no serviço de nuvem Olá
> [!WARNING]
> Olá scripts de instalação que são instalados com o Visual Studio (em tempo de saudação que este artigo foi atualizado pela última) não funcionam. Esta seção descreve uma solução alternativa.
> 
> 

Olá principal problema com scripts de instalação Olá é que eles não instale python. Primeiro, definir dois [tarefas de inicialização](cloud-services-startup-tasks.md) em Olá [servicedefinition. Csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) arquivo. primeira tarefa de saudação (**PrepPython.ps1**) baixa e instala o tempo de execução do Python hello. tarefa de segundo Hello (**PipInstaller.ps1**) executa pip tooinstall quaisquer dependências, você pode ter.

Olá scripts a seguir foram escrita destinados Python 3.5. Se você quiser toouse Olá versão 2. x do python, Olá conjunto **PYTHON2** variável arquivo muito**na** para tarefas de inicialização Olá dois e tarefas de tempo de execução Olá: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.

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

Olá **PYTHON2** e **PYPATH** variáveis devem ser adicionadas a tarefa de inicialização de trabalho toohello. Olá **PYPATH** variável só é usada se hello **PYTHON2** variável for definida muito**em**.

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

#### <a name="sample-servicedefinitioncsdef"></a>ServiceDefinition.csdef de exemplo
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



Em seguida, crie Olá **PrepPython.ps1** e **PipInstaller.ps1** arquivos Olá **. / bin** pasta de sua função.

#### <a name="preppythonps1"></a>PrepPython.ps1
Esse script instala o python. Se hello **PYTHON2** variável de ambiente é definida muito**em**, Python 2.7 é instalado, caso contrário, o Python 3.5 está instalado.

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

#### <a name="pipinstallerps1"></a>PipInstaller.ps1
Esse script chama o pip e instala todas as dependências de saudação em Olá **requirements.txt** arquivo. Se hello **PYTHON2** variável de ambiente é definida muito**em**, Python 2.7 é usado, caso contrário, o Python 3.5 é usado.

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

#### <a name="modify-launchworkerps1"></a>Modificar LaunchWorker.ps1
> [!NOTE]
> No caso de saudação de um **função de trabalho** projeto, **LauncherWorker.ps1** é arquivo de inicialização de saudação tooexecute necessária. Em um **função web** projeto, hello arquivo de inicialização será em vez disso, definido nas propriedades do projeto hello.
> 
> 

Olá **bin\LaunchWorker.ps1** toodo muito trabalho de preparação, mas ele não funciona realmente foi criado. Substitua o conteúdo de saudação nesse arquivo com hello script a seguir.

Esse script chama Olá **worker.py** arquivo do seu projeto de python. Se hello **PYTHON2** variável de ambiente é definida muito**em**, Python 2.7 é usado, caso contrário, o Python 3.5 é usado.

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

#### <a name="pscmd"></a>ps.cmd
modelos do Visual Studio Olá devem ter criado um **ps.cmd** arquivo hello **. / bin** pasta. Esse script de shell chama Olá PowerShell scripts de wrapper acima e fornece registro em log com base no nome de saudação do wrapper do PowerShell Olá chamado. Se esse arquivo não tiver sido criado, veja qual deve ser seu conteúdo. 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a>Executar localmente
Se você definir o seu projeto de serviço de nuvem como projeto de inicialização hello e pressione F5, o serviço de nuvem Olá é executado no emulador do Azure local hello.

Embora PTVS dá suporte ao iniciar no emulador hello, depuração (por exemplo, pontos de interrupção) não funciona.

toodebug suas funções web e de trabalho, você pode definir o projeto de função hello como projeto de inicialização hello e que, em vez de depuração.  Você também pode definir vários projetos de inicialização.  Solução de saudação e, em seguida, selecione **definir projetos de inicialização**.

![Propriedades do projeto de inicialização da solução](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a>Publicar tooAzure
toopublish, projeto de serviço de nuvem Olá na solução hello e, em seguida, selecione **publicar**.

![Conexão de publicação no Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

Siga o Assistente de saudação. Se for necessário, habilite a área de trabalho remota. Área de trabalho remota é útil quando você precisa toodebug algo.

Quando tiver concluído os ajustes de configurações, clique em **Publicar**.

Algum progresso é exibido na janela de saída de hello, em seguida, você verá a janela de Log de atividades do Microsoft Azure Olá.

![Janela Log de atividade do Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

Implantação usa toocomplete de vários minutos, em seguida, web e/ou funções de trabalho são executadas no Azure!

### <a name="investigate-logs"></a>Investigar os logs
Depois de máquina virtual na nuvem Olá serviço é iniciado e instala Python, você pode examinar Olá logs toofind quaisquer mensagens de falha. Esses logs estão localizados em Olá **C:\Resources\Directory\\\LogFiles {função}** pasta. **PrepPython.err.txt** exibe pelo menos um erro de quando o script hello tenta toodetect se Python é instalado e **PipInstaller.err.txt** pode reclamar sobre uma versão desatualizada de pip.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como trabalhar com funções web e de trabalho em ferramentas Python para Visual Studio, consulte a documentação de PTVS de saudação:

* [Projetos do Serviço de Nuvem][Cloud Service Projects]

Para obter mais detalhes sobre como usar os serviços do Azure em suas funções web e de trabalho, como o uso do armazenamento do Azure ou barramento de serviço, consulte Olá artigos a seguir:

* [Serviço Blob][Blob Service]
* [Serviço Tabela][Table Service]
* [Serviço Fila][Queue Service]
* [Filas de Barramento de Serviço][Service Bus Queues]
* [Tópicos do Barramento de Serviço][Service Bus Topics]

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
