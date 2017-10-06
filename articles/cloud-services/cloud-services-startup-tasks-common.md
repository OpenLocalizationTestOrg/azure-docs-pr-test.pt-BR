---
title: "aaaCommon tarefas de inicialização para serviços de nuvem | Microsoft Docs"
description: "Fornece alguns exemplos comuns de tarefas de inicialização, convém tooperform em sua função de web de serviços de nuvem ou uma função de trabalho."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: a7095dad-1ee7-4141-bc6a-ef19a6e570f1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: c80fac4079439410dfc3795e4bce0fbc07dbbfab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="common-cloud-service-startup-tasks"></a>Tarefas de inicialização comuns do Serviço de Nuvem
Este artigo fornece alguns exemplos comuns de tarefas de inicialização seja tooperform em seu serviço de nuvem. Você pode usar operações de tooperform de tarefas de inicialização antes do início de uma função. Operações que convém tooperform incluem instalação de um componente, registrando componentes COM, chaves do registro de configuração ou iniciar um processo de execução longa. 

Consulte [neste artigo](cloud-services-startup-tasks.md) toounderstand como funcionam as tarefas de inicialização e, especificamente como toocreate Olá entradas que definem uma tarefa de inicialização.

> [!NOTE]
> Tarefas de inicialização não são aplicáveis tooVirtual máquinas, apenas tooCloud serviço Web e funções de trabalho.
> 

## <a name="define-environment-variables-before-a-role-starts"></a>Definir variáveis de ambiente antes de iniciar uma função
Se você precisar de variáveis de ambiente definidas para uma tarefa específica, use Olá [ambiente] elemento dentro Olá [tarefa] elemento.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
                <Environment>
                    <Variable name="MyEnvironmentVariable" value="MyVariableValue" />
                </Environment>
            </Task>
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

As variáveis também podem usar um [valor válido do Azure XPath](cloud-services-role-config-xpath.md) tooreference algo sobre implantação de saudação. Em vez de usar o hello `value` de atributo, defina um [RoleInstanceValue] elemento filho.

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a>Configurar a inicialização do IIS com AppCmd.exe
Olá [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) ferramenta de linha de comando pode ser usado toomanage configurações do IIS na inicialização no Azure. *AppCmd.exe* fornece acesso conveniente de linha de comando tooconfiguration configurações para uso nas tarefas de inicialização no Azure. Com *AppCmd.exe*, as configurações do site podem ser adicionadas, modificadas ou removidas para aplicativos e sites.

No entanto, há alguns toowatch de coisas out para usar Olá *AppCmd.exe* como uma tarefa de inicialização:

* As tarefas de inicialização podem ser executadas mais de uma vez entre as reinicializações. Por exemplo, quando uma função é reciclada.
* Se uma ação *AppCmd.exe* for executada mais de uma vez, poderá gerar um erro. Por exemplo, a tentativa de uma seção de tooadd muito*Web. config* duas vezes pode gerar um erro.
* As tarefas de inicialização falharão caso retornem um código de saída diferente de zero ou **errorlevel**. Por exemplo, quando *AppCmd.exe* gera um erro.

Saudação de toocheck uma boa prática é **errorlevel** depois de chamar *AppCmd.exe*, que é fácil toodo se encapsular chamada hello muito*AppCmd.exe* com um *. cmd*  arquivo. Se você detectar uma resposta **errorlevel** conhecida, poderá ignorá-la ou passá-la novamente.

Olá errorlevel retornado por *AppCmd.exe* são listados no arquivo de Winerror hello e também podem ser vistas na [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).

### <a name="example-of-managing-hello-error-level"></a>Exemplo de gerenciamento de nível de erro Olá
Este exemplo adiciona uma seção e uma entrada de compactação para JSON toohello *Web. config* arquivo com tratamento de erros e registro em log.

Olá seções relevantes do hello [servicedefinition. Csdef] arquivo são mostradas aqui, que incluem a definição de saudação [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) atributo muito`elevated` toogive *AppCmd.exe*  suficientes permissões toochange Olá configurações Olá *Web. config* arquivo:

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

