---
title: "Tarefas de inicialização comuns para Serviços de Nuvem | Microsoft Docs"
description: "Oferece alguns exemplos de tarefas de inicialização comuns que talvez você queira executar na função Web ou função de trabalho de seus serviços de nuvem."
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
ms.openlocfilehash: cee23da5b089b02bfc0ef10afd60f0f2272585b1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="c0eb6-103">Tarefas de inicialização comuns do Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="c0eb6-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="c0eb6-104">Este artigo oferece alguns exemplos de tarefas de inicialização comuns que talvez você queira executar no serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-104">This article provides some examples of common startup tasks you may want to perform in your cloud service.</span></span> <span data-ttu-id="c0eb6-105">Você pode usar as tarefas de inicialização para executar operações antes do início de uma função.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="c0eb6-106">As operações que talvez você queira executar incluem a instalação de um componente, o registro de componentes COM, a configuração de chaves do registro ou o início de um processo de longa duração.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="c0eb6-107">Confira [este artigo](cloud-services-startup-tasks.md) para entender o funcionamento das tarefas de inicialização e, especificamente, como criar as entradas que definem uma tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-107">See [this article](cloud-services-startup-tasks.md) to understand how startup tasks work, and specifically how to create the entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="c0eb6-108">As tarefas de inicialização não são aplicáveis às Máquinas Virtuais, apenas às funções Web e de Trabalho do Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-108">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="c0eb6-109">Definir variáveis de ambiente antes de iniciar uma função</span><span class="sxs-lookup"><span data-stu-id="c0eb6-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="c0eb6-110">Se você precisar de variáveis de ambiente definidas para uma tarefa específica, use o elemento [Environment] dentro do elemento [Task].</span><span class="sxs-lookup"><span data-stu-id="c0eb6-110">If you need environment variables defined for a specific task, use the [Environment] element inside the [Task] element.</span></span>

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

