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
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="75fda-103">Tarefas de inicialização comuns do Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="75fda-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="75fda-104">Este artigo fornece alguns exemplos comuns de tarefas de inicialização seja tooperform em seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="75fda-104">This article provides some examples of common startup tasks you may want tooperform in your cloud service.</span></span> <span data-ttu-id="75fda-105">Você pode usar operações de tooperform de tarefas de inicialização antes do início de uma função.</span><span class="sxs-lookup"><span data-stu-id="75fda-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="75fda-106">Operações que convém tooperform incluem instalação de um componente, registrando componentes COM, chaves do registro de configuração ou iniciar um processo de execução longa.</span><span class="sxs-lookup"><span data-stu-id="75fda-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="75fda-107">Consulte [neste artigo](cloud-services-startup-tasks.md) toounderstand como funcionam as tarefas de inicialização e, especificamente como toocreate Olá entradas que definem uma tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="75fda-107">See [this article](cloud-services-startup-tasks.md) toounderstand how startup tasks work, and specifically how toocreate hello entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="75fda-108">Tarefas de inicialização não são aplicáveis tooVirtual máquinas, apenas tooCloud serviço Web e funções de trabalho.</span><span class="sxs-lookup"><span data-stu-id="75fda-108">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="75fda-109">Definir variáveis de ambiente antes de iniciar uma função</span><span class="sxs-lookup"><span data-stu-id="75fda-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="75fda-110">Se você precisar de variáveis de ambiente definidas para uma tarefa específica, use Olá [ambiente] elemento dentro Olá [tarefa] elemento.</span><span class="sxs-lookup"><span data-stu-id="75fda-110">If you need environment variables defined for a specific task, use hello [Environment] element inside hello [Task] element.</span></span>

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

<span data-ttu-id="75fda-111">As variáveis também podem usar um [valor válido do Azure XPath](cloud-services-role-config-xpath.md) tooreference algo sobre implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="75fda-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) tooreference something about hello deployment.</span></span> <span data-ttu-id="75fda-112">Em vez de usar o hello `value` de atributo, defina um [RoleInstanceValue] elemento filho.</span><span class="sxs-lookup"><span data-stu-id="75fda-112">Instead of using hello `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="75fda-113">Configurar a inicialização do IIS com AppCmd.exe</span><span class="sxs-lookup"><span data-stu-id="75fda-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="75fda-114">Olá [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) ferramenta de linha de comando pode ser usado toomanage configurações do IIS na inicialização no Azure.</span><span class="sxs-lookup"><span data-stu-id="75fda-114">hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used toomanage IIS settings at startup on Azure.</span></span> <span data-ttu-id="75fda-115">*AppCmd.exe* fornece acesso conveniente de linha de comando tooconfiguration configurações para uso nas tarefas de inicialização no Azure.</span><span class="sxs-lookup"><span data-stu-id="75fda-115">*AppCmd.exe* provides convenient, command-line access tooconfiguration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="75fda-116">Com *AppCmd.exe*, as configurações do site podem ser adicionadas, modificadas ou removidas para aplicativos e sites.</span><span class="sxs-lookup"><span data-stu-id="75fda-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="75fda-117">No entanto, há alguns toowatch de coisas out para usar Olá *AppCmd.exe* como uma tarefa de inicialização:</span><span class="sxs-lookup"><span data-stu-id="75fda-117">However, there are a few things toowatch out for in hello use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="75fda-118">As tarefas de inicialização podem ser executadas mais de uma vez entre as reinicializações.</span><span class="sxs-lookup"><span data-stu-id="75fda-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="75fda-119">Por exemplo, quando uma função é reciclada.</span><span class="sxs-lookup"><span data-stu-id="75fda-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="75fda-120">Se uma ação *AppCmd.exe* for executada mais de uma vez, poderá gerar um erro.</span><span class="sxs-lookup"><span data-stu-id="75fda-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="75fda-121">Por exemplo, a tentativa de uma seção de tooadd muito*Web. config* duas vezes pode gerar um erro.</span><span class="sxs-lookup"><span data-stu-id="75fda-121">For example, attempting tooadd a section too*Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="75fda-122">As tarefas de inicialização falharão caso retornem um código de saída diferente de zero ou **errorlevel**.</span><span class="sxs-lookup"><span data-stu-id="75fda-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="75fda-123">Por exemplo, quando *AppCmd.exe* gera um erro.</span><span class="sxs-lookup"><span data-stu-id="75fda-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="75fda-124">Saudação de toocheck uma boa prática é **errorlevel** depois de chamar *AppCmd.exe*, que é fácil toodo se encapsular chamada hello muito*AppCmd.exe* com um *. cmd*  arquivo.</span><span class="sxs-lookup"><span data-stu-id="75fda-124">It is a good practice toocheck hello **errorlevel** after calling *AppCmd.exe*, which is easy toodo if you wrap hello call too*AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="75fda-125">Se você detectar uma resposta **errorlevel** conhecida, poderá ignorá-la ou passá-la novamente.</span><span class="sxs-lookup"><span data-stu-id="75fda-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="75fda-126">Olá errorlevel retornado por *AppCmd.exe* são listados no arquivo de Winerror hello e também podem ser vistas na [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="75fda-126">hello errorlevel returned by *AppCmd.exe* are listed in hello winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-hello-error-level"></a><span data-ttu-id="75fda-127">Exemplo de gerenciamento de nível de erro Olá</span><span class="sxs-lookup"><span data-stu-id="75fda-127">Example of managing hello error level</span></span>
<span data-ttu-id="75fda-128">Este exemplo adiciona uma seção e uma entrada de compactação para JSON toohello *Web. config* arquivo com tratamento de erros e registro em log.</span><span class="sxs-lookup"><span data-stu-id="75fda-128">This example adds a compression section and a compression entry for JSON toohello *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="75fda-129">Olá seções relevantes do hello [servicedefinition. Csdef] arquivo são mostradas aqui, que incluem a definição de saudação [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) atributo muito`elevated` toogive *AppCmd.exe*  suficientes permissões toochange Olá configurações Olá *Web. config* arquivo:</span><span class="sxs-lookup"><span data-stu-id="75fda-129">hello relevant sections of hello [ServiceDefinition.csdef] file are shown here, which include setting hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute too`elevated` toogive *AppCmd.exe* sufficient permissions toochange hello settings in hello *Web.config* file:</span></span>

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

