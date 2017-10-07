---
title: "aaaRun tarefas em contas de usuário em lote do Azure | Microsoft Docs"
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
ms.openlocfilehash: 13d7d76451d89a3cca090c4ef24ed0ed781bbf09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="7096e-103">Executar tarefas em contas de usuário no Lote</span><span class="sxs-lookup"><span data-stu-id="7096e-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="7096e-104">Uma tarefa no Lote do Azure sempre é executada em uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="7096e-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="7096e-105">Por padrão, as tarefas são executadas em contas de usuário padrão, sem permissões de administrador.</span><span class="sxs-lookup"><span data-stu-id="7096e-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="7096e-106">Essas configurações da conta de usuário padrão normalmente são suficientes.</span><span class="sxs-lookup"><span data-stu-id="7096e-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="7096e-107">Para determinados cenários, no entanto, é útil toobe tooconfigure capaz de saudação usuário conta sob a qual você deseja toorun uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="7096e-107">For certain scenarios, however, it's useful toobe able tooconfigure hello user account under which you want a task toorun.</span></span> <span data-ttu-id="7096e-108">Este artigo aborda os tipos de saudação de contas de usuário e como configurá-los para seu cenário.</span><span class="sxs-lookup"><span data-stu-id="7096e-108">This article discusses hello types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="7096e-109">Tipos de conta de usuário</span><span class="sxs-lookup"><span data-stu-id="7096e-109">Types of user accounts</span></span>

<span data-ttu-id="7096e-110">O Lote do Azure fornece dois tipos de conta de usuário para execução de tarefas:</span><span class="sxs-lookup"><span data-stu-id="7096e-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="7096e-111">**Contas de usuário automático**</span><span class="sxs-lookup"><span data-stu-id="7096e-111">**Auto-user accounts.**</span></span> <span data-ttu-id="7096e-112">Contas de usuário automático são contas de usuário internas que são criadas automaticamente pelo serviço de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="7096e-112">Auto-user accounts are built-in user accounts that are created automatically by hello Batch service.</span></span> <span data-ttu-id="7096e-113">Por padrão, as tarefas são executadas em uma conta de usuário automático.</span><span class="sxs-lookup"><span data-stu-id="7096e-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="7096e-114">Você pode configurar a especificação de saudação do usuário de automática para um tooindicate de tarefa em qual usuário automaticamente uma tarefa de conta deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="7096e-114">You can configure hello auto-user specification for a task tooindicate under which auto-user account a task should run.</span></span> <span data-ttu-id="7096e-115">especificação de saudação do usuário de automática permite que você toospecify nível de elevação de saudação e escopo Olá autoda conta de usuário que executará a tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="7096e-115">hello auto-user specification allows you toospecify hello elevation level and scope of hello auto-user account that will run hello task.</span></span> 