<span data-ttu-id="c0eb6-111">As variáveis também podem usar um [valor válido do Azure XPath](cloud-services-role-config-xpath.md) para fazer referência a algo sobre a implantação.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) to reference something about the deployment.</span></span> <span data-ttu-id="c0eb6-112">Em vez de usar o atributo `value` , defina um elemento filho [RoleInstanceValue] .</span><span class="sxs-lookup"><span data-stu-id="c0eb6-112">Instead of using the `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="c0eb6-113">Configurar a inicialização do IIS com AppCmd.exe</span><span class="sxs-lookup"><span data-stu-id="c0eb6-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="c0eb6-114">A ferramenta de linha de comando [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) pode ser usada para gerenciar as configurações do IIS na inicialização no Azure.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-114">The [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used to manage IIS settings at startup on Azure.</span></span> <span data-ttu-id="c0eb6-115">*AppCmd.exe* oferece acesso de linha de comando conveniente às definições de configuração para uso nas tarefas de inicialização no Azure.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-115">*AppCmd.exe* provides convenient, command-line access to configuration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="c0eb6-116">Com *AppCmd.exe*, as configurações do site podem ser adicionadas, modificadas ou removidas para aplicativos e sites.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="c0eb6-117">No entanto, há algumas coisas que merecem atenção no uso de *AppCmd.exe* como uma tarefa de inicialização:</span><span class="sxs-lookup"><span data-stu-id="c0eb6-117">However, there are a few things to watch out for in the use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="c0eb6-118">As tarefas de inicialização podem ser executadas mais de uma vez entre as reinicializações.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="c0eb6-119">Por exemplo, quando uma função é reciclada.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="c0eb6-120">Se uma ação *AppCmd.exe* for executada mais de uma vez, poderá gerar um erro.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="c0eb6-121">Por exemplo, a tentativa de adicionar uma seção a *Web.config* duas vezes pode gerar um erro.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-121">For example, attempting to add a section to *Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="c0eb6-122">As tarefas de inicialização falharão caso retornem um código de saída diferente de zero ou **errorlevel**.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="c0eb6-123">Por exemplo, quando *AppCmd.exe* gera um erro.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="c0eb6-124">É uma prática recomendada verificar **errorlevel** depois de chamar *AppCmd.exe*, o que é fácil se você encapsula a chamada a *AppCmd.exe* com um arquivo *.cmd*.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-124">It is a good practice to check the **errorlevel** after calling *AppCmd.exe*, which is easy to do if you wrap the call to *AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="c0eb6-125">Se você detectar uma resposta **errorlevel** conhecida, poderá ignorá-la ou passá-la novamente.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="c0eb6-126">O errorlevel retornado por *AppCmd.exe* é listado no arquivo winerror.h e também pode ser visto no [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0eb6-126">The errorlevel returned by *AppCmd.exe* are listed in the winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-the-error-level"></a><span data-ttu-id="c0eb6-127">Exemplo de gerenciamento de nível de erro</span><span class="sxs-lookup"><span data-stu-id="c0eb6-127">Example of managing the error level</span></span>
<span data-ttu-id="c0eb6-128">Este exemplo adiciona uma seção e uma entrada de compactação para JSON para o arquivo *Web.config* , com tratamento de erros e registro em log.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-128">This example adds a compression section and a compression entry for JSON to the *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="c0eb6-129">As seções relevantes do arquivo [Servicedefinition] são mostradas aqui, o que inclui a definição do atributo [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) como `elevated` para dar a *AppCmd.exe* permissões suficientes para alterar as configurações no arquivo *Web.config*:</span><span class="sxs-lookup"><span data-stu-id="c0eb6-129">The relevant sections of the [ServiceDefinition.csdef] file are shown here, which include setting the [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute to `elevated` to give *AppCmd.exe* sufficient permissions to change the settings in the *Web.config* file:</span></span>

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

<span data-ttu-id="c0eb6-130">O arquivo em lotes *Startup.cmd* usa *AppCmd.exe* para adicionar uma seção e uma entrada de compactação para JSON ao arquivo *Web.config*.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-130">The *Startup.cmd* batch file uses *AppCmd.exe* to add a compression section and a compression entry for JSON to the *Web.config* file.</span></span> <span data-ttu-id="c0eb6-131">O **errorlevel** esperado de 183 é definido como zero usando o programa de linha de comando VERIFY.EXE.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-131">The expected **errorlevel** of 183 is set to zero using the VERIFY.EXE command-line program.</span></span> <span data-ttu-id="c0eb6-132">Os errorlevels inesperados são registrados em StartupErrorLog.txt.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-132">Unexpected errorlevels are logged to StartupErrorLog.txt.</span></span>

```cmd
REM   *** Add a compression section to the Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying to add a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. To handle this situation, set the ERRORLEVEL to zero by using the Verify command. The Verify
REM   command will safely set the ERRORLEVEL to zero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If the ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding the JSON compression type to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report the date, time, and ERRORLEVEL of the error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a><span data-ttu-id="c0eb6-133">Adicionar regras de firewall</span><span class="sxs-lookup"><span data-stu-id="c0eb6-133">Add firewall rules</span></span>
<span data-ttu-id="c0eb6-134">No Azure, há efetivamente dois firewalls.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="c0eb6-135">O primeiro firewall controla conexões entre a máquina virtual e o mundo externo.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-135">The first firewall controls connections between the virtual machine and the outside world.</span></span> <span data-ttu-id="c0eb6-136">Esse firewall é controlado pelo elemento [EndPoints] no arquivo [Servicedefinition].</span><span class="sxs-lookup"><span data-stu-id="c0eb6-136">This firewall is controlled by the [EndPoints] element in the [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="c0eb6-137">O segundo firewall controla conexões entre a máquina virtual e os processos dessa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-137">The second firewall controls connections between the virtual machine and the processes within that virtual machine.</span></span> <span data-ttu-id="c0eb6-138">Esse firewall pode ser controlada pela ferramenta de linha de comando `netsh advfirewall firewall`.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-138">This firewall can be controlled by the `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="c0eb6-139">O Azure cria regras de firewall para processos iniciados em suas funções.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-139">Azure creates firewall rules for the processes started within your roles.</span></span> <span data-ttu-id="c0eb6-140">Por exemplo, quando você inicia um serviço ou um programa, o Azure cria automaticamente as regras de firewall necessárias para permitir que o serviço ser comunique com a Internet.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-140">For example, when you start a service or program, Azure automatically creates the necessary firewall rules to allow that service to communicate with the Internet.</span></span> <span data-ttu-id="c0eb6-141">No entanto, se você criar um serviço que é iniciado por um processo fora de sua função (como um serviço COM+ ou uma tarefa agendada do Windows), precisará criar manualmente uma regra de firewall para permitir o acesso a esse serviço.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need to manually create a firewall rule to allow access to that service.</span></span> <span data-ttu-id="c0eb6-142">Essas regras de firewall podem ser criadas usando uma tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="c0eb6-143">Uma tarefa de inicialização que cria uma regra de firewall deve ter um [executionContext][Task]  **elevado**.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="c0eb6-144">Adicione a seguinte tarefa de inicialização ao arquivo [Servicedefinition] .</span><span class="sxs-lookup"><span data-stu-id="c0eb6-144">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="c0eb6-145">Para adicionar a regra de firewall, você deverá usar os comandos `netsh advfirewall firewall` adequados no arquivo em lotes de inicialização.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-145">To add the firewall rule, you must use the appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="c0eb6-146">Neste exemplo, a tarefa de inicialização exige segurança e criptografia para a porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-146">In this example, the startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="c0eb6-147">Bloquear um endereço IP específico</span><span class="sxs-lookup"><span data-stu-id="c0eb6-147">Block a specific IP address</span></span>
<span data-ttu-id="c0eb6-148">Você pode restringir um acesso de função Web do Azure para um conjunto de endereços IP especificados, modificando o IIS arquivo **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-148">You can restrict an Azure web role access to a set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="c0eb6-149">Você também precisa usar um arquivo de comando que desbloqueie a seção **ipSecurity** do arquivo **applicationHost.config**.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-149">You also need to use a command file which unlocks the **ipSecurity** section of the **ApplicationHost.config** file.</span></span>