<span data-ttu-id="75fda-130">Olá *Startup.cmd* em lotes de arquivos usa *AppCmd.exe* tooadd uma seção e uma entrada de compactação para JSON toohello *Web. config* arquivo.</span><span class="sxs-lookup"><span data-stu-id="75fda-130">hello *Startup.cmd* batch file uses *AppCmd.exe* tooadd a compression section and a compression entry for JSON toohello *Web.config* file.</span></span> <span data-ttu-id="75fda-131">Olá esperado **errorlevel** de 183 é definido toozero usando Olá verificar. Programa de linha de comando do EXE.</span><span class="sxs-lookup"><span data-stu-id="75fda-131">hello expected **errorlevel** of 183 is set toozero using hello VERIFY.EXE command-line program.</span></span> <span data-ttu-id="75fda-132">Os errorlevels inesperados são tooStartupErrorLog.txt conectado.</span><span class="sxs-lookup"><span data-stu-id="75fda-132">Unexpected errorlevels are logged tooStartupErrorLog.txt.</span></span>

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

## <a name="add-firewall-rules"></a><span data-ttu-id="75fda-133">Adicionar regras de firewall</span><span class="sxs-lookup"><span data-stu-id="75fda-133">Add firewall rules</span></span>
<span data-ttu-id="75fda-134">No Azure, há efetivamente dois firewalls.</span><span class="sxs-lookup"><span data-stu-id="75fda-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="75fda-135">Olá primeiro firewall controla conexões entre máquina virtual de saudação e Olá fora do mundo.</span><span class="sxs-lookup"><span data-stu-id="75fda-135">hello first firewall controls connections between hello virtual machine and hello outside world.</span></span> <span data-ttu-id="75fda-136">Esse firewall é controlado pelo Olá [pontos de extremidade] elemento Olá [servicedefinition. Csdef] arquivo.</span><span class="sxs-lookup"><span data-stu-id="75fda-136">This firewall is controlled by hello [EndPoints] element in hello [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="75fda-137">Olá segundo firewall controla conexões entre máquinas virtuais de saudação e processos de saudação dentro dessa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="75fda-137">hello second firewall controls connections between hello virtual machine and hello processes within that virtual machine.</span></span> <span data-ttu-id="75fda-138">Esse firewall pode ser controlado por Olá `netsh advfirewall firewall` ferramenta de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="75fda-138">This firewall can be controlled by hello `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="75fda-139">O Azure cria regras de firewall para Olá processos iniciados em suas funções.</span><span class="sxs-lookup"><span data-stu-id="75fda-139">Azure creates firewall rules for hello processes started within your roles.</span></span> <span data-ttu-id="75fda-140">Por exemplo, quando você inicia um programa ou serviço, Azure cria automaticamente Olá tooallow de regras de firewall necessárias toocommunicate esse serviço com hello da Internet.</span><span class="sxs-lookup"><span data-stu-id="75fda-140">For example, when you start a service or program, Azure automatically creates hello necessary firewall rules tooallow that service toocommunicate with hello Internet.</span></span> <span data-ttu-id="75fda-141">No entanto, se você criar um serviço que é iniciado por um processo fora de sua função (como um serviço COM+ ou uma tarefa agendada do Windows), é necessário toomanually criar um serviço de toothat firewall regra tooallow acesso.</span><span class="sxs-lookup"><span data-stu-id="75fda-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need toomanually create a firewall rule tooallow access toothat service.</span></span> <span data-ttu-id="75fda-142">Essas regras de firewall podem ser criadas usando uma tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="75fda-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="75fda-143">Uma tarefa de inicialização que cria uma regra de firewall deve ter um [executionContext][tarefa]  **elevado**.</span><span class="sxs-lookup"><span data-stu-id="75fda-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="75fda-144">Adicionar Olá toohello da tarefa de inicialização a seguir [servicedefinition. Csdef] arquivo.</span><span class="sxs-lookup"><span data-stu-id="75fda-144">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="75fda-145">regra de firewall de saudação tooadd, você deve usar o hello apropriado `netsh advfirewall firewall` comandos no arquivo em lotes de inicialização.</span><span class="sxs-lookup"><span data-stu-id="75fda-145">tooadd hello firewall rule, you must use hello appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="75fda-146">Neste exemplo, a tarefa de inicialização Olá requer segurança e criptografia para a porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="75fda-146">In this example, hello startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="75fda-147">Bloquear um endereço IP específico</span><span class="sxs-lookup"><span data-stu-id="75fda-147">Block a specific IP address</span></span>
<span data-ttu-id="75fda-148">Você pode restringir um conjunto de tooa de acesso de função web do Azure de endereços IP especificados alterando o IIS **Web. config** arquivo.</span><span class="sxs-lookup"><span data-stu-id="75fda-148">You can restrict an Azure web role access tooa set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="75fda-149">Você também precisa toouse um arquivo de comando que desbloqueie Olá **ipSecurity** seção Olá **applicationHost. config** arquivo.</span><span class="sxs-lookup"><span data-stu-id="75fda-149">You also need toouse a command file which unlocks hello **ipSecurity** section of hello **ApplicationHost.config** file.</span></span>