Olá *Startup.cmd* em lotes de arquivos usa *AppCmd.exe* tooadd uma seção e uma entrada de compactação para JSON toohello *Web. config* arquivo. Olá esperado **errorlevel** de 183 é definido toozero usando Olá verificar. Programa de linha de comando do EXE. Os errorlevels inesperados são tooStartupErrorLog.txt conectado.

```cmd
REM   *** Add a compression section toohello Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying tooadd a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. toohandle this situation, set hello ERRORLEVEL toozero by using hello Verify command. hello Verify
REM   command will safely set hello ERRORLEVEL toozero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If hello ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding hello JSON compression type toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report hello date, time, and ERRORLEVEL of hello error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a>Adicionar regras de firewall
No Azure, há efetivamente dois firewalls. Olá primeiro firewall controla conexões entre máquina virtual de saudação e Olá fora do mundo. Esse firewall é controlado pelo Olá [pontos de extremidade] elemento Olá [servicedefinition. Csdef] arquivo.

Olá segundo firewall controla conexões entre máquinas virtuais de saudação e processos de saudação dentro dessa máquina virtual. Esse firewall pode ser controlado por Olá `netsh advfirewall firewall` ferramenta de linha de comando.

O Azure cria regras de firewall para Olá processos iniciados em suas funções. Por exemplo, quando você inicia um programa ou serviço, Azure cria automaticamente Olá tooallow de regras de firewall necessárias toocommunicate esse serviço com hello da Internet. No entanto, se você criar um serviço que é iniciado por um processo fora de sua função (como um serviço COM+ ou uma tarefa agendada do Windows), é necessário toomanually criar um serviço de toothat firewall regra tooallow acesso. Essas regras de firewall podem ser criadas usando uma tarefa de inicialização.

Uma tarefa de inicialização que cria uma regra de firewall deve ter um [executionContext][tarefa]  **elevado**. Adicionar Olá toohello da tarefa de inicialização a seguir [servicedefinition. Csdef] arquivo.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="AddFirewallRules.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

regra de firewall de saudação tooadd, você deve usar o hello apropriado `netsh advfirewall firewall` comandos no arquivo em lotes de inicialização. Neste exemplo, a tarefa de inicialização Olá requer segurança e criptografia para a porta TCP 80.

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a>Bloquear um endereço IP específico
Você pode restringir um conjunto de tooa de acesso de função web do Azure de endereços IP especificados alterando o IIS **Web. config** arquivo. Você também precisa toouse um arquivo de comando que desbloqueie Olá **ipSecurity** seção Olá **applicationHost. config** arquivo.

toodo desbloquear Olá **ipSecurity** seção Olá **applicationHost. config** de arquivo, crie um arquivo de comando que é executado no início da função. Crie uma pasta no nível de raiz de saudação de sua função web chamada **inicialização** e, dentro dessa pasta, crie um arquivo em lotes chamado **startup.cmd**. Adicionar este projeto do Visual Studio tooyour arquivo e definir propriedades de saudação muito**copiar sempre** tooensure que ele está incluído no pacote.

Adicionar Olá toohello da tarefa de inicialização a seguir [servicedefinition. Csdef] arquivo.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WebRole name="WebRole1">
        ...
        <Startup>
            <Task commandLine="startup.cmd" executionContext="elevated" />
        </Startup>
    </WebRole>
</ServiceDefinition>
```

Adicionar este comando toohello **startup.cmd** arquivo:

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

Esta tarefa faz com que Olá **startup.cmd** toobe arquivo seja executado sempre que a função da web de saudação é inicializada, garantindo que Olá necessárias do lote **ipSecurity** seção está desbloqueada.

Finalmente, modifique Olá [seção System. webServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) da sua função web **Web. config** arquivo tooadd uma lista de endereços IP que têm acesso, conforme mostrado no exemplo a seguir de saudação:

Essa configuração de exemplo **permite** tooaccess de todos os IPs Olá servidor exceto Olá dois definido

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--hello following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

Essa configuração de exemplo **nega** todos os IPs acessem servidor hello, exceto Olá dois definido.

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--hello following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a>Criar uma tarefa de inicialização do PowerShell
Scripts do Windows PowerShell não podem ser chamados diretamente no hello [servicedefinition. Csdef] arquivo, mas pode ser chamado de dentro de um arquivo em lotes de inicialização.

