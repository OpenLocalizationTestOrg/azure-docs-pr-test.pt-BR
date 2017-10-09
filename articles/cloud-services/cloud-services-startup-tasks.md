---
title: "aaaRun tarefas de inicialização nos serviços de nuvem do Azure | Microsoft Docs"
description: "As tarefas de inicialização ajudam a preparar o ambiente de serviço de nuvem para seu aplicativo. Isso ensina como o trabalho de tarefas de inicialização e toomake-los"
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
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="66b70-104">Como as tarefas de inicialização tooconfigure e execução de um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="66b70-104">How tooconfigure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="66b70-105">Você pode usar operações de tooperform de tarefas de inicialização antes do início de uma função.</span><span class="sxs-lookup"><span data-stu-id="66b70-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="66b70-106">Operações que convém tooperform incluem instalação de um componente, registrando componentes COM, chaves do registro de configuração ou iniciar um processo de execução longa.</span><span class="sxs-lookup"><span data-stu-id="66b70-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="66b70-107">Tarefas de inicialização não são aplicáveis tooVirtual máquinas, apenas tooCloud serviço Web e funções de trabalho.</span><span class="sxs-lookup"><span data-stu-id="66b70-107">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="66b70-108">Como funcionam as tarefas de inicialização</span><span class="sxs-lookup"><span data-stu-id="66b70-108">How startup tasks work</span></span>
<span data-ttu-id="66b70-109">Tarefas de inicialização são ações que são executadas antes de suas funções começam e são definidas em hello [servicedefinition. Csdef] arquivo usando Olá [tarefa] elemento dentro do hello [inicialização]elemento.</span><span class="sxs-lookup"><span data-stu-id="66b70-109">Startup tasks are actions that are taken before your roles begin and are defined in hello [ServiceDefinition.csdef] file by using hello [Task] element within hello [Startup] element.</span></span> <span data-ttu-id="66b70-110">Com frequência, as tarefas de inicialização são arquivos em lotes, mas elas também podem ser aplicativos de console ou arquivos em lotes que iniciam scripts do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66b70-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="66b70-111">Variáveis de ambiente transmitem informações em uma tarefa de inicialização e armazenamento local pode ser usado toopass informações fora de uma tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="66b70-111">Environment variables pass information into a startup task, and local storage can be used toopass information out of a startup task.</span></span> <span data-ttu-id="66b70-112">Por exemplo, uma variável de ambiente pode especificar o programa de tooa caminho Olá deseja tooinstall e arquivos podem ser gravados armazenamento toolocal que pode ser lidos posteriormente por suas funções.</span><span class="sxs-lookup"><span data-stu-id="66b70-112">For example, an environment variable can specify hello path tooa program you want tooinstall, and files can be written toolocal storage that can then be read later by your roles.</span></span>

<span data-ttu-id="66b70-113">Sua tarefa de inicialização pode registrar informações e o diretório de toohello de erros especificado pelo Olá **TEMP** variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="66b70-113">Your startup task can log information and errors toohello directory specified by hello **TEMP** environment variable.</span></span> <span data-ttu-id="66b70-114">Durante a tarefa de inicialização de Olá Olá **TEMP** variável de ambiente resolve toohello *c:\\recursos\\temp\\[guid]. [ rolename]\\RoleTemp* diretório quando em execução na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="66b70-114">During hello startup task, hello **TEMP** environment variable resolves toohello *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on hello cloud.</span></span>

<span data-ttu-id="66b70-115">As tarefas de inicialização também podem ser executadas várias vezes entre as reinicializações.</span><span class="sxs-lookup"><span data-stu-id="66b70-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="66b70-116">Por exemplo, Olá inicialização tarefa será executada cada vez Olá função se recicla e a reciclagem de função não pode incluir sempre uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="66b70-116">For example, hello startup task will be run each time hello role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="66b70-117">Tarefas de inicialização devem ser escritas de forma a permitir que eles toorun várias vezes sem problemas.</span><span class="sxs-lookup"><span data-stu-id="66b70-117">Startup tasks should be written in a way that allows them toorun several times without problems.</span></span>

