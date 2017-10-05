---
title: "Executar tarefas em contas de usuário no Lote do Azure | Microsoft Docs"
description: "Configurar contas de usuário para executar tarefas no Lote do Azure"
services: batch
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.openlocfilehash: d408c0565c0ed81fc97cc2b3976a4fc233e31302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="7013e-103">Executar tarefas em contas de usuário no Lote</span><span class="sxs-lookup"><span data-stu-id="7013e-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="7013e-104">Uma tarefa no Lote do Azure sempre é executada em uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="7013e-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="7013e-105">Por padrão, as tarefas são executadas em contas de usuário padrão, sem permissões de administrador.</span><span class="sxs-lookup"><span data-stu-id="7013e-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="7013e-106">Essas configurações da conta de usuário padrão normalmente são suficientes.</span><span class="sxs-lookup"><span data-stu-id="7013e-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="7013e-107">No entanto, para determinados cenários, é útil ser capaz de configurar a conta de usuário sob a qual você deseja executar uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="7013e-107">For certain scenarios, however, it's useful to be able to configure the user account under which you want a task to run.</span></span> <span data-ttu-id="7013e-108">Este artigo descreve os tipos de conta de usuário e como configurá-los para seu cenário.</span><span class="sxs-lookup"><span data-stu-id="7013e-108">This article discusses the types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="7013e-109">Tipos de conta de usuário</span><span class="sxs-lookup"><span data-stu-id="7013e-109">Types of user accounts</span></span>

<span data-ttu-id="7013e-110">O Lote do Azure fornece dois tipos de conta de usuário para execução de tarefas:</span><span class="sxs-lookup"><span data-stu-id="7013e-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="7013e-111">**Contas de usuário automático**</span><span class="sxs-lookup"><span data-stu-id="7013e-111">**Auto-user accounts.**</span></span> <span data-ttu-id="7013e-112">As contas de usuário automático são contas de usuário internas criadas automaticamente pelo serviço de Lote.</span><span class="sxs-lookup"><span data-stu-id="7013e-112">Auto-user accounts are built-in user accounts that are created automatically by the Batch service.</span></span> <span data-ttu-id="7013e-113">Por padrão, as tarefas são executadas em uma conta de usuário automático.</span><span class="sxs-lookup"><span data-stu-id="7013e-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="7013e-114">Você pode configurar a especificação de usuário automático para uma tarefa a fim de indicar sob qual conta de usuário automático ela deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="7013e-114">You can configure the auto-user specification for a task to indicate under which auto-user account a task should run.</span></span> <span data-ttu-id="7013e-115">A especificação de usuário automático permite que você especifique o nível de elevação e o escopo da conta de usuário automático que executará a tarefa.</span><span class="sxs-lookup"><span data-stu-id="7013e-115">The auto-user specification allows you to specify the elevation level and scope of the auto-user account that will run the task.</span></span> 