O PowerShell (por padrão) não executa scripts não assinados. A menos que você assinar o script, você precisa tooconfigure PowerShell toorun de scripts não assinados. toorun scripts não assinados, hello **ExecutionPolicy** deve ser definido muito**irrestrito**. Olá **ExecutionPolicy** configuração que você usa é baseada na versão de saudação do Windows PowerShell.

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

Se você estiver usando um sistema operacional convidado que for executar o PowerShell 2.0 ou 1.0, você pode forçar a toorun versão 2 e se não estiver disponível, use a versão 1.

```cmd
REM   Attempt tooset hello execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set hello execution policy by using hello PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a>Criar arquivos no armazenamento local de uma tarefa de inicialização
Você pode usar um toostore de recursos de armazenamento local arquivos criados por sua tarefa de inicialização que é acessada posteriormente por seu aplicativo.

toocreate Olá o recurso de armazenamento local, adicione uma [LocalResources] seção toohello [servicedefinition. Csdef] de arquivo e, em seguida, adicione Olá [LocalStorage] elemento filho. Fornecer recursos de armazenamento local de saudação um nome exclusivo e um tamanho apropriado para sua tarefa de inicialização.

toouse um recurso de armazenamento local em sua tarefa de inicialização, é necessário toocreate um local de recursos do ambiente variável tooreference Olá armazenamento local. Olá, em seguida, a tarefa de inicialização e aplicativo hello são tooread capaz de gravar o recurso de armazenamento local de toohello de arquivos.

Olá seções relevantes do hello **servicedefinition. Csdef** arquivo são mostradas aqui:

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">
    ...

    <LocalResources>
      <LocalStorage name="StartupLocalStorage" sizeInMB="5"/>
    </LocalResources>

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="PathToStartupStorage">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
  </WorkerRole>
</ServiceDefinition>
```

Por exemplo, isso **Startup.cmd** arquivo em lotes usa Olá **PathToStartupStorage** arquivo hello do ambiente variável toocreate **MyTest.txt** no armazenamento local de saudação local.

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

Você pode acessar a pasta de armazenamento local de saudação do SDK do Azure usando Olá [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) método.

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a>Executar no emulador de saudação ou nuvem
Você pode ter sua tarefa de inicialização executar etapas diferentes ao operar em Olá nuvem quando comparada toowhen é no emulador de computação hello. Por exemplo, convém toouse uma cópia atualizada dos dados do SQL somente quando em execução no emulador de saudação. Ou talvez você queira toodo algumas otimizações de desempenho para a nuvem de saudação que você não precisa toodo quando em execução no emulador de saudação.

Este tooperform capacidade diferente ações em Olá emulador de computação e Olá nuvem pode ser realizada por meio da criação de uma variável de ambiente no hello [servicedefinition. Csdef] arquivo. Você testa então essa variável de ambiente para um valor em sua tarefa de inicialização.

variável de ambiente toocreate Olá adicionar Olá [variável]/[RoleInstanceValue] elemento e crie um valor de XPath do `/RoleEnvironment/Deployment/@emulated`. Olá valor Olá **ComputeEmulatorRunning %** variável de ambiente é `true` quando em execução no emulador de computação Olá, e `false` quando em execução na nuvem hello.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">

    ...

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>

  </WorkerRole>