<span data-ttu-id="c0eb6-150">Para desbloquear a seção **ipSecurity** do arquivo **applicationHost. config**, crie um arquivo de comando que é executado no início da função.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-150">To do unlock the **ipSecurity** section of the **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="c0eb6-151">Crie uma pasta no nível raiz da sua função Web chamada **startup** e, nessa pasta, crie um arquivo em lotes chamado **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-151">Create a folder at the root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="c0eb6-152">Adicione esse arquivo ao projeto do Visual Studio e defina as propriedades como **Copiar Sempre** para garantir que ele seja incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-152">Add this file to your Visual Studio project and set the properties to **Copy Always** to ensure that it is included in your package.</span></span>

<span data-ttu-id="c0eb6-153">Adicione a seguinte tarefa de inicialização ao arquivo [Servicedefinition] .</span><span class="sxs-lookup"><span data-stu-id="c0eb6-153">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="c0eb6-154">Adicione este comando ao arquivo **startup.cmd** :</span><span class="sxs-lookup"><span data-stu-id="c0eb6-154">Add this command to the **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="c0eb6-155">Essa tarefa faz com que o arquivo em lotes **startup.cmd** seja executado sempre que a função Web for inicializada, garantindo que a seção **ipSecurity** necessária seja desbloqueada.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-155">This task causes the **startup.cmd** batch file to be run every time the web role is initialized, ensuring that the required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="c0eb6-156">Por fim, modifique a [seção system.webServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) do arquivo **web.config** da sua função Web para adicionar uma lista de endereços IP com acesso concedido, como mostrado neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="c0eb6-156">Finally, modify the [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file to add a list of IP addresses that are granted access, as shown in the following example:</span></span>

<span data-ttu-id="c0eb6-157">Esta configuração de exemplo **permite** que todos os IPs acessem o servidor, exceto os dois definidos</span><span class="sxs-lookup"><span data-stu-id="c0eb6-157">This sample config **allows** all IPs to access the server except the two defined</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--The following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