- <span data-ttu-id="7096e-116">**Uma conta de usuário nomeado**</span><span class="sxs-lookup"><span data-stu-id="7096e-116">**A named user account.**</span></span> <span data-ttu-id="7096e-117">Você pode especificar uma ou mais contas de usuário nomeado para um pool de quando você cria o pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="7096e-117">You can specify one or more named user accounts for a pool when you create hello pool.</span></span> <span data-ttu-id="7096e-118">Cada conta de usuário é criada em cada nó do pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="7096e-118">Each user account is created on each node of hello pool.</span></span> <span data-ttu-id="7096e-119">Além disso toohello o nome da conta, especifique a senha de conta de usuário hello, elevação nível e, para pools do Linux, a chave privada SSH hello.</span><span class="sxs-lookup"><span data-stu-id="7096e-119">In addition toohello account name, you specify hello user account password, elevation level, and, for Linux pools, hello SSH private key.</span></span> <span data-ttu-id="7096e-120">Quando você adiciona uma tarefa, você pode especificar Olá denominado conta de usuário sob a qual essa tarefa deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="7096e-120">When you add a task, you can specify hello named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="7096e-121">versão de serviço de lote Olá 2017-01-01.4.0 apresenta uma alteração significativa requer que você atualize seu código toocall dessa versão.</span><span class="sxs-lookup"><span data-stu-id="7096e-121">hello Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code toocall that version.</span></span> <span data-ttu-id="7096e-122">Se você estiver migrando o código de uma versão mais antiga do lote, observe que Olá **runElevated** propriedade não é mais suportada em bibliotecas de cliente de API REST ou lote hello.</span><span class="sxs-lookup"><span data-stu-id="7096e-122">If you are migrating code from an older version of Batch, note that hello **runElevated** property is no longer supported in hello REST API or Batch client libraries.</span></span> <span data-ttu-id="7096e-123">Saudação de uso novo **userIdentity** propriedade de um nível de elevação de toospecify de tarefa.</span><span class="sxs-lookup"><span data-stu-id="7096e-123">Use hello new **userIdentity** property of a task toospecify elevation level.</span></span> <span data-ttu-id="7096e-124">Consulte a seção de saudação [atualizar sua biblioteca de cliente de lote mais recente do código toohello](#update-your-code-to-the-latest-batch-client-library) para rápido diretrizes para atualizar seu código de lote, se você estiver usando uma das bibliotecas de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="7096e-124">See hello section titled [Update your code toohello latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of hello client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="7096e-125">contas de usuário Olá discutidas neste artigo não dão suporte a protocolo de área de trabalho remota (RDP) ou Secure Shell (SSH), por motivos de segurança.</span><span class="sxs-lookup"><span data-stu-id="7096e-125">hello user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="7096e-126">tooconnect tooa nó em execução Olá Linux configuração da máquina virtual via SSH, consulte [tooa de área de trabalho remota Use VM do Linux no Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="7096e-126">tooconnect tooa node running hello Linux virtual machine configuration via SSH, see [Use Remote Desktop tooa Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="7096e-127">toonodes tooconnect que executam o Windows por meio do protocolo RDP, consulte [conectar tooa VM do Windows Server](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="7096e-127">tooconnect toonodes running Windows via RDP, see [Connect tooa Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="7096e-128">tooconnect tooa nó em execução Olá serviço configuração de nuvem por meio do protocolo RDP, consulte [habilitar Conexão de área de trabalho remota para uma função nos serviços de nuvem do Azure](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7096e-128">tooconnect tooa node running hello cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-toofiles-and-directories"></a><span data-ttu-id="7096e-129">Diretórios e toofiles de acesso de conta de usuário</span><span class="sxs-lookup"><span data-stu-id="7096e-129">User account access toofiles and directories</span></span>

<span data-ttu-id="7096e-130">Uma conta de usuário automático e uma conta de usuário nomeado tem o diretório de trabalho da tarefa de toohello do acesso de leitura/gravação, o diretório compartilhado e o diretório de tarefas de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="7096e-130">Both an auto-user account and a named user account have read/write access toohello task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="7096e-131">Os dois tipos de contas tem os diretórios preparação do acesso de leitura toohello inicialização e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7096e-131">Both types of accounts have read access toohello startup and job preparation directories.</span></span>

<span data-ttu-id="7096e-132">Se uma tarefa é executada em Olá mesma conta que foi usada para executar uma tarefa de início, a tarefa de saudação tem o diretório de início de tarefas de toohello de acesso de leitura-gravação.</span><span class="sxs-lookup"><span data-stu-id="7096e-132">If a task runs under hello same account that was used for running a start task, hello task has read-write access toohello start task directory.</span></span> <span data-ttu-id="7096e-133">Olá mesmo da mesma forma, se uma tarefa é executada na conta que foi usada para executar uma tarefa de preparação de trabalho, a tarefa de saudação tem diretório tarefas de preparação de trabalho do acesso de leitura-gravação toohello.</span><span class="sxs-lookup"><span data-stu-id="7096e-133">Similarly, if a task runs under hello same account that was used for running a job preparation task, hello task has read-write access toohello job preparation task directory.</span></span> <span data-ttu-id="7096e-134">Se uma tarefa é executada em uma conta diferente de tarefa do saudação inicial ou tarefa de preparação de trabalho, tarefa Olá tem somente acesso de leitura toohello respectiva pasta.</span><span class="sxs-lookup"><span data-stu-id="7096e-134">If a task runs under a different account than hello start task or job preparation task, then hello task has only read access toohello respective directory.</span></span>

<span data-ttu-id="7096e-135">Para saber mais sobre como acessar arquivos e diretórios de uma tarefa, confira [Desenvolver soluções de computação paralela em larga escala com o Lote](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="7096e-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="7096e-136">Acesso elevado para tarefas</span><span class="sxs-lookup"><span data-stu-id="7096e-136">Elevated access for tasks</span></span> 

<span data-ttu-id="7096e-137">nível de privilégio da conta do usuário Olá indica se uma tarefa é executado com acesso com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="7096e-137">hello user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="7096e-138">Tanto uma conta de usuário automático, quanto uma conta de usuário nomeado podem ser executadas com acesso elevado.</span><span class="sxs-lookup"><span data-stu-id="7096e-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="7096e-139">Olá duas opções para o nível de elevação são:</span><span class="sxs-lookup"><span data-stu-id="7096e-139">hello two options for elevation level are:</span></span>

- <span data-ttu-id="7096e-140">**NonAdmin:** tarefa Olá é executado como um usuário padrão sem acesso com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="7096e-140">**NonAdmin:** hello task runs as a standard user without elevated access.</span></span> <span data-ttu-id="7096e-141">nível de elevação saudação padrão para uma conta de usuário do lote é sempre **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="7096e-141">hello default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="7096e-142">**Administração:** tarefa Olá é executado como um usuário com acesso com privilégios elevados e opera com permissões de administrador completas.</span><span class="sxs-lookup"><span data-stu-id="7096e-142">**Admin:** hello task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="7096e-143">Contas de usuário automático</span><span class="sxs-lookup"><span data-stu-id="7096e-143">Auto-user accounts</span></span>

<span data-ttu-id="7096e-144">Por padrão, as tarefas são executadas no Lote em uma conta de usuário automático, como um usuário padrão sem acesso elevado e com escopo de tarefa.</span><span class="sxs-lookup"><span data-stu-id="7096e-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="7096e-145">Quando a especificação de usuário automático Olá estiver configurada para o escopo da tarefa, o serviço de lote de saudação cria uma conta de usuário automaticamente para essa tarefa somente.</span><span class="sxs-lookup"><span data-stu-id="7096e-145">When hello auto-user specification is configured for task scope, hello Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="7096e-146">escopo de tootask alternativo de saudação é o escopo de pool.</span><span class="sxs-lookup"><span data-stu-id="7096e-146">hello alternative tootask scope is pool scope.</span></span> <span data-ttu-id="7096e-147">Quando a especificação de saudação do usuário de automática para uma tarefa está configurada para o escopo de pool, tarefa Olá é executado sob uma conta de usuário automático é tarefa tooany disponível no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="7096e-147">When hello auto-user specification for a task is configured for pool scope, hello task runs under an auto-user account that is available tooany task in hello pool.</span></span> <span data-ttu-id="7096e-148">Para obter mais informações sobre o escopo do pool, consulte a seção de saudação [executar uma tarefa como Olá automático de usuário com escopo de pool](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="7096e-148">For more information about pool scope, see hello section titled [Run a task as hello auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="7096e-149">escopo padrão de saudação é diferente em nós do Windows e Linux:</span><span class="sxs-lookup"><span data-stu-id="7096e-149">hello default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="7096e-150">Em nós do Windows, as tarefas são executadas no escopo de tarefa por padrão.</span><span class="sxs-lookup"><span data-stu-id="7096e-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="7096e-151">Nós do Linux sempre são executados no escopo de pool.</span><span class="sxs-lookup"><span data-stu-id="7096e-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="7096e-152">Há quatro configurações possíveis para especificação de usuário automático hello, cada uma correspondendo tooa única autoconta de usuário:</span><span class="sxs-lookup"><span data-stu-id="7096e-152">There are four possible configurations for hello auto-user specification, each of which corresponds tooa unique auto-user account:</span></span>

- <span data-ttu-id="7096e-153">Acesso de não-administrador com escopo de tarefa (especificação de usuário automático padrão Olá)</span><span class="sxs-lookup"><span data-stu-id="7096e-153">Non-admin access with task scope (hello default auto-user specification)</span></span>
- <span data-ttu-id="7096e-154">Acesso de administrador (elevado) com escopo de tarefa</span><span class="sxs-lookup"><span data-stu-id="7096e-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="7096e-155">Acesso de não administrador com escopo de pool</span><span class="sxs-lookup"><span data-stu-id="7096e-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="7096e-156">Acesso de administrador com escopo de pool</span><span class="sxs-lookup"><span data-stu-id="7096e-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="7096e-157">Tarefas em execução no escopo da tarefa não tem acesso tooother tarefas de fato em um nó.</span><span class="sxs-lookup"><span data-stu-id="7096e-157">Tasks running under task scope do not have de facto access tooother tasks on a node.</span></span> <span data-ttu-id="7096e-158">No entanto, um usuário malintencionado com a conta de acesso de toohello pode contornar essa restrição enviando uma tarefa que é executado com privilégios de administrador e acessa outros diretórios de tarefa.</span><span class="sxs-lookup"><span data-stu-id="7096e-158">However, a malicious user with access toohello account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="7096e-159">Um usuário mal-intencionado também pode usar o nó de tooa tooconnect RDP ou SSH.</span><span class="sxs-lookup"><span data-stu-id="7096e-159">A malicious user could also use RDP or SSH tooconnect tooa node.</span></span> <span data-ttu-id="7096e-160">É importante tooprotect acesso tooyour lote conta chaves tooprevent esse cenário.</span><span class="sxs-lookup"><span data-stu-id="7096e-160">It's important tooprotect access tooyour Batch account keys tooprevent such a scenario.</span></span> <span data-ttu-id="7096e-161">Se você suspeitar de que sua conta pode ter sido comprometida, ser tooregenerate-se de que suas chaves.</span><span class="sxs-lookup"><span data-stu-id="7096e-161">If you suspect your account may have been compromised, be sure tooregenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="7096e-162">Executar uma tarefa como um usuário automático com acesso elevado</span><span class="sxs-lookup"><span data-stu-id="7096e-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="7096e-163">Você pode configurar a especificação de usuário automático Olá privilégios de administrador quando precisar toorun uma tarefa com acesso com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="7096e-163">You can configure hello auto-user specification for administrator privileges when you need toorun a task with elevated access.</span></span> <span data-ttu-id="7096e-164">Por exemplo, uma tarefa inicial pode ser necessário software de tooinstall de acesso com privilégios elevados no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="7096e-164">For example, a start task may need elevated access tooinstall software on hello node.</span></span>

> [!NOTE] 
> <span data-ttu-id="7096e-165">Em geral, é melhor toouse elevados acesso somente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="7096e-165">In general, it's best toouse elevated access only when necessary.</span></span> <span data-ttu-id="7096e-166">As práticas recomendadas sugerem concedendo o resultado desejado do Olá Olá privilégio mínimo necessário tooachieve.</span><span class="sxs-lookup"><span data-stu-id="7096e-166">Best practices recommend granting hello minimum privilege necessary tooachieve hello desired outcome.</span></span> <span data-ttu-id="7096e-167">Por exemplo, se uma tarefa inicial instala o software para o usuário atual do hello, em vez de para todos os usuários, você pode ser capaz de tooavoid concedendo acesso elevado tootasks.</span><span class="sxs-lookup"><span data-stu-id="7096e-167">For example, if a start task installs software for hello current user, instead of for all users, you may be able tooavoid granting elevated access tootasks.</span></span> <span data-ttu-id="7096e-168">Você pode configurar a especificação de saudação do usuário de automática para acesso de escopo e não-administrador do pool para todas as tarefas que precisam de toorun em Olá a mesma conta, incluindo Olá Iniciar tarefa.</span><span class="sxs-lookup"><span data-stu-id="7096e-168">You can configure hello auto-user specification for pool scope and non-admin access for all tasks that need toorun under hello same account, including hello start task.</span></span> 
>
>

<span data-ttu-id="7096e-169">Olá trechos de código a seguir mostra como tooconfigure Olá especificação de usuário automático.</span><span class="sxs-lookup"><span data-stu-id="7096e-169">hello following code snippets show how tooconfigure hello auto-user specification.</span></span> <span data-ttu-id="7096e-170">exemplos de saudação definem nível de elevação de saudação muito`Admin` e Olá escopo muito`Task`.</span><span class="sxs-lookup"><span data-stu-id="7096e-170">hello examples set hello elevation level too`Admin` and hello scope too`Task`.</span></span> <span data-ttu-id="7096e-171">Escopo da tarefa é a configuração padrão de saudação, mas é incluído aqui para bem saudação do exemplo.</span><span class="sxs-lookup"><span data-stu-id="7096e-171">Task scope is hello default setting, but is included here for hello sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="7096e-172">.NET no Lote</span><span class="sxs-lookup"><span data-stu-id="7096e-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="7096e-173">Java no Lote</span><span class="sxs-lookup"><span data-stu-id="7096e-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="7096e-174">Python no Lote</span><span class="sxs-lookup"><span data-stu-id="7096e-174">Batch Python</span></span>

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="7096e-175">Executar uma tarefa como um usuário automático com escopo de pool</span><span class="sxs-lookup"><span data-stu-id="7096e-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="7096e-176">Quando um nó é provisionado, duas todo o pool de autocontas de usuário são criadas em cada nó no pool hello, com acesso com privilégios elevados e sem acesso com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="7096e-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in hello pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="7096e-177">Configuração toopool escopo Olá automática do usuário para uma determinada tarefa executa a tarefa de saudação em uma dessas duas autousuários em todo o pool de contas.</span><span class="sxs-lookup"><span data-stu-id="7096e-177">Setting hello auto-user's scope toopool scope for a given task runs hello task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="7096e-178">Quando você especifica o escopo de pool de usuário Olá automática, todas as tarefas que são executados com acesso de administrador executar sob Olá mesma conta de usuário automaticamente todo o pool.</span><span class="sxs-lookup"><span data-stu-id="7096e-178">When you specify pool scope for hello auto-user, all tasks that run with administrator access run under hello same pool-wide auto-user account.</span></span> <span data-ttu-id="7096e-179">Da mesma forma, as tarefas executadas sem permissões de administrador também o são em uma única conta de usuário automático em todo o pool.</span><span class="sxs-lookup"><span data-stu-id="7096e-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="7096e-180">Olá duas todo o pool de autocontas de usuário são contas separadas.</span><span class="sxs-lookup"><span data-stu-id="7096e-180">hello two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="7096e-181">Tarefas em execução sob a conta administrativa de todo o pool de saudação não podem compartilhar dados com tarefas em execução na conta padrão Olá e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="7096e-181">Tasks running under hello pool-wide administrative account cannot share data with tasks running under hello standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="7096e-182">Olá toorunning vantagem em Olá a mesma conta de usuário automático é tarefas são tooshare capaz de dados com outras tarefas em execução no hello mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="7096e-182">hello advantage toorunning under hello same auto-user account is that tasks are able tooshare data with other tasks running on hello same node.</span></span>

<span data-ttu-id="7096e-183">Compartilhamento de segredos entre tarefas é um cenário em que a execução de tarefas em uma saudação duas contas de usuário automaticamente todo o pool é útil.</span><span class="sxs-lookup"><span data-stu-id="7096e-183">Sharing secrets between tasks is one scenario where running tasks under one of hello two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="7096e-184">Por exemplo, suponha que uma tarefa inicial precisa tooprovision um segredo no nó de saudação que pode usar outras tarefas.</span><span class="sxs-lookup"><span data-stu-id="7096e-184">For example, suppose a start task needs tooprovision a secret onto hello node that other tasks can use.</span></span> <span data-ttu-id="7096e-185">Você pode usar o hello API de proteção de dados do Windows (DPAPI), mas requer privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="7096e-185">You could use hello Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="7096e-186">Em vez disso, você pode proteger segredo Olá no nível de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="7096e-186">Instead, you can protect hello secret at hello user level.</span></span> <span data-ttu-id="7096e-187">Tarefas em execução em Olá a mesma conta de usuário pode acessar Olá segredo sem acesso com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="7096e-187">Tasks running under hello same user account can access hello secret without elevated access.</span></span>

<span data-ttu-id="7096e-188">Outro cenário em que convém toorun tarefas com uma conta de usuário automático com escopo de pool é um arquivo de Interface MPI (Message Passing) compartilhar.</span><span class="sxs-lookup"><span data-stu-id="7096e-188">Another scenario where you may want toorun tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="7096e-189">Um compartilhamento de arquivos MPI é útil quando nós Olá Olá MPI tarefa necessidade toowork em Olá mesmos dados de arquivo.</span><span class="sxs-lookup"><span data-stu-id="7096e-189">An MPI file share is useful when hello nodes in hello MPI task need toowork on hello same file data.</span></span> <span data-ttu-id="7096e-190">nó principal Hello cria um compartilhamento de arquivos que nós filho de saudação podem acessar se eles estiverem executando em Olá mesma conta de usuário automático.</span><span class="sxs-lookup"><span data-stu-id="7096e-190">hello head node creates a file share that hello child nodes can access if they are running under hello same auto-user account.</span></span> 

<span data-ttu-id="7096e-191">Olá trecho de código a seguir define toopool escopo Olá automática do usuário para uma tarefa no .NET de lote.</span><span class="sxs-lookup"><span data-stu-id="7096e-191">hello following code snippet sets hello auto-user's scope toopool scope for a task in Batch .NET.</span></span> <span data-ttu-id="7096e-192">nível de elevação Olá for omitido, tarefa Olá é executado na conta de autousuário todo o pool padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="7096e-192">hello elevation level is omitted, so hello task runs under hello standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="7096e-193">Contas de usuário nomeado</span><span class="sxs-lookup"><span data-stu-id="7096e-193">Named user accounts</span></span>

<span data-ttu-id="7096e-194">Você pode definir contas de usuário nomeado ao criar um pool.</span><span class="sxs-lookup"><span data-stu-id="7096e-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="7096e-195">Uma conta de usuário nomeado tem um nome e uma senha fornecidos por você.</span><span class="sxs-lookup"><span data-stu-id="7096e-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="7096e-196">Você pode especificar o nível de elevação Olá para uma conta de usuário nomeado.</span><span class="sxs-lookup"><span data-stu-id="7096e-196">You can specify hello elevation level for a named user account.</span></span> <span data-ttu-id="7096e-197">Para nós Linux, você também pode fornecer uma chave privada SSH.</span><span class="sxs-lookup"><span data-stu-id="7096e-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="7096e-198">Uma conta de usuário nomeado existe em todos os nós no pool de saudação e está disponível tooall tarefas em execução em nós.</span><span class="sxs-lookup"><span data-stu-id="7096e-198">A named user account exists on all nodes in hello pool and is available tooall tasks running on those nodes.</span></span> <span data-ttu-id="7096e-199">É possível definir qualquer número de usuários nomeados para um pool.</span><span class="sxs-lookup"><span data-stu-id="7096e-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="7096e-200">Quando você adiciona uma tarefa ou um conjunto de tarefas, você pode especificar que essa tarefa Olá é executado em uma saudação chamada contas de usuário definidas no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="7096e-200">When you add a task or task collection, you can specify that hello task runs under one of hello named user accounts defined on hello pool.</span></span>

<span data-ttu-id="7096e-201">Uma conta de usuário nomeado é útil quando você deseja toorun todas as tarefas em um trabalho em Olá a mesma conta de usuário, mas isolá-los de tarefas em execução em outros trabalhos em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="7096e-201">A named user account is useful when you want toorun all tasks in a job under hello same user account, but isolate them from tasks running in other jobs at hello same time.</span></span> <span data-ttu-id="7096e-202">Por exemplo, é possível criar um usuário nomeado para cada trabalho e executar as tarefas de cada trabalho nessa conta de usuário nomeado.</span><span class="sxs-lookup"><span data-stu-id="7096e-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="7096e-203">Cada trabalho pode compartilhar um segredo com suas próprias tarefas, mas não com tarefas em execução em outros trabalhos.</span><span class="sxs-lookup"><span data-stu-id="7096e-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="7096e-204">Você também pode usar uma conta de usuário nomeado toorun uma tarefa que define permissões de recursos externos, como compartilhamentos de arquivos.</span><span class="sxs-lookup"><span data-stu-id="7096e-204">You can also use a named user account toorun a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="7096e-205">Com uma conta de usuário nomeado, você controlar a identidade do usuário hello e pode usar essa identidade tooset permissões do usuário.</span><span class="sxs-lookup"><span data-stu-id="7096e-205">With a named user account, you control hello user identity and can use that user identity tooset permissions.</span></span>  

<span data-ttu-id="7096e-206">As contas de usuário nomeado permitem o SSH sem senha entre os nós Linux.</span><span class="sxs-lookup"><span data-stu-id="7096e-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="7096e-207">Você pode usar uma conta de usuário nomeado conosco do Linux que precisam de tarefas de várias instâncias de toorun.</span><span class="sxs-lookup"><span data-stu-id="7096e-207">You can use a named user account with Linux nodes that need toorun multi-instance tasks.</span></span> <span data-ttu-id="7096e-208">Cada nó no pool de saudação pode executar tarefas em uma conta de usuário definida no pool inteiro hello.</span><span class="sxs-lookup"><span data-stu-id="7096e-208">Each node in hello pool can run tasks under a user account defined on hello whole pool.</span></span> <span data-ttu-id="7096e-209">Para obter mais informações sobre tarefas de várias instâncias, consulte [usar várias\-instância tarefas aplicativos de MPI toorun](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="7096e-209">For more information about multi-instance tasks, see [Use multi\-instance tasks toorun MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="7096e-210">Criar contas de usuário nomeado</span><span class="sxs-lookup"><span data-stu-id="7096e-210">Create named user accounts</span></span>

<span data-ttu-id="7096e-211">toocreate chamado contas de usuário em lote, adicionar uma coleção de pool de toohello de contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="7096e-211">toocreate named user accounts in Batch, add a collection of user accounts toohello pool.</span></span> <span data-ttu-id="7096e-212">Olá trechos de código a seguir mostram como toocreate nomeados contas de usuário no .NET, Java e Python.</span><span class="sxs-lookup"><span data-stu-id="7096e-212">hello following code snippets show how toocreate named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="7096e-213">Esses mostrar trechos de código como toocreate chamada contas em um pool não-administrador e o administrador.</span><span class="sxs-lookup"><span data-stu-id="7096e-213">These code snippets show how toocreate both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="7096e-214">exemplos de saudação criam pools usando a configuração de serviço de nuvem hello, mas use Olá mesma abordagem ao criar um pool do Windows ou Linux usando a configuração de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="7096e-214">hello examples create pools using hello cloud service configuration, but you use hello same approach when creating a Windows or Linux pool using hello virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="7096e-215">Exemplo de .NET do Lote (Windows)</span><span class="sxs-lookup"><span data-stu-id="7096e-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using hello cloud service configuration.
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

// Commit hello pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="7096e-216">Exemplo de .NET do Lote (Linux)</span><span class="sxs-lookup"><span data-stu-id="7096e-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello virtual machine configuration toouse toocreate hello pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create hello unbound pool.
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

// Commit hello pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="7096e-217">Exemplo de Java no Lote</span><span class="sxs-lookup"><span data-stu-id="7096e-217">Batch Java example</span></span>

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

#### <a name="batch-python-example"></a><span data-ttu-id="7096e-218">Exemplo de Python no Lote</span><span class="sxs-lookup"><span data-stu-id="7096e-218">Batch Python example</span></span>

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="7096e-219">Executar uma tarefa em uma conta de usuário nomeado com acesso elevado</span><span class="sxs-lookup"><span data-stu-id="7096e-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="7096e-220">toorun uma tarefa como de um usuário elevado, conjunto de tarefas de saudação **UserIdentity** tooa propriedade denominada conta de usuário que foi criada com sua **ElevationLevel** propriedade definida muito`Admin`.</span><span class="sxs-lookup"><span data-stu-id="7096e-220">toorun a task as an elevated user, set hello task's **UserIdentity** property tooa named user account that was created with its **ElevationLevel** property set too`Admin`.</span></span>

<span data-ttu-id="7096e-221">Este trecho de código especifica a que tarefa Olá deve executar sob uma conta de usuário nomeado.</span><span class="sxs-lookup"><span data-stu-id="7096e-221">This code snippet specifies that hello task should run under a named user account.</span></span> <span data-ttu-id="7096e-222">Essa conta de usuário nomeado foi definida no pool de saudação quando Olá pool foi criado.</span><span class="sxs-lookup"><span data-stu-id="7096e-222">This named user account was defined on hello pool when hello pool was created.</span></span> <span data-ttu-id="7096e-223">Nesse caso, Olá denominado conta de usuário foi criada com permissões de administrador:</span><span class="sxs-lookup"><span data-stu-id="7096e-223">In this case, hello named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a><span data-ttu-id="7096e-224">Atualizar sua biblioteca de cliente de lote mais recente do código toohello</span><span class="sxs-lookup"><span data-stu-id="7096e-224">Update your code toohello latest Batch client library</span></span>

<span data-ttu-id="7096e-225">versão do serviço de lote Olá 2017-01-01.4.0 apresenta uma alteração significativa, substituindo Olá **runElevated** propriedade disponível em versões anteriores com hello **userIdentity** propriedade.</span><span class="sxs-lookup"><span data-stu-id="7096e-225">hello Batch service version 2017-01-01.4.0 introduces a breaking change, replacing hello **runElevated** property available in earlier versions with hello **userIdentity** property.</span></span> <span data-ttu-id="7096e-226">Olá tabelas a seguir fornece um simples de mapeamento que você pode usar tooupdate seu código de versões anteriores de bibliotecas de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="7096e-226">hello following tables provide a simple mapping that you can use tooupdate your code from earlier versions of hello client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="7096e-227">.NET no Lote</span><span class="sxs-lookup"><span data-stu-id="7096e-227">Batch .NET</span></span>

| <span data-ttu-id="7096e-228">Se seu código usar...</span><span class="sxs-lookup"><span data-stu-id="7096e-228">If your code uses...</span></span>                  | <span data-ttu-id="7096e-229">Atualize-o para...</span><span class="sxs-lookup"><span data-stu-id="7096e-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="7096e-230">`CloudTask.RunElevated` não especificado</span><span class="sxs-lookup"><span data-stu-id="7096e-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="7096e-231">Nenhuma atualização é necessária</span><span class="sxs-lookup"><span data-stu-id="7096e-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="7096e-232">Java no Lote</span><span class="sxs-lookup"><span data-stu-id="7096e-232">Batch Java</span></span>

| <span data-ttu-id="7096e-233">Se seu código usar...</span><span class="sxs-lookup"><span data-stu-id="7096e-233">If your code uses...</span></span>                      | <span data-ttu-id="7096e-234">Atualize-o para...</span><span class="sxs-lookup"><span data-stu-id="7096e-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="7096e-235">`CloudTask.withRunElevated` não especificado</span><span class="sxs-lookup"><span data-stu-id="7096e-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="7096e-236">Nenhuma atualização é necessária</span><span class="sxs-lookup"><span data-stu-id="7096e-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="7096e-237">Python no Lote</span><span class="sxs-lookup"><span data-stu-id="7096e-237">Batch Python</span></span>

| <span data-ttu-id="7096e-238">Se seu código usar...</span><span class="sxs-lookup"><span data-stu-id="7096e-238">If your code uses...</span></span>                      | <span data-ttu-id="7096e-239">Atualize-o para...</span><span class="sxs-lookup"><span data-stu-id="7096e-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="7096e-240">`user_identity=user`, em que</span><span class="sxs-lookup"><span data-stu-id="7096e-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="7096e-241">`user_identity=user`, em que</span><span class="sxs-lookup"><span data-stu-id="7096e-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="7096e-242">`run_elevated` não especificado</span><span class="sxs-lookup"><span data-stu-id="7096e-242">`run_elevated` not specified</span></span> | <span data-ttu-id="7096e-243">Nenhuma atualização é necessária</span><span class="sxs-lookup"><span data-stu-id="7096e-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="7096e-244">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7096e-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="7096e-245">Fórum do Lote</span><span class="sxs-lookup"><span data-stu-id="7096e-245">Batch Forum</span></span>

<span data-ttu-id="7096e-246">Olá [Fórum do lote do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) no MSDN é um ótimo colocar toodiscuss em lotes e fazer perguntas sobre o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="7096e-246">hello [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="7096e-247">Acesse diretamente as postagens úteis fixadas e poste suas dúvidas conforme elas surgirem enquanto você cria suas soluções do Lote.</span><span class="sxs-lookup"><span data-stu-id="7096e-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>