</ServiceDefinition>
```

tarefa Olá agora pode verificar Olá **ComputeEmulatorRunning %** ações diferentes de tooperform variável de ambiente com base em se a função hello está sendo executado no hello nuvem ou Olá emulador. A seguir, um script de shell .cmd que verifica essa variável de ambiente.

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a>Detectar se a tarefa já foi executada
função Hello pode reciclar sem uma reinicialização, causando o toorun de tarefas de inicialização novamente. Não há nenhum tooindicate de sinalizador que uma tarefa já executada em Olá hospeda a VM. Talvez você tenha algumas tarefas onde não importará se elas forem executadas várias vezes. No entanto, você pode executar em uma situação em que você precisa tooprevent uma tarefa de execução mais de uma vez.

toodetect forma mais simples Olá que uma tarefa já foi executado é toocreate um arquivo em Olá **% TEMP %** pasta quando a tarefa de saudação é bem-sucedida e examinar para ele Olá iniciam tarefa hello. A seguir, um script de shell cmd de exemplo que faz isso para você.

```cmd
REM   If Task1_Success.txt exists, then Application 1 is already installed.
IF EXIST "%RoleRoot%\Task1_Success.txt" (
  ECHO Application 1 is already installed. Exiting. >> "%TEMP%\StartupLog.txt" 2>&1
  GOTO Finish
)

REM   Run your real exe task
ECHO Running XYZ >> "%TEMP%\StartupLog.txt" 2>&1
"%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (
  REM   hello application installed without error. Create a file tooindicate that hello task
  REM   does not need toobe run again.

  ECHO This line will create a file tooindicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log hello error and exit with hello error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a>Práticas recomendadas para tarefas
A seguir, algumas práticas recomendadas que você deve seguir ao configurar a tarefa para sua função Web ou de trabalho.

### <a name="always-log-startup-activities"></a>Sempre registrar em log as atividades de inicialização
Visual Studio não fornece toostep um depurador por meio de arquivos em lotes, portanto é bom tooget todos os dados na operação de saudação dos arquivos em lotes possível. Log de saída de hello dos arquivos em lotes, ambos **stdout** e **stderr**, pode fornecer informações importantes durante a tentativa de toodebug e corrigir arquivos em lotes. toolog ambas as **stdout** e **stderr** toohello um arquivo StartupLog.txt no Olá Olá de tooby apontada diretório **% TEMP %** variável de ambiente, adicione o texto de saudação `>>  "%TEMP%\\StartupLog.txt" 2>&1`toohello final de específicos linhas que você deseja toolog. Por exemplo, tooexecute setup.exe em Olá **% PathToApp1Install %** diretório:

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

toosimplify o xml, você pode criar um wrapper *cmd* arquivo que chama todos sua inicialização tarefas juntamente com o registro em log e garante Olá de compartilhamentos cada tarefa filho mesmas variáveis de ambiente.

Você pode descobrir que embora irritantes toouse `>> "%TEMP%\StartupLog.txt" 2>&1` no final de saudação de cada tarefa de inicialização. Você pode impor o log de tarefas criando um invólucro que manipula o registro em log para você. Esse wrapper chama o arquivo de lote real Olá desejado toorun. Nenhuma saída do arquivo de lote de destino Olá será redirecionado toohello *Startuplog.txt* arquivo.

saudação de exemplo a seguir mostra como tooredirect todas as saídas de um arquivo em lotes de inicialização. Neste exemplo, o arquivo de Serverdefinition Olá cria uma tarefa de inicialização que chama *logwrap.cmd*. *logwrap.cmd* chamadas *Startup2.cmd*, redirecionando a saída de todos os demais**% TEMP %\\StartupLog.txt**.

ServiceDefinition.cmd:

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

**logwrap.cmd:**

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output toohello StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call hello child command batch file, redirecting all output toohello StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log hello completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log hello error.
   ECHO [%date% %time%] An error occurred. hello ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

**Startup2.cmd:**

