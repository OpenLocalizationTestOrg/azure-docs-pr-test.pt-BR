---
title: "Executar Tarefas de Inicialização nos Serviços de Nuvem do Azure | Microsoft Docs"
description: "As tarefas de inicialização ajudam a preparar o ambiente de serviço de nuvem para seu aplicativo. Isso mostra o funcionamento das tarefas de inicialização e como criá-las"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 1c1b3aa86dc8211de0c07c9fb68da5685c86f551
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="bb684-104">Como configurar e executar tarefas de inicialização para um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="bb684-104">How to configure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="bb684-105">Você pode usar as tarefas de inicialização para executar operações antes do início de uma função.</span><span class="sxs-lookup"><span data-stu-id="bb684-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="bb684-106">As operações que talvez você queira executar incluem a instalação de um componente, o registro de componentes COM, a configuração de chaves do Registro ou o início de um processo de longa duração.</span><span class="sxs-lookup"><span data-stu-id="bb684-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="bb684-107">As tarefas de inicialização não são aplicáveis às Máquinas Virtuais, apenas às funções Web e de Trabalho do Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="bb684-107">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="bb684-108">Como funcionam as tarefas de inicialização</span><span class="sxs-lookup"><span data-stu-id="bb684-108">How startup tasks work</span></span>
<span data-ttu-id="bb684-109">As tarefas de inicialização são as ações executadas antes de suas funções começarem e são definidas no arquivo [ServiceDefinition.csdef] usando o elemento [Task] dentro do elemento [Startup].</span><span class="sxs-lookup"><span data-stu-id="bb684-109">Startup tasks are actions that are taken before your roles begin and are defined in the [ServiceDefinition.csdef] file by using the [Task] element within the [Startup] element.</span></span> <span data-ttu-id="bb684-110">Com frequência, as tarefas de inicialização são arquivos em lotes, mas elas também podem ser aplicativos de console ou arquivos em lotes que iniciam scripts do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb684-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="bb684-111">As variáveis de ambiente passam informações para uma tarefa de inicialização e o armazenamento local pode ser usado para transmitir informações para fora de uma tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="bb684-111">Environment variables pass information into a startup task, and local storage can be used to pass information out of a startup task.</span></span> <span data-ttu-id="bb684-112">Por exemplo, uma variável de ambiente pode especificar o caminho para um programa que você deseja instalar e arquivos podem ser gravados no armazenamento local que poderá então ser lido posteriormente por suas funções.</span><span class="sxs-lookup"><span data-stu-id="bb684-112">For example, an environment variable can specify the path to a program you want to install, and files can be written to local storage that can then be read later by your roles.</span></span>

<span data-ttu-id="bb684-113">Sua tarefa de inicialização pode registrar informações e erros no diretório especificado pela variável de ambiente **TEMP** .</span><span class="sxs-lookup"><span data-stu-id="bb684-113">Your startup task can log information and errors to the directory specified by the **TEMP** environment variable.</span></span> <span data-ttu-id="bb684-114">Durante a tarefa de inicialização, a variável de ambiente **TEMP** determina o diretório *C:\\Resources\\temp\\[guid].[nomefunção]\\RoleTemp* ao executar na nuvem.</span><span class="sxs-lookup"><span data-stu-id="bb684-114">During the startup task, the **TEMP** environment variable resolves to the *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on the cloud.</span></span>

<span data-ttu-id="bb684-115">As tarefas de inicialização também podem ser executadas várias vezes entre as reinicializações.</span><span class="sxs-lookup"><span data-stu-id="bb684-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="bb684-116">Por exemplo, a tarefa de inicialização será executada sempre que a função for reciclada, e as reciclagens de função nem sempre incluirão uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="bb684-116">For example, the startup task will be run each time the role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="bb684-117">As tarefas de inicialização devem ser gravadas de uma maneira que permita que sejam executadas diversas vezes sem problemas.</span><span class="sxs-lookup"><span data-stu-id="bb684-117">Startup tasks should be written in a way that allows them to run several times without problems.</span></span>