<span data-ttu-id="c0eb6-158">Esta configuração de exemplo **nega** que todos os IPs acessem o servidor, exceto os dois definidos.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-158">This sample config **denies** all IPs from accessing the server except for the two defined.</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--The following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="c0eb6-159">Criar uma tarefa de inicialização do PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0eb6-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="c0eb6-160">Os scripts do Windows PowerShell não podem ser chamados diretamente do arquivo [Servicedefinition] , mas podem ser chamados de um arquivo em lotes de inicialização.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-160">Windows PowerShell scripts cannot be called directly from the [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="c0eb6-161">O PowerShell (por padrão) não executa scripts não assinados.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="c0eb6-162">A menos que você assine seu script, precisará configurar o PowerShell para executar scripts não assinados.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-162">Unless you sign your script, you need to configure PowerShell to run unsigned scripts.</span></span> <span data-ttu-id="c0eb6-163">Para executar scripts não assinados, **ExecutionPolicy** deve ser definido como **Irrestrito**.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-163">To run unsigned scripts, the **ExecutionPolicy** must be set to **Unrestricted**.</span></span> <span data-ttu-id="c0eb6-164">A configuração **ExecutionPolicy** que você usa baseia-se na versão do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-164">The **ExecutionPolicy** setting that you use is based on the version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log the output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="c0eb6-165">Se você estiver usando um SO Convidado que esteja executando o PowerShell 2.0 ou 1.0, poderá impor a execução da versão 2. Se ela não estiver disponível, use a versão 1.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 to run, and if unavailable, use version 1.</span></span>

```cmd
REM   Attempt to set the execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set the execution policy by using the PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="c0eb6-166">Criar arquivos no armazenamento local de uma tarefa de inicialização</span><span class="sxs-lookup"><span data-stu-id="c0eb6-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="c0eb6-167">Você pode usar um recurso de armazenamento local para armazenar os arquivos criados pela tarefa de inicialização que será acessada posteriormente por seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-167">You can use a local storage resource to store files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="c0eb6-168">Para criar o recurso de armazenamento local, adicione uma seção [LocalResources] ao arquivo [Servicedefinition] e adicione o elemento filho [LocalStorage].</span><span class="sxs-lookup"><span data-stu-id="c0eb6-168">To create the local storage resource, add a [LocalResources] section to the [ServiceDefinition.csdef] file and then add the [LocalStorage] child element.</span></span> <span data-ttu-id="c0eb6-169">Dê ao recurso de armazenamento local um nome exclusivo e um tamanho adequado para sua tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-169">Give the local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="c0eb6-170">Para usar um recurso de armazenamento local em sua tarefa de inicialização, será necessário criar uma variável de ambiente para fazer referência ao local do recurso de armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-170">To use a local storage resource in your startup task, you need to create an environment variable to reference the local storage resource location.</span></span> <span data-ttu-id="c0eb6-171">Em seguida, a tarefa de Inicialização e o aplicativo podem ler e gravar arquivos no recurso de armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-171">Then the startup task and the application are able to read and write files to the local storage resource.</span></span>

<span data-ttu-id="c0eb6-172">As seções relevantes do arquivo **ServiceDefinition.csdef** são mostradas aqui:</span><span class="sxs-lookup"><span data-stu-id="c0eb6-172">The relevant sections of the **ServiceDefinition.csdef** file are shown here:</span></span>

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

<span data-ttu-id="c0eb6-173">Como um exemplo, esse arquivo em lotes **Startup.cmd** usa a variável de ambiente **PathToStartupStorage** para criar o arquivo **MyTest.txt** no armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-173">As an example, this **Startup.cmd** batch file uses the **PathToStartupStorage** environment variable to create the file **MyTest.txt** on the local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into the MyTest.txt file which will be in the    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed to by the PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO The contents of the PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit the batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="c0eb6-174">Você pode acessar a pasta de armazenamento local do SDK do Azure usando o método [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0eb6-174">You can access local storage folder from the Azure SDK by using the [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-the-emulator-or-cloud"></a><span data-ttu-id="c0eb6-175">Executar no emulador ou na nuvem</span><span class="sxs-lookup"><span data-stu-id="c0eb6-175">Run in the emulator or cloud</span></span>
<span data-ttu-id="c0eb6-176">Você pode fazer com que sua tarefa de inicialização execute etapas diferentes quando estiver funcionando na nuvem em comparação a quando estiver no emulador de computação.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-176">You can have your startup task perform different steps when it is operating in the cloud compared to when it is in the compute emulator.</span></span> <span data-ttu-id="c0eb6-177">Por exemplo, convém usar uma cópia atualizada dos dados SQL somente durante a execução no emulador.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-177">For example, you may want to use a fresh copy of your SQL data only when running in the emulator.</span></span> <span data-ttu-id="c0eb6-178">Ou você talvez queira fazer alguma otimização de desempenho para a nuvem que não seja necessária na execução no emulador.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-178">Or you may want to do some performance optimizations for the cloud that you don't need to do when running in the emulator.</span></span>

<span data-ttu-id="c0eb6-179">Essa capacidade de executar ações diferentes no emulador de computação e na nuvem pode ser obtida criando uma variável de ambiente no arquivo [Servicedefinition].</span><span class="sxs-lookup"><span data-stu-id="c0eb6-179">This ability to perform different actions on the compute emulator and the cloud can be accomplished by creating an environment variable in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="c0eb6-180">Você testa então essa variável de ambiente para um valor em sua tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="c0eb6-181">Para criar a variável de ambiente, adicione o elemento [Variable]/[RoleInstanceValue] e crie um valor XPath de `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-181">To create the environment variable, add the [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="c0eb6-182">O valor da variável de ambiente **%ComputeEmulatorRunning%** é `true` na execução no emulador de computação e `false` na execução na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-182">The value of the **%ComputeEmulatorRunning%** environment variable is `true` when running on the compute emulator, and `false` when running on the cloud.</span></span>

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

<span data-ttu-id="c0eb6-183">Agora a tarefa pode verificar a variável de ambiente **%ComputeEmulatorRunning%** para executar ações diferentes com base na função estar em execução na nuvem ou no emulador.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-183">The task can now check the **%ComputeEmulatorRunning%** environment variable to perform different actions based on whether the role is running in the cloud or the emulator.</span></span> <span data-ttu-id="c0eb6-184">A seguir, um script de shell .cmd que verifica essa variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on the compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on the compute emulator. Perform tasks that must be run only in the compute emulator.
) ELSE (
    REM   This task is running on the cloud. Perform tasks that must be run only in the cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="c0eb6-185">Detectar se a tarefa já foi executada</span><span class="sxs-lookup"><span data-stu-id="c0eb6-185">Detect that your task has already run</span></span>
<span data-ttu-id="c0eb6-186">A função pode ser reciclada sem uma reinicialização, fazendo com que suas tarefas de inicialização sejam executadas novamente.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-186">The role may recycle without a reboot causing your startup tasks to run again.</span></span> <span data-ttu-id="c0eb6-187">Não há um sinalizador para indicar se uma tarefa já foi executada na VM de host.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-187">There is no flag to indicate that a task has already run on the hosting VM.</span></span> <span data-ttu-id="c0eb6-188">Talvez você tenha algumas tarefas onde não importará se elas forem executadas várias vezes.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="c0eb6-189">No entanto, você poderá encontrar uma situação em que precisará impedir que uma tarefa seja executada mais de uma vez.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-189">However, you may run into a situation where you need to prevent a task from running more than once.</span></span>

<span data-ttu-id="c0eb6-190">A maneira mais simples de detectar se uma tarefa já foi executada é criar um arquivo na pasta **%TEMP%** quando a tarefa for bem-sucedida e procurá-lo no início da tarefa.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-190">The simplest way to detect that a task has already run is to create a file in the **%TEMP%** folder when the task is successful and look for it at the start of the task.</span></span> <span data-ttu-id="c0eb6-191">A seguir, um script de shell cmd de exemplo que faz isso para você.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-191">Here is a sample cmd shell script that does that for you.</span></span>

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
  REM   The application installed without error. Create a file to indicate that the task
  REM   does not need to be run again.

  ECHO This line will create a file to indicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log the error and exit with the error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a><span data-ttu-id="c0eb6-192">Práticas recomendadas para tarefas</span><span class="sxs-lookup"><span data-stu-id="c0eb6-192">Task best practices</span></span>
<span data-ttu-id="c0eb6-193">A seguir, algumas práticas recomendadas que você deve seguir ao configurar a tarefa para sua função Web ou de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="c0eb6-194">Sempre registrar em log as atividades de inicialização</span><span class="sxs-lookup"><span data-stu-id="c0eb6-194">Always log startup activities</span></span>
<span data-ttu-id="c0eb6-195">O Visual Studio não fornece um depurador para percorrer arquivos em lotes e, portanto, será bom ter tantos dados sobre a operação de arquivos em lotes quanto possível.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-195">Visual Studio does not provide a debugger to step through batch files, so it's good to get as much data on the operation of batch files as possible.</span></span> <span data-ttu-id="c0eb6-196">O registro em log da saída de arquivos em lotes, **stdout** e **stderr**, pode fornecer informações importantes ao tentar depurar e corrigir arquivos em lotes.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-196">Logging the output of batch files, both **stdout** and **stderr**, can give you important information when trying to debug and fix batch files.</span></span> <span data-ttu-id="c0eb6-197">Para registrar em log **stdout** e **stderr** para o arquivo StartupLog.txt no diretório apontado pela variável de ambiente **%TEMP%**, adicione o texto `>>  "%TEMP%\\StartupLog.txt" 2>&1` ao final de linhas específicas que deseja registrar em log.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-197">To log both **stdout** and **stderr** to the StartupLog.txt file in the directory pointed to by the **%TEMP%** environment variable, add the text `>>  "%TEMP%\\StartupLog.txt" 2>&1` to the end of specific lines you want to log.</span></span> <span data-ttu-id="c0eb6-198">Por exemplo, para executar setup.exe no diretório **%PathToApp1Install%** :</span><span class="sxs-lookup"><span data-stu-id="c0eb6-198">For example, to execute setup.exe in the **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="c0eb6-199">Para simplificar o xml, você pode criar um arquivo wrapper *cmd* que chama todas as tarefas de inicialização, juntamente com o registro em log, e garante que cada tarefa filho compartilhe as mesmas variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-199">To simplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares the same environment variables.</span></span>

<span data-ttu-id="c0eb6-200">Porém, talvez você ache incômodo usar `>> "%TEMP%\StartupLog.txt" 2>&1` ao fim de cada tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-200">You may find it annoying though to use `>> "%TEMP%\StartupLog.txt" 2>&1` on the end of each startup task.</span></span> <span data-ttu-id="c0eb6-201">Você pode impor o log de tarefas criando um invólucro que manipula o registro em log para você.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="c0eb6-202">Este wrapper chama o arquivo de lote real que você deseja executar.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-202">This wrapper calls the real batch file you want to run.</span></span> <span data-ttu-id="c0eb6-203">Nenhuma saída do arquivo de lote de destino será redirecionada para o arquivo *startuplog*.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-203">Any output from the target batch file will be redirected to the *Startuplog.txt* file.</span></span>

<span data-ttu-id="c0eb6-204">O exemplo a seguir mostra como redirecionar todas as saídas de um arquivo em lotes de inicialização.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-204">The following example shows how to redirect all output from a startup batch file.</span></span> <span data-ttu-id="c0eb6-205">Neste exemplo, o arquivo ServerDefinition.csdef cria uma tarefa de inicialização que chama *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-205">In this example, the ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="c0eb6-206">*logwrap.cmd* chama *Startup2.cmd*, redirecionando toda a saída para **%TEMP%\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output to **%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="c0eb6-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="c0eb6-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="c0eb6-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="c0eb6-208">**logwrap.cmd:**</span></span>

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output to the StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call the child command batch file, redirecting all output to the StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log the completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log the error.
   ECHO [%date% %time%] An error occurred. The ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

<span data-ttu-id="c0eb6-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="c0eb6-209">**Startup2.cmd:**</span></span>

```cmd
@ECHO OFF

REM   This is the batch file where the startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in the directory pointed to by the TEMP environment variable.

REM   If an error occurs, the following command will pass the ERRORLEVEL back to the
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

<span data-ttu-id="c0eb6-210">Exemplo de saída no arquivo **Startuplog**:</span><span class="sxs-lookup"><span data-stu-id="c0eb6-210">Sample output in the **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="c0eb6-211">O arquivo **Startuplog** está localizado na pasta *C:\Resources\temp\\{role identifier}\RoleTemp*.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-211">The **StartupLog.txt** file is located in the *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="c0eb6-212">Definir executionContext adequadamente para tarefas de inicialização</span><span class="sxs-lookup"><span data-stu-id="c0eb6-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="c0eb6-213">Definir privilégios adequadamente para a tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-213">Set privileges appropriately for the startup task.</span></span> <span data-ttu-id="c0eb6-214">Às vezes, as tarefas de inicialização devem ser executadas com privilégios elevados, mesmo que a função seja executada com privilégios normais.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-214">Sometimes startup tasks must run with elevated privileges even though the role runs with normal privileges.</span></span>

<span data-ttu-id="c0eb6-215">A ferramenta de linha de comando [executionContext][Task] define o nível de privilégio da tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-215">The [executionContext][Task] attribute sets the privilege level of the startup task.</span></span> <span data-ttu-id="c0eb6-216">A utilização de `executionContext="limited"` significa que a tarefa de inicialização tem o mesmo nível de privilégio que a função.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-216">Using `executionContext="limited"` means the startup task has the same privilege level as the role.</span></span> <span data-ttu-id="c0eb6-217">A utilização de `executionContext="elevated"` significa que a tarefa de inicialização tem privilégios de administrador, o que permite que a tarefa de inicialização execute tarefas de administrador sem conceder privilégios de administrador à sua função.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-217">Using `executionContext="elevated"` means the startup task has administrator privileges, which allows the startup task to perform administrator tasks without giving administrator privileges to your role.</span></span>

<span data-ttu-id="c0eb6-218">Um exemplo de uma tarefa de inicialização que exija privilégios elevados é uma tarefa de inicialização que usa **AppCmd.exe** para configurar o IIS.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** to configure IIS.</span></span> <span data-ttu-id="c0eb6-219">**AppCmd.exe** requer `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-the-appropriate-tasktype"></a><span data-ttu-id="c0eb6-220">Usar o taskType adequado</span><span class="sxs-lookup"><span data-stu-id="c0eb6-220">Use the appropriate taskType</span></span>
<span data-ttu-id="c0eb6-221">A ferramenta de linha de comando [taskType][Task] determina a maneira como a tarefa de inicialização é executada.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-221">The [taskType][Task] attribute determines the way the startup task is executed.</span></span> <span data-ttu-id="c0eb6-222">Há três valores: **simples**, **segundo plano** e **primeiro plano**.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="c0eb6-223">As tarefas em primeiro e segundo plano são iniciadas de forma assíncrona e as tarefas simples são executadas de forma síncrona, uma de cada vez.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-223">The background and foreground tasks are started asynchronously, and then the simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="c0eb6-224">Com as tarefas de inicialização **simples**, você pode definir a ordem na qual as tarefas são executadas pela ordem na qual as tarefas são listadas no arquivo ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-224">With **simple** startup tasks, you can set the order in which the tasks run by the order in which the tasks are listed in the ServiceDefinition.csdef file.</span></span> <span data-ttu-id="c0eb6-225">Se uma tarefa **simples** terminar com um código de saída diferente de zero, o procedimento de inicialização será interrompido e a função não será iniciada.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-225">If a **simple** task ends with a non-zero exit code, then the startup procedure stops and the role does not start.</span></span>

<span data-ttu-id="c0eb6-226">A diferença entre as tarefas de inicialização em **segundo plano** e em **primeiro plano** é que as tarefas de inicialização em **primeiro plano** mantêm a função em execução até a tarefa em **primeiro plano** ser encerrada.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-226">The difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep the role running until the **foreground** task ends.</span></span> <span data-ttu-id="c0eb6-227">Isso também significa que, se a tarefa em **primeiro plano** congelar ou falhar, a função não será reciclada até a tarefa em **primeiro plano** ser forçada a fechar.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-227">This also means that if the **foreground** task hangs or crashes, the role will not recycle until the **foreground** task is forced closed.</span></span> <span data-ttu-id="c0eb6-228">Por esse motivo, as tarefas em **segundo plano** são recomendadas para tarefas de inicialização assíncronas, a menos que você precise desse recurso da tarefa em **primeiro plano**.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of the **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="c0eb6-229">Encerrar arquivos em lotes com EXIT /B 0</span><span class="sxs-lookup"><span data-stu-id="c0eb6-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="c0eb6-230">A função só será iniciada se o **errorlevel** de cada uma de suas tarefas de inicialização simples for zero.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-230">The role will only start if the **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="c0eb6-231">Nem todos os programas definem o **errorlevel** (código de saída) corretamente e, portanto, o arquivo em lotes deverá terminar com um `EXIT /B 0` se tudo tiver sido executado corretamente.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-231">Not all programs set the **errorlevel** (exit code) correctly, so the batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="c0eb6-232">Um `EXIT /B 0` ausente no final de um arquivo em lotes de inicialização é uma causa comum de funções que não são iniciadas.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-232">A missing `EXIT /B 0` at the end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="c0eb6-233">Observei que arquivos em lotes aninhados às vezes travarm ao usar o parâmetro `/B`.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-233">I've noticed that nested batch files sometimes hang when using the `/B` parameter.</span></span> <span data-ttu-id="c0eb6-234">Convém verificar se esse problema de suspensão não acontece se outro arquivo em lotes chama o arquivo em lotes atual, como quando você usa o [wrapper de log](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="c0eb6-234">You may want to make sure that this hang problem does not happen if another batch file calls your current batch file, like if you use the [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="c0eb6-235">Você pode omitir o parâmetro `/B` nesse caso.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-235">You can omit the `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-to-run-more-than-once"></a><span data-ttu-id="c0eb6-236">Esperar que tarefas de inicialização sejam executadas mais de uma vez</span><span class="sxs-lookup"><span data-stu-id="c0eb6-236">Expect startup tasks to run more than once</span></span>
<span data-ttu-id="c0eb6-237">Nem todas as reciclagens de função incluem uma reinicialização, mas todas as reciclagens incluem a execução de todas as tarefas de inicialização.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="c0eb6-238">Isso significa que deve ser possível executar as tarefas de inicialização várias vezes entre as reinicializações sem problemas.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-238">This means that startup tasks must be able to run multiple times between reboots without any problems.</span></span> <span data-ttu-id="c0eb6-239">Isso é discutido na [seção anterior](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="c0eb6-239">This is discussed in the [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-to-store-files-that-must-be-accessed-in-the-role"></a><span data-ttu-id="c0eb6-240">Usar o armazenamento local para armazenar arquivos que devem ser acessados na função</span><span class="sxs-lookup"><span data-stu-id="c0eb6-240">Use local storage to store files that must be accessed in the role</span></span>
<span data-ttu-id="c0eb6-241">Se você quiser copiar ou criar um arquivo enquanto sua tarefa de inicialização estiver acessível para sua função, esse arquivo deverá ser colocado no armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-241">If you want to copy or create a file during your startup task that is then accessible to your role, then that file must be placed in local storage.</span></span> <span data-ttu-id="c0eb6-242">Confira a [seção anterior](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="c0eb6-242">See the [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0eb6-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c0eb6-243">Next steps</span></span>
<span data-ttu-id="c0eb6-244">Examine o [modelo de serviço e o pacote da nuvem](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="c0eb6-244">Review the cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="c0eb6-245">Saiba mais sobre o funcionamento de [Tarefas](cloud-services-startup-tasks.md) .</span><span class="sxs-lookup"><span data-stu-id="c0eb6-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="c0eb6-246">[Crie e implante](cloud-services-how-to-create-deploy-portal.md) seu pacote de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c0eb6-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

<span data-ttu-id="c0eb6-247">[Servicedefinition]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="c0eb6-247">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="c0eb6-248">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="c0eb6-248">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
<span data-ttu-id="c0eb6-249">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="c0eb6-249">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="c0eb6-250">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="c0eb6-250">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="c0eb6-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="c0eb6-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
<span data-ttu-id="c0eb6-252">[EndPoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span><span class="sxs-lookup"><span data-stu-id="c0eb6-252">[Endpoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span></span>
<span data-ttu-id="c0eb6-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span><span class="sxs-lookup"><span data-stu-id="c0eb6-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span></span>
<span data-ttu-id="c0eb6-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span><span class="sxs-lookup"><span data-stu-id="c0eb6-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span></span>
<span data-ttu-id="c0eb6-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="c0eb6-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