- <span data-ttu-id="7013e-116">**Uma conta de usuário nomeado**</span><span class="sxs-lookup"><span data-stu-id="7013e-116">**A named user account.**</span></span> <span data-ttu-id="7013e-117">Você pode especificar uma ou mais contas de usuário nomeado para um pool ao criar o pool.</span><span class="sxs-lookup"><span data-stu-id="7013e-117">You can specify one or more named user accounts for a pool when you create the pool.</span></span> <span data-ttu-id="7013e-118">Cada conta de usuário é criada em cada nó do pool.</span><span class="sxs-lookup"><span data-stu-id="7013e-118">Each user account is created on each node of the pool.</span></span> <span data-ttu-id="7013e-119">Além do nome de conta, você especifica a senha, o nível de elevação e, para pools do Linux, a chave privada SSH da conta do usuário.</span><span class="sxs-lookup"><span data-stu-id="7013e-119">In addition to the account name, you specify the user account password, elevation level, and, for Linux pools, the SSH private key.</span></span> <span data-ttu-id="7013e-120">Ao adicionar uma tarefa, você pode especificar a conta de usuário nomeado na qual essa tarefa deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="7013e-120">When you add a task, you can specify the named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="7013e-121">A versão 2017-01-01.4.0 do serviço de Lote introduz uma alteração significativa que exige a atualização do seu código para chamar essa versão.</span><span class="sxs-lookup"><span data-stu-id="7013e-121">The Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code to call that version.</span></span> <span data-ttu-id="7013e-122">Se você estiver migrando o código de uma versão antiga do Lote, observe que a propriedade **runElevated** não tem mais suporte na API REST ou nas bibliotecas de cliente do Lote.</span><span class="sxs-lookup"><span data-stu-id="7013e-122">If you are migrating code from an older version of Batch, note that the **runElevated** property is no longer supported in the REST API or Batch client libraries.</span></span> <span data-ttu-id="7013e-123">Use a nova propriedade **userIdentity** de uma tarefa para especificar o nível de elevação.</span><span class="sxs-lookup"><span data-stu-id="7013e-123">Use the new **userIdentity** property of a task to specify elevation level.</span></span> <span data-ttu-id="7013e-124">Veja a seção [Atualizar seu código para a biblioteca de cliente mais recente do Lote](#update-your-code-to-the-latest-batch-client-library) para obter diretrizes rápidas a fim de atualizar o código do Lote se estiver usando uma das bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="7013e-124">See the section titled [Update your code to the latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of the client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="7013e-125">As contas de usuário abordadas neste artigo não dão suporte ao RDP (Protocolo de Área de Trabalho Remota) nem ao SSH (Secure Shell) por motivos de segurança.</span><span class="sxs-lookup"><span data-stu-id="7013e-125">The user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="7013e-126">Para se conectar a um nó em execução na configuração da máquina virtual Linux via SSH, confira [Usar Área de Trabalho Remota para uma VM Linux no Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="7013e-126">To connect to a node running the Linux virtual machine configuration via SSH, see [Use Remote Desktop to a Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="7013e-127">Para se conectar a nós em execução no Windows via RDP, confira [Conectar-se a uma VM do Windows Server](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="7013e-127">To connect to nodes running Windows via RDP, see [Connect to a Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="7013e-128">Para se conectar a um nó em execução na configuração do serviço de nuvem via RDP, confira [Habilitar a Conexão de Área de Trabalho Remota para uma função nos Serviços de Nuvem do Azure](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7013e-128">To connect to a node running the cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-to-files-and-directories"></a><span data-ttu-id="7013e-129">Acesso de conta de usuário a arquivos e diretórios</span><span class="sxs-lookup"><span data-stu-id="7013e-129">User account access to files and directories</span></span>

<span data-ttu-id="7013e-130">Uma conta de usuário automático e uma conta de usuário nomeado têm acesso de leitura/gravação ao diretório de trabalho da tarefa, diretório compartilhado e diretório de tarefas de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="7013e-130">Both an auto-user account and a named user account have read/write access to the task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="7013e-131">Ambos os tipos de conta têm acesso de leitura nos diretórios de preparação de inicialização e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7013e-131">Both types of accounts have read access to the startup and job preparation directories.</span></span>

<span data-ttu-id="7013e-132">Se uma tarefa for executada na mesma conta que foi usada para executar uma tarefa de inicialização, a tarefa terá acesso de leitura/gravação ao diretório da tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="7013e-132">If a task runs under the same account that was used for running a start task, the task has read-write access to the start task directory.</span></span> <span data-ttu-id="7013e-133">Da mesma forma, se uma tarefa for executada na mesma conta que foi usada para executar uma tarefa de preparação de trabalho, a tarefa terá acesso de leitura/gravação ao diretório de tarefa de preparação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7013e-133">Similarly, if a task runs under the same account that was used for running a job preparation task, the task has read-write access to the job preparation task directory.</span></span> <span data-ttu-id="7013e-134">Se uma tarefa for executada em uma conta diferente da tarefa de inicialização ou da tarefa de preparação de trabalho, a tarefa terá acesso somente leitura ao respectivo diretório.</span><span class="sxs-lookup"><span data-stu-id="7013e-134">If a task runs under a different account than the start task or job preparation task, then the task has only read access to the respective directory.</span></span>

<span data-ttu-id="7013e-135">Para saber mais sobre como acessar arquivos e diretórios de uma tarefa, confira [Desenvolver soluções de computação paralela em larga escala com o Lote](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="7013e-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="7013e-136">Acesso elevado para tarefas</span><span class="sxs-lookup"><span data-stu-id="7013e-136">Elevated access for tasks</span></span> 

<span data-ttu-id="7013e-137">O nível de elevação da conta de usuário indica se uma tarefa é executada com acesso elevado.</span><span class="sxs-lookup"><span data-stu-id="7013e-137">The user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="7013e-138">Tanto uma conta de usuário automático, quanto uma conta de usuário nomeado podem ser executadas com acesso elevado.</span><span class="sxs-lookup"><span data-stu-id="7013e-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="7013e-139">As duas opções de nível de elevação são:</span><span class="sxs-lookup"><span data-stu-id="7013e-139">The two options for elevation level are:</span></span>

- <span data-ttu-id="7013e-140">**Não Administrador:** a tarefa é executada como um usuário padrão sem acesso elevado.</span><span class="sxs-lookup"><span data-stu-id="7013e-140">**NonAdmin:** The task runs as a standard user without elevated access.</span></span> <span data-ttu-id="7013e-141">O nível de elevação padrão de uma conta de usuário do Lote é sempre **Não Administrador**.</span><span class="sxs-lookup"><span data-stu-id="7013e-141">The default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="7013e-142">**Administrador:** a tarefa é executada como um usuário com acesso elevado e opera com permissões completas de Administrador.</span><span class="sxs-lookup"><span data-stu-id="7013e-142">**Admin:** The task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="7013e-143">Contas de usuário automático</span><span class="sxs-lookup"><span data-stu-id="7013e-143">Auto-user accounts</span></span>

<span data-ttu-id="7013e-144">Por padrão, as tarefas são executadas no Lote em uma conta de usuário automático, como um usuário padrão sem acesso elevado e com escopo de tarefa.</span><span class="sxs-lookup"><span data-stu-id="7013e-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="7013e-145">Quando a especificação de usuário automático é configurada para o escopo de tarefa, o serviço de Lote cria uma conta de usuário automático apenas para essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="7013e-145">When the auto-user specification is configured for task scope, the Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="7013e-146">A alternativa ao escopo de tarefa é o escopo de pool.</span><span class="sxs-lookup"><span data-stu-id="7013e-146">The alternative to task scope is pool scope.</span></span> <span data-ttu-id="7013e-147">Quando a especificação de usuário automático para uma tarefa é configurada para o escopo de pool, a tarefa é executada em uma conta de usuário automático que está disponível para qualquer tarefa no pool.</span><span class="sxs-lookup"><span data-stu-id="7013e-147">When the auto-user specification for a task is configured for pool scope, the task runs under an auto-user account that is available to any task in the pool.</span></span> <span data-ttu-id="7013e-148">Para saber mais sobre escopo de pool, confira a seção [Executar uma tarefa como o usuário automático com escopo de pool](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="7013e-148">For more information about pool scope, see the section titled [Run a task as the auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="7013e-149">O escopo padrão é diferente em nós do Windows e Linux:</span><span class="sxs-lookup"><span data-stu-id="7013e-149">The default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="7013e-150">Em nós do Windows, as tarefas são executadas no escopo de tarefa por padrão.</span><span class="sxs-lookup"><span data-stu-id="7013e-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="7013e-151">Nós do Linux sempre são executados no escopo de pool.</span><span class="sxs-lookup"><span data-stu-id="7013e-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="7013e-152">Há quatro configurações possíveis para a especificação de usuário automático, e cada uma delas corresponde a uma conta de usuário automático exclusiva:</span><span class="sxs-lookup"><span data-stu-id="7013e-152">There are four possible configurations for the auto-user specification, each of which corresponds to a unique auto-user account:</span></span>

- <span data-ttu-id="7013e-153">Acesso de não administrador com escopo de tarefa (a especificação padrão de usuário automático)</span><span class="sxs-lookup"><span data-stu-id="7013e-153">Non-admin access with task scope (the default auto-user specification)</span></span>
- <span data-ttu-id="7013e-154">Acesso de administrador (elevado) com escopo de tarefa</span><span class="sxs-lookup"><span data-stu-id="7013e-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="7013e-155">Acesso de não administrador com escopo de pool</span><span class="sxs-lookup"><span data-stu-id="7013e-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="7013e-156">Acesso de administrador com escopo de pool</span><span class="sxs-lookup"><span data-stu-id="7013e-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="7013e-157">As tarefas em execução no escopo de tarefa não têm de fato acesso a outras tarefas em um nó.</span><span class="sxs-lookup"><span data-stu-id="7013e-157">Tasks running under task scope do not have de facto access to other tasks on a node.</span></span> <span data-ttu-id="7013e-158">No entanto, um usuário mal-intencionado com acesso à conta pode contornar essa restrição enviando uma tarefa que é executada com privilégios de administrador e acessa outros diretórios de tarefa.</span><span class="sxs-lookup"><span data-stu-id="7013e-158">However, a malicious user with access to the account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="7013e-159">Um usuário mal-intencionado também pode usar um RDP ou SSH para se conectar a um nó.</span><span class="sxs-lookup"><span data-stu-id="7013e-159">A malicious user could also use RDP or SSH to connect to a node.</span></span> <span data-ttu-id="7013e-160">É importante proteger o acesso às chaves da sua conta do Lote para evitar uma situação como essa.</span><span class="sxs-lookup"><span data-stu-id="7013e-160">It's important to protect access to your Batch account keys to prevent such a scenario.</span></span> <span data-ttu-id="7013e-161">Se você suspeitar de que sua conta pode ter sido comprometida, certifique-se de regenerar as chaves.</span><span class="sxs-lookup"><span data-stu-id="7013e-161">If you suspect your account may have been compromised, be sure to regenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="7013e-162">Executar uma tarefa como um usuário automático com acesso elevado</span><span class="sxs-lookup"><span data-stu-id="7013e-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="7013e-163">Você pode configurar a especificação de usuário automático para privilégios de administrador quando precisar executar uma tarefa com acesso elevado.</span><span class="sxs-lookup"><span data-stu-id="7013e-163">You can configure the auto-user specification for administrator privileges when you need to run a task with elevated access.</span></span> <span data-ttu-id="7013e-164">Por exemplo, uma tarefa de inicialização pode precisar de acesso elevado para instalar software no nó.</span><span class="sxs-lookup"><span data-stu-id="7013e-164">For example, a start task may need elevated access to install software on the node.</span></span>

> [!NOTE] 
> <span data-ttu-id="7013e-165">De modo geral, é melhor usar acesso elevado somente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="7013e-165">In general, it's best to use elevated access only when necessary.</span></span> <span data-ttu-id="7013e-166">A prática recomendada é conceder o privilégio mínimo necessário para obter o resultado desejado.</span><span class="sxs-lookup"><span data-stu-id="7013e-166">Best practices recommend granting the minimum privilege necessary to achieve the desired outcome.</span></span> <span data-ttu-id="7013e-167">Por exemplo, se uma tarefa de inicialização instala o software para o usuário atual, e não para todos os usuários, você poderá evitar conceder acesso elevado para tarefas.</span><span class="sxs-lookup"><span data-stu-id="7013e-167">For example, if a start task installs software for the current user, instead of for all users, you may be able to avoid granting elevated access to tasks.</span></span> <span data-ttu-id="7013e-168">É possível configurar a especificação de usuário automático para escopo de pool e acesso de não administrador para todas as tarefas que precisam ser executadas na mesma conta, incluindo a tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="7013e-168">You can configure the auto-user specification for pool scope and non-admin access for all tasks that need to run under the same account, including the start task.</span></span> 
>
>

<span data-ttu-id="7013e-169">Os trechos de código a seguir mostram como configurar a especificação de usuário automático.</span><span class="sxs-lookup"><span data-stu-id="7013e-169">The following code snippets show how to configure the auto-user specification.</span></span> <span data-ttu-id="7013e-170">Os exemplos definem o nível de elevação para `Admin` e o escopo para `Task`.</span><span class="sxs-lookup"><span data-stu-id="7013e-170">The examples set the elevation level to `Admin` and the scope to `Task`.</span></span> <span data-ttu-id="7013e-171">O escopo de tarefa é a configuração padrão, mas está incluído aqui em virtude do exemplo.</span><span class="sxs-lookup"><span data-stu-id="7013e-171">Task scope is the default setting, but is included here for the sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="7013e-172">.NET no Lote</span><span class="sxs-lookup"><span data-stu-id="7013e-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="7013e-173">Java no Lote</span><span class="sxs-lookup"><span data-stu-id="7013e-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="7013e-174">Python no Lote</span><span class="sxs-lookup"><span data-stu-id="7013e-174">Batch Python</span></span>

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="7013e-175">Executar uma tarefa como um usuário automático com escopo de pool</span><span class="sxs-lookup"><span data-stu-id="7013e-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="7013e-176">Quando um nó é provisionado, duas contas de usuário automático em todo o pool são criadas em cada nó do pool, uma com acesso elevado e outra sem.</span><span class="sxs-lookup"><span data-stu-id="7013e-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in the pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="7013e-177">Configurar o escopo do usuário automático para o escopo de pool em uma determinada tarefa executa a tarefa em uma dessas duas contas de usuário automático em todo o pool.</span><span class="sxs-lookup"><span data-stu-id="7013e-177">Setting the auto-user's scope to pool scope for a given task runs the task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="7013e-178">Quando você especifica o escopo de pool para o usuário automático, todas as tarefas que são executadas com acesso de administrador o são na mesma conta de usuário automático em todo o pool.</span><span class="sxs-lookup"><span data-stu-id="7013e-178">When you specify pool scope for the auto-user, all tasks that run with administrator access run under the same pool-wide auto-user account.</span></span> <span data-ttu-id="7013e-179">Da mesma forma, as tarefas executadas sem permissões de administrador também o são em uma única conta de usuário automático em todo o pool.</span><span class="sxs-lookup"><span data-stu-id="7013e-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="7013e-180">As duas contas de usuário automático em todo o pool são distintas.</span><span class="sxs-lookup"><span data-stu-id="7013e-180">The two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="7013e-181">As tarefas executadas na conta administrativa em todo o pool não podem compartilhar dados com tarefas em execução na conta padrão, e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="7013e-181">Tasks running under the pool-wide administrative account cannot share data with tasks running under the standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="7013e-182">A vantagem da execução na mesma conta de usuário automático é que as tarefas podem compartilhar dados com outras tarefas em execução no mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="7013e-182">The advantage to running under the same auto-user account is that tasks are able to share data with other tasks running on the same node.</span></span>

<span data-ttu-id="7013e-183">O compartilhamento de segredos entre tarefas é um cenário em que a execução de tarefas em um das duas contas de usuário automático em todo o pool é útil.</span><span class="sxs-lookup"><span data-stu-id="7013e-183">Sharing secrets between tasks is one scenario where running tasks under one of the two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="7013e-184">Por exemplo, suponha que a tarefa de inicialização precise provisionar um segredo no nó que outras tarefas podem usar.</span><span class="sxs-lookup"><span data-stu-id="7013e-184">For example, suppose a start task needs to provision a secret onto the node that other tasks can use.</span></span> <span data-ttu-id="7013e-185">Você pode usar o DPAPI (API da Proteção de Dados) do Windows, mas ele exige privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="7013e-185">You could use the Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="7013e-186">Em vez disso, é possível proteger o segredo no nível de usuário.</span><span class="sxs-lookup"><span data-stu-id="7013e-186">Instead, you can protect the secret at the user level.</span></span> <span data-ttu-id="7013e-187">As tarefas em execução na mesma conta de usuário podem acessar o segredo sem acesso elevado.</span><span class="sxs-lookup"><span data-stu-id="7013e-187">Tasks running under the same user account can access the secret without elevated access.</span></span>

<span data-ttu-id="7013e-188">Outro cenário em que talvez seja conveniente executar tarefas em uma conta de usuário automático com escopo de pool é em um compartilhamento de arquivos MPI (Interface de Transmissão de Mensagens).</span><span class="sxs-lookup"><span data-stu-id="7013e-188">Another scenario where you may want to run tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="7013e-189">Um compartilhamento de arquivos MPI é útil quando os nós da tarefa MPI precisam trabalhar nos mesmos dados de arquivo.</span><span class="sxs-lookup"><span data-stu-id="7013e-189">An MPI file share is useful when the nodes in the MPI task need to work on the same file data.</span></span> <span data-ttu-id="7013e-190">O nó de cabeçalho cria um compartilhamento de arquivos que os nós filho podem acessar se estiverem sendo executados na mesma conta de usuário automático.</span><span class="sxs-lookup"><span data-stu-id="7013e-190">The head node creates a file share that the child nodes can access if they are running under the same auto-user account.</span></span> 

<span data-ttu-id="7013e-191">O trecho de código a seguir define o escopo do usuário automático para escopo de pool em uma tarefa do .NET no Lote.</span><span class="sxs-lookup"><span data-stu-id="7013e-191">The following code snippet sets the auto-user's scope to pool scope for a task in Batch .NET.</span></span> <span data-ttu-id="7013e-192">O nível de elevação é omitido, de modo que a tarefa é executada na conta de usuário automático em todo o pool padrão.</span><span class="sxs-lookup"><span data-stu-id="7013e-192">The elevation level is omitted, so the task runs under the standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="7013e-193">Contas de usuário nomeado</span><span class="sxs-lookup"><span data-stu-id="7013e-193">Named user accounts</span></span>

<span data-ttu-id="7013e-194">Você pode definir contas de usuário nomeado ao criar um pool.</span><span class="sxs-lookup"><span data-stu-id="7013e-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="7013e-195">Uma conta de usuário nomeado tem um nome e uma senha fornecidos por você.</span><span class="sxs-lookup"><span data-stu-id="7013e-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="7013e-196">É possível especificar o nível de elevação para uma conta de usuário nomeado.</span><span class="sxs-lookup"><span data-stu-id="7013e-196">You can specify the elevation level for a named user account.</span></span> <span data-ttu-id="7013e-197">Para nós Linux, você também pode fornecer uma chave privada SSH.</span><span class="sxs-lookup"><span data-stu-id="7013e-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="7013e-198">Uma conta de usuário nomeado existe em todos os nós no pool e está disponível para todas as tarefas em execução nesses nós.</span><span class="sxs-lookup"><span data-stu-id="7013e-198">A named user account exists on all nodes in the pool and is available to all tasks running on those nodes.</span></span> <span data-ttu-id="7013e-199">É possível definir qualquer número de usuários nomeados para um pool.</span><span class="sxs-lookup"><span data-stu-id="7013e-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="7013e-200">Ao adicionar uma tarefa ou um conjunto de tarefas, você pode especificar que a tarefa será executada em uma das contas de usuário nomeado definidas no pool.</span><span class="sxs-lookup"><span data-stu-id="7013e-200">When you add a task or task collection, you can specify that the task runs under one of the named user accounts defined on the pool.</span></span>

<span data-ttu-id="7013e-201">Uma conta de usuário nomeado é útil quando você deseja executar todas as tarefas em um trabalho na mesma conta de usuário, mas isolá-las de tarefas em execução em outros trabalhos ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="7013e-201">A named user account is useful when you want to run all tasks in a job under the same user account, but isolate them from tasks running in other jobs at the same time.</span></span> <span data-ttu-id="7013e-202">Por exemplo, é possível criar um usuário nomeado para cada trabalho e executar as tarefas de cada trabalho nessa conta de usuário nomeado.</span><span class="sxs-lookup"><span data-stu-id="7013e-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="7013e-203">Cada trabalho pode compartilhar um segredo com suas próprias tarefas, mas não com tarefas em execução em outros trabalhos.</span><span class="sxs-lookup"><span data-stu-id="7013e-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="7013e-204">Você também pode usar uma conta de usuário nomeado para executar uma tarefa que defina permissões em recursos externos, como compartilhamentos de arquivos.</span><span class="sxs-lookup"><span data-stu-id="7013e-204">You can also use a named user account to run a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="7013e-205">Com uma conta de usuário nomeado, você controla a identidade do usuário e pode usar a identidade do usuário para definir permissões.</span><span class="sxs-lookup"><span data-stu-id="7013e-205">With a named user account, you control the user identity and can use that user identity to set permissions.</span></span>  

<span data-ttu-id="7013e-206">As contas de usuário nomeado permitem o SSH sem senha entre os nós Linux.</span><span class="sxs-lookup"><span data-stu-id="7013e-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="7013e-207">É possível usar uma conta de usuário nomeado com nós Linux que precisam executar tarefas de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="7013e-207">You can use a named user account with Linux nodes that need to run multi-instance tasks.</span></span> <span data-ttu-id="7013e-208">Cada nó no pool pode executar tarefas em uma conta de usuário definida no pool inteiro.</span><span class="sxs-lookup"><span data-stu-id="7013e-208">Each node in the pool can run tasks under a user account defined on the whole pool.</span></span> <span data-ttu-id="7013e-209">Para saber mais sobre tarefas de várias instâncias, confira [Usar tarefas de várias instâncias para executar aplicativos de MPI](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="7013e-209">For more information about multi-instance tasks, see [Use multi\-instance tasks to run MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="7013e-210">Criar contas de usuário nomeado</span><span class="sxs-lookup"><span data-stu-id="7013e-210">Create named user accounts</span></span>

<span data-ttu-id="7013e-211">Para criar contas de usuário nomeado no Lote, adicione um conjunto de contas de usuário no pool.</span><span class="sxs-lookup"><span data-stu-id="7013e-211">To create named user accounts in Batch, add a collection of user accounts to the pool.</span></span> <span data-ttu-id="7013e-212">Os trechos de código a seguir mostram como criar contas de usuário nomeado em .NET, Java e Python.</span><span class="sxs-lookup"><span data-stu-id="7013e-212">The following code snippets show how to create named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="7013e-213">Esses trechos de código mostram como criar contas nomeadas de administrador e não administrador em um pool.</span><span class="sxs-lookup"><span data-stu-id="7013e-213">These code snippets show how to create both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="7013e-214">Os exemplos criam pools usando a configuração de serviço de nuvem, mas você usa a mesma abordagem na criação de um pool do Windows ou Linux usando a configuração da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7013e-214">The examples create pools using the cloud service configuration, but you use the same approach when creating a Windows or Linux pool using the virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="7013e-215">Exemplo de .NET do Lote (Windows)</span><span class="sxs-lookup"><span data-stu-id="7013e-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using the cloud service configuration.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount("adminUser", "xyz123", ElevationLevel.Admin),
    new UserAccount("nonAdminUser", "123xyz", ElevationLevel.NonAdmin),
};

// Commit the pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="7013e-216">Exemplo de .NET do Lote (Linux)</span><span class="sxs-lookup"><span data-stu-id="7013e-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the virtual machine configuration to use to create the pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create the unbound pool.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                             
    virtualMachineSize: "Standard_A1",                                      
    virtualMachineConfiguration: virtualMachineConfiguration);                  

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(
        name: "adminUser",
        password: "xyz123",
        elevationLevel: ElevationLevel.Admin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 12345,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
    new UserAccount(
        name: "nonAdminUser",
        password: "123xyz",
        elevationLevel: ElevationLevel.NonAdmin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 45678,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
};

// Commit the pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="7013e-217">Exemplo de Java no Lote</span><span class="sxs-lookup"><span data-stu-id="7013e-217">Batch Java example</span></span>

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a><span data-ttu-id="7013e-218">Exemplo de Python no Lote</span><span class="sxs-lookup"><span data-stu-id="7013e-218">Batch Python example</span></span>

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="7013e-219">Executar uma tarefa em uma conta de usuário nomeado com acesso elevado</span><span class="sxs-lookup"><span data-stu-id="7013e-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="7013e-220">Para executar uma tarefa como um usuário com acesso elevado, defina a propriedade **UserIdentity** da tarefa como uma conta de usuário nomeado que foi criada com sua propriedade **ElevationLevel** definida como `Admin`.</span><span class="sxs-lookup"><span data-stu-id="7013e-220">To run a task as an elevated user, set the task's **UserIdentity** property to a named user account that was created with its **ElevationLevel** property set to `Admin`.</span></span>

<span data-ttu-id="7013e-221">Este trecho de código especifica que a tarefa deve ser executada em uma conta de usuário nomeado.</span><span class="sxs-lookup"><span data-stu-id="7013e-221">This code snippet specifies that the task should run under a named user account.</span></span> <span data-ttu-id="7013e-222">Essa conta de usuário nomeado foi definida no pool quando este foi criado.</span><span class="sxs-lookup"><span data-stu-id="7013e-222">This named user account was defined on the pool when the pool was created.</span></span> <span data-ttu-id="7013e-223">Nesse caso, a conta de usuário nomeado foi criada com permissões de administrador:</span><span class="sxs-lookup"><span data-stu-id="7013e-223">In this case, the named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-to-the-latest-batch-client-library"></a><span data-ttu-id="7013e-224">Atualizar seu código para a biblioteca de cliente mais recente do Lote</span><span class="sxs-lookup"><span data-stu-id="7013e-224">Update your code to the latest Batch client library</span></span>

<span data-ttu-id="7013e-225">A versão 2017-01-01.4.0 do serviço de Lote introduz uma alteração significativa, substituindo a propriedade **runElevated** disponível em versões anteriores pela propriedade **userIdentity**.</span><span class="sxs-lookup"><span data-stu-id="7013e-225">The Batch service version 2017-01-01.4.0 introduces a breaking change, replacing the **runElevated** property available in earlier versions with the **userIdentity** property.</span></span> <span data-ttu-id="7013e-226">As tabelas a seguir fornecem um mapeamento simples que você pode usar para atualizar o código de versões anteriores das bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="7013e-226">The following tables provide a simple mapping that you can use to update your code from earlier versions of the client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="7013e-227">.NET no Lote</span><span class="sxs-lookup"><span data-stu-id="7013e-227">Batch .NET</span></span>

| <span data-ttu-id="7013e-228">Se seu código usar...</span><span class="sxs-lookup"><span data-stu-id="7013e-228">If your code uses...</span></span>                  | <span data-ttu-id="7013e-229">Atualize-o para...</span><span class="sxs-lookup"><span data-stu-id="7013e-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="7013e-230">`CloudTask.RunElevated` não especificado</span><span class="sxs-lookup"><span data-stu-id="7013e-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="7013e-231">Nenhuma atualização é necessária</span><span class="sxs-lookup"><span data-stu-id="7013e-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="7013e-232">Java no Lote</span><span class="sxs-lookup"><span data-stu-id="7013e-232">Batch Java</span></span>

| <span data-ttu-id="7013e-233">Se seu código usar...</span><span class="sxs-lookup"><span data-stu-id="7013e-233">If your code uses...</span></span>                      | <span data-ttu-id="7013e-234">Atualize-o para...</span><span class="sxs-lookup"><span data-stu-id="7013e-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="7013e-235">`CloudTask.withRunElevated` não especificado</span><span class="sxs-lookup"><span data-stu-id="7013e-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="7013e-236">Nenhuma atualização é necessária</span><span class="sxs-lookup"><span data-stu-id="7013e-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="7013e-237">Python no Lote</span><span class="sxs-lookup"><span data-stu-id="7013e-237">Batch Python</span></span>

| <span data-ttu-id="7013e-238">Se seu código usar...</span><span class="sxs-lookup"><span data-stu-id="7013e-238">If your code uses...</span></span>                      | <span data-ttu-id="7013e-239">Atualize-o para...</span><span class="sxs-lookup"><span data-stu-id="7013e-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="7013e-240">`user_identity=user`, em que</span><span class="sxs-lookup"><span data-stu-id="7013e-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="7013e-241">`user_identity=user`, em que</span><span class="sxs-lookup"><span data-stu-id="7013e-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="7013e-242">`run_elevated` não especificado</span><span class="sxs-lookup"><span data-stu-id="7013e-242">`run_elevated` not specified</span></span> | <span data-ttu-id="7013e-243">Nenhuma atualização é necessária</span><span class="sxs-lookup"><span data-stu-id="7013e-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="7013e-244">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7013e-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="7013e-245">Fórum do Lote</span><span class="sxs-lookup"><span data-stu-id="7013e-245">Batch Forum</span></span>

<span data-ttu-id="7013e-246">O [Fórum do Lote do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) no MSDN é um ótimo lugar para discutir sobre o Lote e fazer perguntas sobre o serviço.</span><span class="sxs-lookup"><span data-stu-id="7013e-246">The [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="7013e-247">Acesse diretamente as postagens úteis fixadas e poste suas dúvidas conforme elas surgirem enquanto você cria suas soluções do Lote.</span><span class="sxs-lookup"><span data-stu-id="7013e-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>