<span data-ttu-id="75fda-150">toodo desbloquear Olá **ipSecurity** seção Olá **applicationHost. config** de arquivo, crie um arquivo de comando que é executado no início da função.</span><span class="sxs-lookup"><span data-stu-id="75fda-150">toodo unlock hello **ipSecurity** section of hello **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="75fda-151">Crie uma pasta no nível de raiz de saudação de sua função web chamada **inicialização** e, dentro dessa pasta, crie um arquivo em lotes chamado **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="75fda-151">Create a folder at hello root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="75fda-152">Adicionar este projeto do Visual Studio tooyour arquivo e definir propriedades de saudação muito**copiar sempre** tooensure que ele está incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="75fda-152">Add this file tooyour Visual Studio project and set hello properties too**Copy Always** tooensure that it is included in your package.</span></span>

<span data-ttu-id="75fda-153">Adicionar Olá toohello da tarefa de inicialização a seguir [servicedefinition. Csdef] arquivo.</span><span class="sxs-lookup"><span data-stu-id="75fda-153">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="75fda-154">Adicionar este comando toohello **startup.cmd** arquivo:</span><span class="sxs-lookup"><span data-stu-id="75fda-154">Add this command toohello **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="75fda-155">Esta tarefa faz com que Olá **startup.cmd** toobe arquivo seja executado sempre que a função da web de saudação é inicializada, garantindo que Olá necessárias do lote **ipSecurity** seção está desbloqueada.</span><span class="sxs-lookup"><span data-stu-id="75fda-155">This task causes hello **startup.cmd** batch file toobe run every time hello web role is initialized, ensuring that hello required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="75fda-156">Finalmente, modifique Olá [seção System. webServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) da sua função web **Web. config** arquivo tooadd uma lista de endereços IP que têm acesso, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="75fda-156">Finally, modify hello [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file tooadd a list of IP addresses that are granted access, as shown in hello following example:</span></span>

<span data-ttu-id="75fda-157">Essa configuração de exemplo **permite** tooaccess de todos os IPs Olá servidor exceto Olá dois definido</span><span class="sxs-lookup"><span data-stu-id="75fda-157">This sample config **allows** all IPs tooaccess hello server except hello two defined</span></span>

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

<span data-ttu-id="75fda-158">Essa configuração de exemplo **nega** todos os IPs acessem servidor hello, exceto Olá dois definido.</span><span class="sxs-lookup"><span data-stu-id="75fda-158">This sample config **denies** all IPs from accessing hello server except for hello two defined.</span></span>

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

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="75fda-159">Criar uma tarefa de inicialização do PowerShell</span><span class="sxs-lookup"><span data-stu-id="75fda-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="75fda-160">Scripts do Windows PowerShell não podem ser chamados diretamente no hello [servicedefinition. Csdef] arquivo, mas pode ser chamado de dentro de um arquivo em lotes de inicialização.</span><span class="sxs-lookup"><span data-stu-id="75fda-160">Windows PowerShell scripts cannot be called directly from hello [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="75fda-161">O PowerShell (por padrão) não executa scripts não assinados.</span><span class="sxs-lookup"><span data-stu-id="75fda-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="75fda-162">A menos que você assinar o script, você precisa tooconfigure PowerShell toorun de scripts não assinados.</span><span class="sxs-lookup"><span data-stu-id="75fda-162">Unless you sign your script, you need tooconfigure PowerShell toorun unsigned scripts.</span></span> <span data-ttu-id="75fda-163">toorun scripts não assinados, hello **ExecutionPolicy** deve ser definido muito**irrestrito**.</span><span class="sxs-lookup"><span data-stu-id="75fda-163">toorun unsigned scripts, hello **ExecutionPolicy** must be set too**Unrestricted**.</span></span> <span data-ttu-id="75fda-164">Olá **ExecutionPolicy** configuração que você usa é baseada na versão de saudação do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="75fda-164">hello **ExecutionPolicy** setting that you use is based on hello version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="75fda-165">Se você estiver usando um sistema operacional convidado que for executar o PowerShell 2.0 ou 1.0, você pode forçar a toorun versão 2 e se não estiver disponível, use a versão 1.</span><span class="sxs-lookup"><span data-stu-id="75fda-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 toorun, and if unavailable, use version 1.</span></span>

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

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="75fda-166">Criar arquivos no armazenamento local de uma tarefa de inicialização</span><span class="sxs-lookup"><span data-stu-id="75fda-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="75fda-167">Você pode usar um toostore de recursos de armazenamento local arquivos criados por sua tarefa de inicialização que é acessada posteriormente por seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="75fda-167">You can use a local storage resource toostore files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="75fda-168">toocreate Olá o recurso de armazenamento local, adicione uma [LocalResources] seção toohello [servicedefinition. Csdef] de arquivo e, em seguida, adicione Olá [LocalStorage] elemento filho.</span><span class="sxs-lookup"><span data-stu-id="75fda-168">toocreate hello local storage resource, add a [LocalResources] section toohello [ServiceDefinition.csdef] file and then add hello [LocalStorage] child element.</span></span> <span data-ttu-id="75fda-169">Fornecer recursos de armazenamento local de saudação um nome exclusivo e um tamanho apropriado para sua tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="75fda-169">Give hello local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="75fda-170">toouse um recurso de armazenamento local em sua tarefa de inicialização, é necessário toocreate um local de recursos do ambiente variável tooreference Olá armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="75fda-170">toouse a local storage resource in your startup task, you need toocreate an environment variable tooreference hello local storage resource location.</span></span> <span data-ttu-id="75fda-171">Olá, em seguida, a tarefa de inicialização e aplicativo hello são tooread capaz de gravar o recurso de armazenamento local de toohello de arquivos.</span><span class="sxs-lookup"><span data-stu-id="75fda-171">Then hello startup task and hello application are able tooread and write files toohello local storage resource.</span></span>

<span data-ttu-id="75fda-172">Olá seções relevantes do hello **servicedefinition. Csdef** arquivo são mostradas aqui:</span><span class="sxs-lookup"><span data-stu-id="75fda-172">hello relevant sections of hello **ServiceDefinition.csdef** file are shown here:</span></span>

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

<span data-ttu-id="75fda-173">Por exemplo, isso **Startup.cmd** arquivo em lotes usa Olá **PathToStartupStorage** arquivo hello do ambiente variável toocreate **MyTest.txt** no armazenamento local de saudação local.</span><span class="sxs-lookup"><span data-stu-id="75fda-173">As an example, this **Startup.cmd** batch file uses hello **PathToStartupStorage** environment variable toocreate hello file **MyTest.txt** on hello local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="75fda-174">Você pode acessar a pasta de armazenamento local de saudação do SDK do Azure usando Olá [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="75fda-174">You can access local storage folder from hello Azure SDK by using hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a><span data-ttu-id="75fda-175">Executar no emulador de saudação ou nuvem</span><span class="sxs-lookup"><span data-stu-id="75fda-175">Run in hello emulator or cloud</span></span>
<span data-ttu-id="75fda-176">Você pode ter sua tarefa de inicialização executar etapas diferentes ao operar em Olá nuvem quando comparada toowhen é no emulador de computação hello.</span><span class="sxs-lookup"><span data-stu-id="75fda-176">You can have your startup task perform different steps when it is operating in hello cloud compared toowhen it is in hello compute emulator.</span></span> <span data-ttu-id="75fda-177">Por exemplo, convém toouse uma cópia atualizada dos dados do SQL somente quando em execução no emulador de saudação.</span><span class="sxs-lookup"><span data-stu-id="75fda-177">For example, you may want toouse a fresh copy of your SQL data only when running in hello emulator.</span></span> <span data-ttu-id="75fda-178">Ou talvez você queira toodo algumas otimizações de desempenho para a nuvem de saudação que você não precisa toodo quando em execução no emulador de saudação.</span><span class="sxs-lookup"><span data-stu-id="75fda-178">Or you may want toodo some performance optimizations for hello cloud that you don't need toodo when running in hello emulator.</span></span>

<span data-ttu-id="75fda-179">Este tooperform capacidade diferente ações em Olá emulador de computação e Olá nuvem pode ser realizada por meio da criação de uma variável de ambiente no hello [servicedefinition. Csdef] arquivo.</span><span class="sxs-lookup"><span data-stu-id="75fda-179">This ability tooperform different actions on hello compute emulator and hello cloud can be accomplished by creating an environment variable in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="75fda-180">Você testa então essa variável de ambiente para um valor em sua tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="75fda-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="75fda-181">variável de ambiente toocreate Olá adicionar Olá [variável]/[RoleInstanceValue] elemento e crie um valor de XPath do `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="75fda-181">toocreate hello environment variable, add hello [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="75fda-182">Olá valor Olá **ComputeEmulatorRunning %** variável de ambiente é `true` quando em execução no emulador de computação Olá, e `false` quando em execução na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="75fda-182">hello value of hello **%ComputeEmulatorRunning%** environment variable is `true` when running on hello compute emulator, and `false` when running on hello cloud.</span></span>

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

<span data-ttu-id="75fda-183">tarefa Olá agora pode verificar Olá **ComputeEmulatorRunning %** ações diferentes de tooperform variável de ambiente com base em se a função hello está sendo executado no hello nuvem ou Olá emulador.</span><span class="sxs-lookup"><span data-stu-id="75fda-183">hello task can now check hello **%ComputeEmulatorRunning%** environment variable tooperform different actions based on whether hello role is running in hello cloud or hello emulator.</span></span> <span data-ttu-id="75fda-184">A seguir, um script de shell .cmd que verifica essa variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="75fda-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="75fda-185">Detectar se a tarefa já foi executada</span><span class="sxs-lookup"><span data-stu-id="75fda-185">Detect that your task has already run</span></span>
<span data-ttu-id="75fda-186">função Hello pode reciclar sem uma reinicialização, causando o toorun de tarefas de inicialização novamente.</span><span class="sxs-lookup"><span data-stu-id="75fda-186">hello role may recycle without a reboot causing your startup tasks toorun again.</span></span> <span data-ttu-id="75fda-187">Não há nenhum tooindicate de sinalizador que uma tarefa já executada em Olá hospeda a VM.</span><span class="sxs-lookup"><span data-stu-id="75fda-187">There is no flag tooindicate that a task has already run on hello hosting VM.</span></span> <span data-ttu-id="75fda-188">Talvez você tenha algumas tarefas onde não importará se elas forem executadas várias vezes.</span><span class="sxs-lookup"><span data-stu-id="75fda-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="75fda-189">No entanto, você pode executar em uma situação em que você precisa tooprevent uma tarefa de execução mais de uma vez.</span><span class="sxs-lookup"><span data-stu-id="75fda-189">However, you may run into a situation where you need tooprevent a task from running more than once.</span></span>

<span data-ttu-id="75fda-190">toodetect forma mais simples Olá que uma tarefa já foi executado é toocreate um arquivo em Olá **% TEMP %** pasta quando a tarefa de saudação é bem-sucedida e examinar para ele Olá iniciam tarefa hello.</span><span class="sxs-lookup"><span data-stu-id="75fda-190">hello simplest way toodetect that a task has already run is toocreate a file in hello **%TEMP%** folder when hello task is successful and look for it at hello start of hello task.</span></span> <span data-ttu-id="75fda-191">A seguir, um script de shell cmd de exemplo que faz isso para você.</span><span class="sxs-lookup"><span data-stu-id="75fda-191">Here is a sample cmd shell script that does that for you.</span></span>

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

## <a name="task-best-practices"></a><span data-ttu-id="75fda-192">Práticas recomendadas para tarefas</span><span class="sxs-lookup"><span data-stu-id="75fda-192">Task best practices</span></span>
<span data-ttu-id="75fda-193">A seguir, algumas práticas recomendadas que você deve seguir ao configurar a tarefa para sua função Web ou de trabalho.</span><span class="sxs-lookup"><span data-stu-id="75fda-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="75fda-194">Sempre registrar em log as atividades de inicialização</span><span class="sxs-lookup"><span data-stu-id="75fda-194">Always log startup activities</span></span>
<span data-ttu-id="75fda-195">Visual Studio não fornece toostep um depurador por meio de arquivos em lotes, portanto é bom tooget todos os dados na operação de saudação dos arquivos em lotes possível.</span><span class="sxs-lookup"><span data-stu-id="75fda-195">Visual Studio does not provide a debugger toostep through batch files, so it's good tooget as much data on hello operation of batch files as possible.</span></span> <span data-ttu-id="75fda-196">Log de saída de hello dos arquivos em lotes, ambos **stdout** e **stderr**, pode fornecer informações importantes durante a tentativa de toodebug e corrigir arquivos em lotes.</span><span class="sxs-lookup"><span data-stu-id="75fda-196">Logging hello output of batch files, both **stdout** and **stderr**, can give you important information when trying toodebug and fix batch files.</span></span> <span data-ttu-id="75fda-197">toolog ambas as **stdout** e **stderr** toohello um arquivo StartupLog.txt no Olá Olá de tooby apontada diretório **% TEMP %** variável de ambiente, adicione o texto de saudação `>>  "%TEMP%\\StartupLog.txt" 2>&1`toohello final de específicos linhas que você deseja toolog.</span><span class="sxs-lookup"><span data-stu-id="75fda-197">toolog both **stdout** and **stderr** toohello StartupLog.txt file in hello directory pointed tooby hello **%TEMP%** environment variable, add hello text `>>  "%TEMP%\\StartupLog.txt" 2>&1` toohello end of specific lines you want toolog.</span></span> <span data-ttu-id="75fda-198">Por exemplo, tooexecute setup.exe em Olá **% PathToApp1Install %** diretório:</span><span class="sxs-lookup"><span data-stu-id="75fda-198">For example, tooexecute setup.exe in hello **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="75fda-199">toosimplify o xml, você pode criar um wrapper *cmd* arquivo que chama todos sua inicialização tarefas juntamente com o registro em log e garante Olá de compartilhamentos cada tarefa filho mesmas variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="75fda-199">toosimplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares hello same environment variables.</span></span>

<span data-ttu-id="75fda-200">Você pode descobrir que embora irritantes toouse `>> "%TEMP%\StartupLog.txt" 2>&1` no final de saudação de cada tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="75fda-200">You may find it annoying though toouse `>> "%TEMP%\StartupLog.txt" 2>&1` on hello end of each startup task.</span></span> <span data-ttu-id="75fda-201">Você pode impor o log de tarefas criando um invólucro que manipula o registro em log para você.</span><span class="sxs-lookup"><span data-stu-id="75fda-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="75fda-202">Esse wrapper chama o arquivo de lote real Olá desejado toorun.</span><span class="sxs-lookup"><span data-stu-id="75fda-202">This wrapper calls hello real batch file you want toorun.</span></span> <span data-ttu-id="75fda-203">Nenhuma saída do arquivo de lote de destino Olá será redirecionado toohello *Startuplog.txt* arquivo.</span><span class="sxs-lookup"><span data-stu-id="75fda-203">Any output from hello target batch file will be redirected toohello *Startuplog.txt* file.</span></span>

<span data-ttu-id="75fda-204">saudação de exemplo a seguir mostra como tooredirect todas as saídas de um arquivo em lotes de inicialização.</span><span class="sxs-lookup"><span data-stu-id="75fda-204">hello following example shows how tooredirect all output from a startup batch file.</span></span> <span data-ttu-id="75fda-205">Neste exemplo, o arquivo de Serverdefinition Olá cria uma tarefa de inicialização que chama *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="75fda-205">In this example, hello ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="75fda-206">*logwrap.cmd* chamadas *Startup2.cmd*, redirecionando a saída de todos os demais**% TEMP %\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="75fda-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output too**%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="75fda-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="75fda-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="75fda-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="75fda-208">**logwrap.cmd:**</span></span>

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

<span data-ttu-id="75fda-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="75fda-209">**Startup2.cmd:**</span></span>

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

<span data-ttu-id="75fda-210">Exemplo de saída em Olá **StartupLog.txt** arquivo:</span><span class="sxs-lookup"><span data-stu-id="75fda-210">Sample output in hello **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="75fda-211">Olá **StartupLog.txt** arquivo está localizado em Olá *C:\Resources\temp\\\RoleTemp {identificador de função}* pasta.</span><span class="sxs-lookup"><span data-stu-id="75fda-211">hello **StartupLog.txt** file is located in hello *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="75fda-212">Definir executionContext adequadamente para tarefas de inicialização</span><span class="sxs-lookup"><span data-stu-id="75fda-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="75fda-213">Definir privilégios corretamente para a tarefa de inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="75fda-213">Set privileges appropriately for hello startup task.</span></span> <span data-ttu-id="75fda-214">Às vezes, as tarefas de inicialização devem executar com privilégios elevados, mesmo que a função hello é executado com privilégios normais.</span><span class="sxs-lookup"><span data-stu-id="75fda-214">Sometimes startup tasks must run with elevated privileges even though hello role runs with normal privileges.</span></span>

<span data-ttu-id="75fda-215">Olá [executionContext][tarefa] atributo define o nível de privilégio de saudação da tarefa de inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="75fda-215">hello [executionContext][Task] attribute sets hello privilege level of hello startup task.</span></span> <span data-ttu-id="75fda-216">Usando `executionContext="limited"` significa tem de tarefa de inicialização Olá Olá mesmo nível de privilégio como função hello.</span><span class="sxs-lookup"><span data-stu-id="75fda-216">Using `executionContext="limited"` means hello startup task has hello same privilege level as hello role.</span></span> <span data-ttu-id="75fda-217">Usando `executionContext="elevated"` significa a tarefa de inicialização Olá tem privilégios de administrador, que permite inicialização Olá tarefa tooperform tarefas de administrador sem conceder função tooyour de privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="75fda-217">Using `executionContext="elevated"` means hello startup task has administrator privileges, which allows hello startup task tooperform administrator tasks without giving administrator privileges tooyour role.</span></span>

<span data-ttu-id="75fda-218">Um exemplo de uma tarefa de inicialização que exige privilégios elevados é uma tarefa de inicialização que usa **AppCmd.exe** tooconfigure IIS.</span><span class="sxs-lookup"><span data-stu-id="75fda-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** tooconfigure IIS.</span></span> <span data-ttu-id="75fda-219">**AppCmd.exe** requer `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="75fda-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-hello-appropriate-tasktype"></a><span data-ttu-id="75fda-220">Use o taskType apropriado Olá</span><span class="sxs-lookup"><span data-stu-id="75fda-220">Use hello appropriate taskType</span></span>
<span data-ttu-id="75fda-221">Olá [taskType][tarefa] atributo determina a tarefa de inicialização de Olá Olá maneira é executada.</span><span class="sxs-lookup"><span data-stu-id="75fda-221">hello [taskType][Task] attribute determines hello way hello startup task is executed.</span></span> <span data-ttu-id="75fda-222">Há três valores: **simples**, **segundo plano** e **primeiro plano**.</span><span class="sxs-lookup"><span data-stu-id="75fda-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="75fda-223">Olá tarefas primeiro e segundo plano são iniciadas assincronamente, e, em seguida, tarefas simples Olá são executadas de forma síncrona um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="75fda-223">hello background and foreground tasks are started asynchronously, and then hello simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="75fda-224">Com **simples** tarefas de inicialização, em que você pode definir a ordem hello, no qual executar tarefas de saudação pela ordem Olá no qual Olá tarefas estão listadas no arquivo servicedefinition. Csdef de saudação.</span><span class="sxs-lookup"><span data-stu-id="75fda-224">With **simple** startup tasks, you can set hello order in which hello tasks run by hello order in which hello tasks are listed in hello ServiceDefinition.csdef file.</span></span> <span data-ttu-id="75fda-225">Se um **simples** tarefa termina com diferente de zero código de saída, em seguida, Olá paradas do procedimento de inicialização e função hello não iniciar.</span><span class="sxs-lookup"><span data-stu-id="75fda-225">If a **simple** task ends with a non-zero exit code, then hello startup procedure stops and hello role does not start.</span></span>

<span data-ttu-id="75fda-226">Olá diferença entre **em segundo plano** tarefas de inicialização e **primeiro plano** é que as tarefas de inicialização **primeiro plano** tarefas manter a execução da função de Olá até Olá  **primeiro plano** terminar.</span><span class="sxs-lookup"><span data-stu-id="75fda-226">hello difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep hello role running until hello **foreground** task ends.</span></span> <span data-ttu-id="75fda-227">Isso também significa que se hello **primeiro plano** tarefa congelar ou falhas, a função hello não será reciclada até Olá **primeiro plano** tarefa é forçada fechado.</span><span class="sxs-lookup"><span data-stu-id="75fda-227">This also means that if hello **foreground** task hangs or crashes, hello role will not recycle until hello **foreground** task is forced closed.</span></span> <span data-ttu-id="75fda-228">Por esse motivo, **em segundo plano** tarefas são recomendadas para tarefas de inicialização assíncronas, a menos que você precise do recurso de saudação **primeiro plano** tarefa.</span><span class="sxs-lookup"><span data-stu-id="75fda-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of hello **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="75fda-229">Encerrar arquivos em lotes com EXIT /B 0</span><span class="sxs-lookup"><span data-stu-id="75fda-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="75fda-230">Olá função começará somente se hello **errorlevel** de cada um dos seu inicialização simple tarefa é zero.</span><span class="sxs-lookup"><span data-stu-id="75fda-230">hello role will only start if hello **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="75fda-231">Nem todos os programas definem Olá **errorlevel** (código de saída) corretamente, portanto o arquivo de lote Olá deve terminar com um `EXIT /B 0` se tudo foi executado corretamente.</span><span class="sxs-lookup"><span data-stu-id="75fda-231">Not all programs set hello **errorlevel** (exit code) correctly, so hello batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="75fda-232">A ausência de um `EXIT /B 0` em Olá final de um arquivo em lotes de inicialização é uma causa comum de funções que não são iniciados.</span><span class="sxs-lookup"><span data-stu-id="75fda-232">A missing `EXIT /B 0` at hello end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="75fda-233">Eu já ter notado que lote aninhado arquivos de suspensão, às vezes, ao usar o hello `/B` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="75fda-233">I've noticed that nested batch files sometimes hang when using hello `/B` parameter.</span></span> <span data-ttu-id="75fda-234">Talvez você queira toomake-se de que esse problema de suspensão não ocorre se o outro arquivo em lotes chama o arquivo em lotes atual, como se você usar o hello [wrapper de log](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="75fda-234">You may want toomake sure that this hang problem does not happen if another batch file calls your current batch file, like if you use hello [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="75fda-235">Você pode omitir Olá `/B` parâmetro nesse caso.</span><span class="sxs-lookup"><span data-stu-id="75fda-235">You can omit hello `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a><span data-ttu-id="75fda-236">Esperar toorun de tarefas de inicialização mais de uma vez</span><span class="sxs-lookup"><span data-stu-id="75fda-236">Expect startup tasks toorun more than once</span></span>
<span data-ttu-id="75fda-237">Nem todas as reciclagens de função incluem uma reinicialização, mas todas as reciclagens incluem a execução de todas as tarefas de inicialização.</span><span class="sxs-lookup"><span data-stu-id="75fda-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="75fda-238">Isso significa que as tarefas de inicialização devem ser capaz de toorun várias vezes entre reinicializações sem problemas.</span><span class="sxs-lookup"><span data-stu-id="75fda-238">This means that startup tasks must be able toorun multiple times between reboots without any problems.</span></span> <span data-ttu-id="75fda-239">Isso é discutido em Olá [anterior seção](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="75fda-239">This is discussed in hello [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a><span data-ttu-id="75fda-240">Usar arquivos de toostore de armazenamento local que devem ser acessados na função hello</span><span class="sxs-lookup"><span data-stu-id="75fda-240">Use local storage toostore files that must be accessed in hello role</span></span>
<span data-ttu-id="75fda-241">Se você deseja toocopy ou cria um arquivo durante sua tarefa de inicialização que é acessível tooyour função, esse arquivo deve ser colocado no armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="75fda-241">If you want toocopy or create a file during your startup task that is then accessible tooyour role, then that file must be placed in local storage.</span></span> <span data-ttu-id="75fda-242">Consulte Olá [anterior seção](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="75fda-242">See hello [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="75fda-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="75fda-243">Next steps</span></span>
<span data-ttu-id="75fda-244">Examine a nuvem Olá [modelo e o pacote de serviço](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="75fda-244">Review hello cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="75fda-245">Saiba mais sobre o funcionamento de [Tarefas](cloud-services-startup-tasks.md) .</span><span class="sxs-lookup"><span data-stu-id="75fda-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="75fda-246">[Crie e implante](cloud-services-how-to-create-deploy-portal.md) seu pacote de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="75fda-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

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