<span data-ttu-id="66b70-118">Tarefas de inicialização devem terminar com uma **errorlevel** (ou código de saída) de zero para Olá toocomplete de processo de inicialização.</span><span class="sxs-lookup"><span data-stu-id="66b70-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for hello startup process toocomplete.</span></span> <span data-ttu-id="66b70-119">Se uma tarefa de inicialização termina com diferente de zero **errorlevel**, Olá função não será iniciada.</span><span class="sxs-lookup"><span data-stu-id="66b70-119">If a startup task ends with a non-zero **errorlevel**, hello role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="66b70-120">Ordem de inicialização de função</span><span class="sxs-lookup"><span data-stu-id="66b70-120">Role startup order</span></span>
<span data-ttu-id="66b70-121">Olá seguindo o procedimento de inicialização de função listas Olá no Azure:</span><span class="sxs-lookup"><span data-stu-id="66b70-121">hello following lists hello role startup procedure in Azure:</span></span>

1. <span data-ttu-id="66b70-122">Olá instância é marcada como **iniciando** e não recebe o tráfego.</span><span class="sxs-lookup"><span data-stu-id="66b70-122">hello instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="66b70-123">Todas as tarefas de inicialização são executadas de acordo com tootheir **taskType** atributo.</span><span class="sxs-lookup"><span data-stu-id="66b70-123">All startup tasks are executed according tootheir **taskType** attribute.</span></span>
   
   * <span data-ttu-id="66b70-124">Olá **simples** tarefas são executadas de forma síncrona, uma de cada vez.</span><span class="sxs-lookup"><span data-stu-id="66b70-124">hello **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="66b70-125">Olá **em segundo plano** e **primeiro plano** tarefas são iniciadas de forma assíncrona, paralelas toohello tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="66b70-125">hello **background** and **foreground** tasks are started asynchronously, parallel toohello startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="66b70-126">O IIS pode não estar totalmente configurado durante a fase de tarefas de inicialização Olá no processo de inicialização hello, para que dados específicos de função podem não estar disponíveis.</span><span class="sxs-lookup"><span data-stu-id="66b70-126">IIS may not be fully configured during hello startup task stage in hello startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="66b70-127">As tarefas de inicialização que exigem dados específicos da função devem usar [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="66b70-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="66b70-128">processo de host de função Hello é iniciado e Olá site é criado no IIS.</span><span class="sxs-lookup"><span data-stu-id="66b70-128">hello role host process is started and hello site is created in IIS.</span></span>
4. <span data-ttu-id="66b70-129">Olá [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) método é chamado.</span><span class="sxs-lookup"><span data-stu-id="66b70-129">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="66b70-130">Olá instância é marcada como **pronto** e o tráfego é roteado toohello instância.</span><span class="sxs-lookup"><span data-stu-id="66b70-130">hello instance is marked as **Ready** and traffic is routed toohello instance.</span></span>
6. <span data-ttu-id="66b70-131">Olá [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método é chamado.</span><span class="sxs-lookup"><span data-stu-id="66b70-131">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="66b70-132">Exemplo de uma tarefa de inicialização</span><span class="sxs-lookup"><span data-stu-id="66b70-132">Example of a startup task</span></span>
<span data-ttu-id="66b70-133">Tarefas de inicialização são definidas no hello [servicedefinition. Csdef] arquivo, em Olá **tarefa** elemento.</span><span class="sxs-lookup"><span data-stu-id="66b70-133">Startup tasks are defined in hello [ServiceDefinition.csdef] file, in hello **Task** element.</span></span> <span data-ttu-id="66b70-134">Olá **commandLine** atributo especifica o nome da saudação e parâmetros do lote de inicialização de saudação do arquivo ou no console de comando, hello **executionContext** atributo especifica o nível de privilégio de saudação de inicialização Olá tarefas e hello **taskType** atributo especifica como Olá tarefa será executada.</span><span class="sxs-lookup"><span data-stu-id="66b70-134">hello **commandLine** attribute specifies hello name and parameters of hello startup batch file or console command, hello **executionContext** attribute specifies hello privilege level of hello startup task, and hello **taskType** attribute specifies how hello task will be executed.</span></span>

<span data-ttu-id="66b70-135">Neste exemplo, uma variável de ambiente **MyVersionNumber**, é criado para a tarefa de inicialização hello e defina o valor de toohello "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="66b70-135">In this example, an environment variable, **MyVersionNumber**, is created for hello startup task and set toohello value "**1.0.0.0**".</span></span>

<span data-ttu-id="66b70-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="66b70-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="66b70-137">Em Olá exemplo a seguir, Olá **Startup.cmd** arquivo em lote grava linha hello "o hello current version is 1.0.0.0" arquivo de StartupLog.txt toohello no diretório de saudação especificado pela variável de ambiente TEMP hello.</span><span class="sxs-lookup"><span data-stu-id="66b70-137">In hello following example, hello **Startup.cmd** batch file writes hello line "hello current version is 1.0.0.0" toohello StartupLog.txt file in hello directory specified by hello TEMP environment variable.</span></span> <span data-ttu-id="66b70-138">Olá `EXIT /B 0` linha garante que essa tarefa de inicialização Olá termina com um **errorlevel** igual a zero.</span><span class="sxs-lookup"><span data-stu-id="66b70-138">hello `EXIT /B 0` line ensures that hello startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="66b70-139">No Visual Studio, Olá **copiar tooOutput diretório** propriedade para o arquivo em lotes de inicialização deve ser definida muito**copiar sempre** toobe-se de que o arquivo em lotes de inicialização esteja adequadamente implantado tooyour projeto no Azure (**approot\\bin** para funções da Web, e **approot** para funções de trabalho).</span><span class="sxs-lookup"><span data-stu-id="66b70-139">In Visual Studio, hello **Copy tooOutput Directory** property for your startup batch file should be set too**Copy Always** toobe sure that your startup batch file is properly deployed tooyour project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="66b70-140">Descrição dos atributos da tarefa</span><span class="sxs-lookup"><span data-stu-id="66b70-140">Description of task attributes</span></span>
<span data-ttu-id="66b70-141">Hello, a seguir descreve os atributos de saudação do hello **tarefa** elemento Olá [servicedefinition. Csdef] arquivo:</span><span class="sxs-lookup"><span data-stu-id="66b70-141">hello following describes hello attributes of hello **Task** element in hello [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="66b70-142">**linha de comando** -Especifica Olá a linha de comando para a tarefa de inicialização hello:</span><span class="sxs-lookup"><span data-stu-id="66b70-142">**commandLine** - Specifies hello command line for hello startup task:</span></span>

* <span data-ttu-id="66b70-143">comando Hello, com parâmetros de linha de comando opcional, que inicia a tarefa de inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="66b70-143">hello command, with optional command line parameters, which begins hello startup task.</span></span>
* <span data-ttu-id="66b70-144">Geralmente, isso é Olá nome do arquivo de um arquivo em lotes. cmd ou. bat.</span><span class="sxs-lookup"><span data-stu-id="66b70-144">Frequently this is hello filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="66b70-145">tarefa de saudação é relativo toohello AppRoot\\pasta Bin para implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="66b70-145">hello task is relative toohello AppRoot\\Bin folder for hello deployment.</span></span> <span data-ttu-id="66b70-146">Variáveis de ambiente não são expandidas para determinar o caminho hello e da tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="66b70-146">Environment variables are not expanded in determining hello path and file of hello task.</span></span> <span data-ttu-id="66b70-147">Se a expansão de ambiente for necessária, você poderá criar um script .cmd pequeno que chame sua tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="66b70-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="66b70-148">Pode ser um aplicativo de console ou um arquivo em lotes que inicie um [script do PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="66b70-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="66b70-149">**executionContext** -Especifica o nível de privilégio Olá para tarefa de inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="66b70-149">**executionContext** - Specifies hello privilege level for hello startup task.</span></span> <span data-ttu-id="66b70-150">nível de privilégio Olá pode ser limitado ou elevado:</span><span class="sxs-lookup"><span data-stu-id="66b70-150">hello privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="66b70-151">**limitado**</span><span class="sxs-lookup"><span data-stu-id="66b70-151">**limited**</span></span>  
  <span data-ttu-id="66b70-152">tarefa de inicialização de saudação é executado com hello mesmo privilégios como função hello.</span><span class="sxs-lookup"><span data-stu-id="66b70-152">hello startup task runs with hello same privileges as hello role.</span></span> <span data-ttu-id="66b70-153">Olá quando **executionContext** atributo Olá [tempo de execução] elemento também é **limitado**, privilégios de usuário são usadas.</span><span class="sxs-lookup"><span data-stu-id="66b70-153">When hello **executionContext** attribute for hello [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="66b70-154">**elevado**</span><span class="sxs-lookup"><span data-stu-id="66b70-154">**elevated**</span></span>  
  <span data-ttu-id="66b70-155">tarefa de inicialização de saudação é executado com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="66b70-155">hello startup task runs with administrator privileges.</span></span> <span data-ttu-id="66b70-156">Isso permite que as tarefas de inicialização tooinstall programas, faça as alterações de configuração do IIS, realizar alterações no registro e outras tarefas de nível de administrador sem aumentar o nível de privilégio de saudação da própria função hello.</span><span class="sxs-lookup"><span data-stu-id="66b70-156">This allows startup tasks tooinstall programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing hello privilege level of hello role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="66b70-157">Olá nível de privilégio de uma tarefa de inicialização não precisa toobe Olá mesmo como função hello em si.</span><span class="sxs-lookup"><span data-stu-id="66b70-157">hello privilege level of a startup task does not need toobe hello same as hello role itself.</span></span>
> 
> 

<span data-ttu-id="66b70-158">**taskType** -Especifica Olá forma uma tarefa de inicialização é executado.</span><span class="sxs-lookup"><span data-stu-id="66b70-158">**taskType** - Specifies hello way a startup task is executed.</span></span>

* <span data-ttu-id="66b70-159">**simpless**</span><span class="sxs-lookup"><span data-stu-id="66b70-159">**simple**</span></span>  
  <span data-ttu-id="66b70-160">Tarefas são executadas de forma síncrona, uma de cada vez, em ordem de saudação especificado no hello [servicedefinition. Csdef] arquivo.</span><span class="sxs-lookup"><span data-stu-id="66b70-160">Tasks are executed synchronously, one at a time, in hello order specified in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="66b70-161">Quando um **simples** tarefa de inicialização termina com um **errorlevel** de zero, em seguida Olá **simples** tarefa de inicialização é executada.</span><span class="sxs-lookup"><span data-stu-id="66b70-161">When one **simple** startup task ends with an **errorlevel** of zero, hello next **simple** startup task is executed.</span></span> <span data-ttu-id="66b70-162">Se houver mais **simples** tooexecute, tarefas de inicialização e a função hello em si será iniciada.</span><span class="sxs-lookup"><span data-stu-id="66b70-162">If there are no more **simple** startup tasks tooexecute, then hello role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="66b70-163">Se hello **simples** tarefa termina com diferente de zero **errorlevel**, Olá instância será bloqueada.</span><span class="sxs-lookup"><span data-stu-id="66b70-163">If hello **simple** task ends with a non-zero **errorlevel**, hello instance will be blocked.</span></span> <span data-ttu-id="66b70-164">Subsequentes **simples** tarefas de inicialização e a função hello em si, não serão iniciado.</span><span class="sxs-lookup"><span data-stu-id="66b70-164">Subsequent **simple** startup tasks, and hello role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="66b70-165">tooensure o arquivo em lotes termina com um **errorlevel** de zero, execute o comando Olá `EXIT /B 0` final de saudação de seu processo de arquivo em lotes.</span><span class="sxs-lookup"><span data-stu-id="66b70-165">tooensure that your batch file ends with an **errorlevel** of zero, execute hello command `EXIT /B 0` at hello end of your batch file process.</span></span>
* <span data-ttu-id="66b70-166">**segundo plano**</span><span class="sxs-lookup"><span data-stu-id="66b70-166">**background**</span></span>  
  <span data-ttu-id="66b70-167">Tarefas são executadas de forma assíncrona, em paralelo com a inicialização de saudação da função hello.</span><span class="sxs-lookup"><span data-stu-id="66b70-167">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span>
* <span data-ttu-id="66b70-168">**primeiro plano**</span><span class="sxs-lookup"><span data-stu-id="66b70-168">**foreground**</span></span>  
  <span data-ttu-id="66b70-169">Tarefas são executadas de forma assíncrona, em paralelo com a inicialização de saudação da função hello.</span><span class="sxs-lookup"><span data-stu-id="66b70-169">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span> <span data-ttu-id="66b70-170">Olá a principal diferença entre um **primeiro plano** e um **em segundo plano** tarefa é que um **primeiro plano** tarefa impede que a função de saudação do reciclado ou desligado até que a tarefa de saudação tem terminou.</span><span class="sxs-lookup"><span data-stu-id="66b70-170">hello key difference between a **foreground** and a **background** task is that a **foreground** task prevents hello role from recycling or shutting down until hello task has ended.</span></span> <span data-ttu-id="66b70-171">Olá **em segundo plano** tarefas não têm essa restrição.</span><span class="sxs-lookup"><span data-stu-id="66b70-171">hello **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="66b70-172">Variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="66b70-172">Environment variables</span></span>
<span data-ttu-id="66b70-173">Variáveis de ambiente são uma tarefa de inicialização do modo toopass informações tooa.</span><span class="sxs-lookup"><span data-stu-id="66b70-173">Environment variables are a way toopass information tooa startup task.</span></span> <span data-ttu-id="66b70-174">Por exemplo, você pode colocar blob Olá de tooa de caminho que contém um tooinstall de programa, ou números de porta que usará a função ou recursos de toocontrol de configurações de sua tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="66b70-174">For example, you can put hello path tooa blob that contains a program tooinstall, or port numbers that your role will use, or settings toocontrol features of your startup task.</span></span>

<span data-ttu-id="66b70-175">Há dois tipos de variáveis de ambiente para tarefas de inicialização. variáveis de ambiente estáticos e variáveis de ambiente com base nos membros de saudação [ RoleEnvironment] classe.</span><span class="sxs-lookup"><span data-stu-id="66b70-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="66b70-176">Ambos são Olá [ambiente] seção Olá [servicedefinition. Csdef] arquivo e ambos Olá use [variável] elemento e **nome** atributo.</span><span class="sxs-lookup"><span data-stu-id="66b70-176">Both are in hello [Environment] section of hello [ServiceDefinition.csdef] file, and both use hello [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="66b70-177">Saudação de usa de variáveis de ambiente estático **valor** atributo de saudação [variável] elemento.</span><span class="sxs-lookup"><span data-stu-id="66b70-177">Static environment variables uses hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="66b70-178">exemplo Hello acima cria a variável de ambiente Olá **MyVersionNumber** que tem um valor estático de "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="66b70-178">hello example above creates hello environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="66b70-179">Outro exemplo seria toocreate um **StagingOrProduction** variável de ambiente que você pode definir manualmente toovalues de "**preparo**"ou"**produção**" tooperform ações diferentes de inicialização com base no valor Olá Olá **StagingOrProduction** variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="66b70-179">Another example would be toocreate a **StagingOrProduction** environment variable which you can manually set toovalues of "**staging**" or "**production**" tooperform different startup actions based on hello value of hello **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="66b70-180">Variáveis de ambiente com base nos membros de saudação classe RoleEnvironment não usam Olá **valor** atributo de saudação [variável] elemento.</span><span class="sxs-lookup"><span data-stu-id="66b70-180">Environment variables based on members of hello RoleEnvironment class do not use hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="66b70-181">Em vez disso, Olá [RoleInstanceValue] elemento filho, com hello apropriado **XPath** valor do atributo, é usada toocreate uma variável de ambiente com base em um membro específico de saudação [ RoleEnvironment] classe.</span><span class="sxs-lookup"><span data-stu-id="66b70-181">Instead, hello [RoleInstanceValue] child element, with hello appropriate **XPath** attribute value, are used toocreate an environment variable based on a specific member of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="66b70-182">Valores para Olá **XPath** atributo tooaccess vários [ RoleEnvironment] valores podem ser encontrados [aqui](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="66b70-182">Values for hello **XPath** attribute tooaccess various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="66b70-183">Toocreate por exemplo, uma variável de ambiente é "**true**" quando a instância de saudação está em execução no emulador de computação Olá, e "**false**" ao executar em nuvem Olá, use o seguinte Olá [variável] e [RoleInstanceValue] elementos:</span><span class="sxs-lookup"><span data-stu-id="66b70-183">For example, toocreate an environment variable that is "**true**" when hello instance is running in hello compute emulator, and "**false**" when running in hello cloud, use hello following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="66b70-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="66b70-184">Next steps</span></span>
<span data-ttu-id="66b70-185">Saiba como tooperform alguns [tarefas comuns de inicialização](cloud-services-startup-tasks-common.md) com seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="66b70-185">Learn how tooperform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="66b70-186">[Empacote](cloud-services-model-and-package.md) seu Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="66b70-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

[servicedefinition. Csdef]: cloud-services-model-and-package.md#csdef
[tarefa]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[inicialização]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[tempo de execução]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[ambiente]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[variável]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