<span data-ttu-id="bb684-118">As tarefas de inicialização devem terminar com um **errorlevel** (ou código de saída) zero para que o processo de inicialização seja concluído.</span><span class="sxs-lookup"><span data-stu-id="bb684-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for the startup process to complete.</span></span> <span data-ttu-id="bb684-119">Se uma tarefa de inicialização terminar com um **errorlevel**diferente de zero, a função não será iniciada.</span><span class="sxs-lookup"><span data-stu-id="bb684-119">If a startup task ends with a non-zero **errorlevel**, the role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="bb684-120">Ordem de inicialização de função</span><span class="sxs-lookup"><span data-stu-id="bb684-120">Role startup order</span></span>
<span data-ttu-id="bb684-121">A seguir, o procedimento de inicialização da função no Azure:</span><span class="sxs-lookup"><span data-stu-id="bb684-121">The following lists the role startup procedure in Azure:</span></span>

1. <span data-ttu-id="bb684-122">A instância está marcada como **Iniciando** e não recebe o tráfego.</span><span class="sxs-lookup"><span data-stu-id="bb684-122">The instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="bb684-123">Todas as tarefas de inicialização são executadas de acordo com o atributo **taskType** .</span><span class="sxs-lookup"><span data-stu-id="bb684-123">All startup tasks are executed according to their **taskType** attribute.</span></span>
   
   * <span data-ttu-id="bb684-124">As tarefas **simples** são executadas de forma síncrona, uma de cada vez.</span><span class="sxs-lookup"><span data-stu-id="bb684-124">The **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="bb684-125">As tarefas em **segundo plano** e **primeiro plano** são iniciadas de forma assíncrona, paralelas com a tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="bb684-125">The **background** and **foreground** tasks are started asynchronously, parallel to the startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="bb684-126">O IIS pode não estar totalmente configurado durante a fase de tarefas de inicialização no processo de inicialização e, portanto, os dados específicos da função podem não estar disponíveis.</span><span class="sxs-lookup"><span data-stu-id="bb684-126">IIS may not be fully configured during the startup task stage in the startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="bb684-127">As tarefas de inicialização que exigem dados específicos da função devem usar [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb684-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="bb684-128">O processo de host da função é iniciado e o site é criado no IIS.</span><span class="sxs-lookup"><span data-stu-id="bb684-128">The role host process is started and the site is created in IIS.</span></span>
4. <span data-ttu-id="bb684-129">O método [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) é chamado.</span><span class="sxs-lookup"><span data-stu-id="bb684-129">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="bb684-130">A instância é marcada como **Pronta** e o tráfego é roteado para a instância.</span><span class="sxs-lookup"><span data-stu-id="bb684-130">The instance is marked as **Ready** and traffic is routed to the instance.</span></span>
6. <span data-ttu-id="bb684-131">O método [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) é chamado.</span><span class="sxs-lookup"><span data-stu-id="bb684-131">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="bb684-132">Exemplo de uma tarefa de inicialização</span><span class="sxs-lookup"><span data-stu-id="bb684-132">Example of a startup task</span></span>
<span data-ttu-id="bb684-133">As tarefas de inicialização são definidas no arquivo [ServiceDefinition.csdef] , no elemento **Tarefa** .</span><span class="sxs-lookup"><span data-stu-id="bb684-133">Startup tasks are defined in the [ServiceDefinition.csdef] file, in the **Task** element.</span></span> <span data-ttu-id="bb684-134">O atributo **commandLine** especifica o nome e os parâmetros do arquivo de inicialização em lote ou do comando de console, o atributo **executionContext** especifica o nível de privilégio da tarefa de inicialização e o atributo **taskType** especifica como a tarefa será executada.</span><span class="sxs-lookup"><span data-stu-id="bb684-134">The **commandLine** attribute specifies the name and parameters of the startup batch file or console command, the **executionContext** attribute specifies the privilege level of the startup task, and the **taskType** attribute specifies how the task will be executed.</span></span>

<span data-ttu-id="bb684-135">Neste exemplo, uma variável de ambiente, **MyVersionNumber**, é criada para a tarefa de inicialização e definida para o valor "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="bb684-135">In this example, an environment variable, **MyVersionNumber**, is created for the startup task and set to the value "**1.0.0.0**".</span></span>

<span data-ttu-id="bb684-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="bb684-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="bb684-137">No exemplo a seguir, o arquivo em lotes **Startup.cmd** grava a linha "A versão atual é 1.0.0.0" no arquivo StartupLog.txt no diretório especificado pela variável de ambiente TEMP.</span><span class="sxs-lookup"><span data-stu-id="bb684-137">In the following example, the **Startup.cmd** batch file writes the line "The current version is 1.0.0.0" to the StartupLog.txt file in the directory specified by the TEMP environment variable.</span></span> <span data-ttu-id="bb684-138">A linha `EXIT /B 0` garante que a tarefa de inicialização termine com um **errorlevel** zero.</span><span class="sxs-lookup"><span data-stu-id="bb684-138">The `EXIT /B 0` line ensures that the startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO The current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="bb684-139">No Visual Studio, a propriedade **Copy to Output Directory** do arquivo de inicialização em lote deve ser definida para **Copy Always** para verificar se o arquivo de inicialização em lote está implantado corretamente em seu projeto no Azure (**approot\\bin** para as funções Web e **approot** para as funções de trabalho).</span><span class="sxs-lookup"><span data-stu-id="bb684-139">In Visual Studio, the **Copy to Output Directory** property for your startup batch file should be set to **Copy Always** to be sure that your startup batch file is properly deployed to your project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="bb684-140">Descrição dos atributos da tarefa</span><span class="sxs-lookup"><span data-stu-id="bb684-140">Description of task attributes</span></span>
<span data-ttu-id="bb684-141">A seguir, a descrição dos atributos do elemento **Task** do arquivo [ServiceDefinition.csdef] :</span><span class="sxs-lookup"><span data-stu-id="bb684-141">The following describes the attributes of the **Task** element in the [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="bb684-142">**commandLine** - especifica a linha de comando para a tarefa de inicialização:</span><span class="sxs-lookup"><span data-stu-id="bb684-142">**commandLine** - Specifies the command line for the startup task:</span></span>

* <span data-ttu-id="bb684-143">O comando, com parâmetros de linha de comando opcionais, que inicia a tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="bb684-143">The command, with optional command line parameters, which begins the startup task.</span></span>
* <span data-ttu-id="bb684-144">Geralmente, esse é o nome do arquivo de um arquivo em lotes .cmd ou .bat.</span><span class="sxs-lookup"><span data-stu-id="bb684-144">Frequently this is the filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="bb684-145">A tarefa é relativa à pasta Bin do \\AppRoot da implantação.</span><span class="sxs-lookup"><span data-stu-id="bb684-145">The task is relative to the AppRoot\\Bin folder for the deployment.</span></span> <span data-ttu-id="bb684-146">As variáveis de ambiente não são expandidas para a determinação do caminho e do arquivo da tarefa.</span><span class="sxs-lookup"><span data-stu-id="bb684-146">Environment variables are not expanded in determining the path and file of the task.</span></span> <span data-ttu-id="bb684-147">Se a expansão de ambiente for necessária, você poderá criar um script .cmd pequeno que chame sua tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="bb684-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="bb684-148">Pode ser um aplicativo de console ou um arquivo em lotes que inicie um [script do PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="bb684-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="bb684-149">**executionContext** - especifica o nível de privilégio para a tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="bb684-149">**executionContext** - Specifies the privilege level for the startup task.</span></span> <span data-ttu-id="bb684-150">O nível de privilégio pode ser limitado ou elevado:</span><span class="sxs-lookup"><span data-stu-id="bb684-150">The privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="bb684-151">**limitado**</span><span class="sxs-lookup"><span data-stu-id="bb684-151">**limited**</span></span>  
  <span data-ttu-id="bb684-152">A tarefa de inicialização é executada com os mesmos privilégios da função.</span><span class="sxs-lookup"><span data-stu-id="bb684-152">The startup task runs with the same privileges as the role.</span></span> <span data-ttu-id="bb684-153">Quando o atributo **executionContext** do elemento [Runtime] também é **limitado**, os privilégios do usuário são usados.</span><span class="sxs-lookup"><span data-stu-id="bb684-153">When the **executionContext** attribute for the [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="bb684-154">**elevado**</span><span class="sxs-lookup"><span data-stu-id="bb684-154">**elevated**</span></span>  
  <span data-ttu-id="bb684-155">A tarefa de inicialização é executada com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="bb684-155">The startup task runs with administrator privileges.</span></span> <span data-ttu-id="bb684-156">Isso permite que as tarefas de inicialização instalem programas, façam alterações de configuração no IIS, executem alterações no Registro e outras tarefas no nível de administrador sem aumentar o nível de privilégio da própria função.</span><span class="sxs-lookup"><span data-stu-id="bb684-156">This allows startup tasks to install programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing the privilege level of the role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="bb684-157">O nível de privilégio de uma tarefa de inicialização não precisa ser igual ao da própria função.</span><span class="sxs-lookup"><span data-stu-id="bb684-157">The privilege level of a startup task does not need to be the same as the role itself.</span></span>
> 
> 

<span data-ttu-id="bb684-158">**taskType** - especifica a maneira como uma tarefa de inicialização é executada.</span><span class="sxs-lookup"><span data-stu-id="bb684-158">**taskType** - Specifies the way a startup task is executed.</span></span>

* <span data-ttu-id="bb684-159">**simpless**</span><span class="sxs-lookup"><span data-stu-id="bb684-159">**simple**</span></span>  
  <span data-ttu-id="bb684-160">As tarefas são executadas de forma síncrona, uma de cada vez, na ordem especificada no arquivo [ServiceDefinition.csdef] .</span><span class="sxs-lookup"><span data-stu-id="bb684-160">Tasks are executed synchronously, one at a time, in the order specified in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="bb684-161">Quando uma tarefa de inicialização **simples**termina com um **errorlevel** zero, a próxima tarefa de inicialização **simples** é executada.</span><span class="sxs-lookup"><span data-stu-id="bb684-161">When one **simple** startup task ends with an **errorlevel** of zero, the next **simple** startup task is executed.</span></span> <span data-ttu-id="bb684-162">Se não houver nenhum mais tarefas de inicialização **simples** a serem executadas, então a função será iniciada.</span><span class="sxs-lookup"><span data-stu-id="bb684-162">If there are no more **simple** startup tasks to execute, then the role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="bb684-163">Se a tarefa **simples** terminar com um **errorlevel** diferente de zero, a instância será bloqueada.</span><span class="sxs-lookup"><span data-stu-id="bb684-163">If the **simple** task ends with a non-zero **errorlevel**, the instance will be blocked.</span></span> <span data-ttu-id="bb684-164">As tarefas de inicialização **simples** subsequentes , e a própria função, não serão iniciadas.</span><span class="sxs-lookup"><span data-stu-id="bb684-164">Subsequent **simple** startup tasks, and the role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="bb684-165">Para garantir que o arquivo em lote terminará com um **errorlevel** zero, execute o comando `EXIT /B 0` no final do processo do arquivo em lote.</span><span class="sxs-lookup"><span data-stu-id="bb684-165">To ensure that your batch file ends with an **errorlevel** of zero, execute the command `EXIT /B 0` at the end of your batch file process.</span></span>
* <span data-ttu-id="bb684-166">**segundo plano**</span><span class="sxs-lookup"><span data-stu-id="bb684-166">**background**</span></span>  
  <span data-ttu-id="bb684-167">As tarefas são executadas de forma assíncrona, em paralelo com a inicialização da função.</span><span class="sxs-lookup"><span data-stu-id="bb684-167">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span>
* <span data-ttu-id="bb684-168">**primeiro plano**</span><span class="sxs-lookup"><span data-stu-id="bb684-168">**foreground**</span></span>  
  <span data-ttu-id="bb684-169">As tarefas são executadas de forma assíncrona, em paralelo com a inicialização da função.</span><span class="sxs-lookup"><span data-stu-id="bb684-169">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span> <span data-ttu-id="bb684-170">A principal diferença entre uma tarefa em **primeiro plano** e **segundo plano** é que uma tarefa em **primeiro plano** evita que a função recicle ou finalize até que a tarefa seja concluída.</span><span class="sxs-lookup"><span data-stu-id="bb684-170">The key difference between a **foreground** and a **background** task is that a **foreground** task prevents the role from recycling or shutting down until the task has ended.</span></span> <span data-ttu-id="bb684-171">As tarefas em **segundo plano** não têm essa restrição.</span><span class="sxs-lookup"><span data-stu-id="bb684-171">The **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="bb684-172">Variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="bb684-172">Environment variables</span></span>
<span data-ttu-id="bb684-173">As variáveis de ambiente são uma maneira de passar informações para uma tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="bb684-173">Environment variables are a way to pass information to a startup task.</span></span> <span data-ttu-id="bb684-174">Por exemplo, você pode colocar o caminho para um blob que contenha um programa a ser instalado, ou números de porta que sua função usará, ou configurações para controlar recursos de sua tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="bb684-174">For example, you can put the path to a blob that contains a program to install, or port numbers that your role will use, or settings to control features of your startup task.</span></span>

<span data-ttu-id="bb684-175">Há dois tipos de variáveis de ambiente para tarefas de inicialização; variáveis de ambiente estáticas e variáveis de ambiente baseadas nos membros da classe [RoleEnvironment] .</span><span class="sxs-lookup"><span data-stu-id="bb684-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of the [RoleEnvironment] class.</span></span> <span data-ttu-id="bb684-176">Ambas estão na seção [Environment] do arquivo [ServiceDefinition.csdef] e usam o elemento [Variable] e o atributo **name**.</span><span class="sxs-lookup"><span data-stu-id="bb684-176">Both are in the [Environment] section of the [ServiceDefinition.csdef] file, and both use the [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="bb684-177">As variáveis de ambiente estáticas usam o atributo **value** do elemento [Variable] .</span><span class="sxs-lookup"><span data-stu-id="bb684-177">Static environment variables uses the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="bb684-178">O exemplo acima cria a variável de ambiente **MyVersionNumber** que tem um valor estático "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="bb684-178">The example above creates the environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="bb684-179">Outro exemplo seria criar uma variável de ambiente **StagingOrProduction** que você pode definir manualmente para os valores de "**preparo**" ou "**produção**" para executar ações diferentes de inicialização com base no valor da variável de ambiente **StagingOrProduction**.</span><span class="sxs-lookup"><span data-stu-id="bb684-179">Another example would be to create a **StagingOrProduction** environment variable which you can manually set to values of "**staging**" or "**production**" to perform different startup actions based on the value of the **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="bb684-180">As variáveis de ambiente baseadas nos membros da classe RoleEnvironment não usam o atributo **value** do elemento [Variable] .</span><span class="sxs-lookup"><span data-stu-id="bb684-180">Environment variables based on members of the RoleEnvironment class do not use the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="bb684-181">Em vez disso, o elemento-filho [RoleInstanceValue], com o devido valor do atributo **XPath**, é usado para criar uma variável de ambiente com base em um membro específico da classe [RoleEnvironment].</span><span class="sxs-lookup"><span data-stu-id="bb684-181">Instead, the [RoleInstanceValue] child element, with the appropriate **XPath** attribute value, are used to create an environment variable based on a specific member of the [RoleEnvironment] class.</span></span> <span data-ttu-id="bb684-182">Os valores do atributo **XPath** para acessar os diversos valores [RoleEnvironment] podem ser encontrados [aqui](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="bb684-182">Values for the **XPath** attribute to access various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="bb684-183">Por exemplo, para criar uma variável de ambiente "**true**" quando a instância está em execução no emulador de computação, e "**false**" quando em execução na nuvem, use os seguintes elementos [Variable] e [RoleInstanceValue] :</span><span class="sxs-lookup"><span data-stu-id="bb684-183">For example, to create an environment variable that is "**true**" when the instance is running in the compute emulator, and "**false**" when running in the cloud, use the following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create the environment variable that informs the startup task whether it is running
                in the Compute Emulator or in the cloud. "%ComputeEmulatorRunning%"=="true" when
                running in the Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in the cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="bb684-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb684-184">Next steps</span></span>
<span data-ttu-id="bb684-185">Saiba como executar algumas [tarefas de inicialização comuns](cloud-services-startup-tasks-common.md) com seu Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="bb684-185">Learn how to perform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="bb684-186">[Empacote](cloud-services-model-and-package.md) seu Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="bb684-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

<span data-ttu-id="bb684-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="bb684-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="bb684-188">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="bb684-188">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
<span data-ttu-id="bb684-189">[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span><span class="sxs-lookup"><span data-stu-id="bb684-189">[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span></span>
<span data-ttu-id="bb684-190">[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span><span class="sxs-lookup"><span data-stu-id="bb684-190">[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span></span>
<span data-ttu-id="bb684-191">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="bb684-191">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="bb684-192">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="bb684-192">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="bb684-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="bb684-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
<span data-ttu-id="bb684-194">[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span><span class="sxs-lookup"><span data-stu-id="bb684-194">[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span></span>