```cmd
@ECHO OFF

REM   This is hello batch file where hello startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in hello directory pointed tooby hello TEMP environment variable.

REM   If an error occurs, hello following command will pass hello ERRORLEVEL back toothe
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

Exemplo de saída em Olá **StartupLog.txt** arquivo:

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> Olá **StartupLog.txt** arquivo está localizado em Olá *C:\Resources\temp\\\RoleTemp {identificador de função}* pasta.
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a>Definir executionContext adequadamente para tarefas de inicialização
Definir privilégios corretamente para a tarefa de inicialização de saudação. Às vezes, as tarefas de inicialização devem executar com privilégios elevados, mesmo que a função hello é executado com privilégios normais.

Olá [executionContext][tarefa] atributo define o nível de privilégio de saudação da tarefa de inicialização de saudação. Usando `executionContext="limited"` significa tem de tarefa de inicialização Olá Olá mesmo nível de privilégio como função hello. Usando `executionContext="elevated"` significa a tarefa de inicialização Olá tem privilégios de administrador, que permite inicialização Olá tarefa tooperform tarefas de administrador sem conceder função tooyour de privilégios de administrador.

Um exemplo de uma tarefa de inicialização que exige privilégios elevados é uma tarefa de inicialização que usa **AppCmd.exe** tooconfigure IIS. **AppCmd.exe** requer `executionContext="elevated"`.

### <a name="use-hello-appropriate-tasktype"></a>Use o taskType apropriado Olá
Olá [taskType][tarefa] atributo determina a tarefa de inicialização de Olá Olá maneira é executada. Há três valores: **simples**, **segundo plano** e **primeiro plano**. Olá tarefas primeiro e segundo plano são iniciadas assincronamente, e, em seguida, tarefas simples Olá são executadas de forma síncrona um de cada vez.

Com **simples** tarefas de inicialização, em que você pode definir a ordem hello, no qual executar tarefas de saudação pela ordem Olá no qual Olá tarefas estão listadas no arquivo servicedefinition. Csdef de saudação. Se um **simples** tarefa termina com diferente de zero código de saída, em seguida, Olá paradas do procedimento de inicialização e função hello não iniciar.

Olá diferença entre **em segundo plano** tarefas de inicialização e **primeiro plano** é que as tarefas de inicialização **primeiro plano** tarefas manter a execução da função de Olá até Olá  **primeiro plano** terminar. Isso também significa que se hello **primeiro plano** tarefa congelar ou falhas, a função hello não será reciclada até Olá **primeiro plano** tarefa é forçada fechado. Por esse motivo, **em segundo plano** tarefas são recomendadas para tarefas de inicialização assíncronas, a menos que você precise do recurso de saudação **primeiro plano** tarefa.

### <a name="end-batch-files-with-exit-b-0"></a>Encerrar arquivos em lotes com EXIT /B 0
Olá função começará somente se hello **errorlevel** de cada um dos seu inicialização simple tarefa é zero. Nem todos os programas definem Olá **errorlevel** (código de saída) corretamente, portanto o arquivo de lote Olá deve terminar com um `EXIT /B 0` se tudo foi executado corretamente.

A ausência de um `EXIT /B 0` em Olá final de um arquivo em lotes de inicialização é uma causa comum de funções que não são iniciados.

> [!NOTE]
> Eu já ter notado que lote aninhado arquivos de suspensão, às vezes, ao usar o hello `/B` parâmetro. Talvez você queira toomake-se de que esse problema de suspensão não ocorre se o outro arquivo em lotes chama o arquivo em lotes atual, como se você usar o hello [wrapper de log](#always-log-startup-activities). Você pode omitir Olá `/B` parâmetro nesse caso.
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a>Esperar toorun de tarefas de inicialização mais de uma vez
Nem todas as reciclagens de função incluem uma reinicialização, mas todas as reciclagens incluem a execução de todas as tarefas de inicialização. Isso significa que as tarefas de inicialização devem ser capaz de toorun várias vezes entre reinicializações sem problemas. Isso é discutido em Olá [anterior seção](#detect-that-your-task-has-already-run).

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a>Usar arquivos de toostore de armazenamento local que devem ser acessados na função hello
Se você deseja toocopy ou cria um arquivo durante sua tarefa de inicialização que é acessível tooyour função, esse arquivo deve ser colocado no armazenamento local. Consulte Olá [anterior seção](#create-files-in-local-storage-from-a-startup-task).

## <a name="next-steps"></a>Próximas etapas
Examine a nuvem Olá [modelo e o pacote de serviço](cloud-services-model-and-package.md)

Saiba mais sobre o funcionamento de [Tarefas](cloud-services-startup-tasks.md) .

[Crie e implante](cloud-services-how-to-create-deploy-portal.md) seu pacote de serviço de nuvem.

[servicedefinition. Csdef]: cloud-services-model-and-package.md#csdef
[tarefa]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[ambiente]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[variável]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
[EndPoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints
[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage
[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
