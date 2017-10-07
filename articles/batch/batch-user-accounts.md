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
# <a name="run-tasks-under-user-accounts-in-batch"></a>Executar tarefas em contas de usuário no Lote

Uma tarefa no Lote do Azure sempre é executada em uma conta de usuário. Por padrão, as tarefas são executadas em contas de usuário padrão, sem permissões de administrador. Essas configurações da conta de usuário padrão normalmente são suficientes. Para determinados cenários, no entanto, é útil toobe tooconfigure capaz de saudação usuário conta sob a qual você deseja toorun uma tarefa. Este artigo aborda os tipos de saudação de contas de usuário e como configurá-los para seu cenário.

## <a name="types-of-user-accounts"></a>Tipos de conta de usuário

O Lote do Azure fornece dois tipos de conta de usuário para execução de tarefas:

- **Contas de usuário automático** Contas de usuário automático são contas de usuário internas que são criadas automaticamente pelo serviço de lote de saudação. Por padrão, as tarefas são executadas em uma conta de usuário automático. Você pode configurar a especificação de saudação do usuário de automática para um tooindicate de tarefa em qual usuário automaticamente uma tarefa de conta deve ser executada. especificação de saudação do usuário de automática permite que você toospecify nível de elevação de saudação e escopo Olá autoda conta de usuário que executará a tarefa de saudação. 

- **Uma conta de usuário nomeado** Você pode especificar uma ou mais contas de usuário nomeado para um pool de quando você cria o pool de saudação. Cada conta de usuário é criada em cada nó do pool de saudação. Além disso toohello o nome da conta, especifique a senha de conta de usuário hello, elevação nível e, para pools do Linux, a chave privada SSH hello. Quando você adiciona uma tarefa, você pode especificar Olá denominado conta de usuário sob a qual essa tarefa deve ser executada.

> [!IMPORTANT] 
> versão de serviço de lote Olá 2017-01-01.4.0 apresenta uma alteração significativa requer que você atualize seu código toocall dessa versão. Se você estiver migrando o código de uma versão mais antiga do lote, observe que Olá **runElevated** propriedade não é mais suportada em bibliotecas de cliente de API REST ou lote hello. Saudação de uso novo **userIdentity** propriedade de um nível de elevação de toospecify de tarefa. Consulte a seção de saudação [atualizar sua biblioteca de cliente de lote mais recente do código toohello](#update-your-code-to-the-latest-batch-client-library) para rápido diretrizes para atualizar seu código de lote, se você estiver usando uma das bibliotecas de saudação do cliente.
>
>

> [!NOTE] 
> contas de usuário Olá discutidas neste artigo não dão suporte a protocolo de área de trabalho remota (RDP) ou Secure Shell (SSH), por motivos de segurança. 
>
> tooconnect tooa nó em execução Olá Linux configuração da máquina virtual via SSH, consulte [tooa de área de trabalho remota Use VM do Linux no Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md). toonodes tooconnect que executam o Windows por meio do protocolo RDP, consulte [conectar tooa VM do Windows Server](../virtual-machines/windows/connect-logon.md).<br /><br />
> tooconnect tooa nó em execução Olá serviço configuração de nuvem por meio do protocolo RDP, consulte [habilitar Conexão de área de trabalho remota para uma função nos serviços de nuvem do Azure](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).
>
>

## <a name="user-account-access-toofiles-and-directories"></a>Diretórios e toofiles de acesso de conta de usuário

Uma conta de usuário automático e uma conta de usuário nomeado tem o diretório de trabalho da tarefa de toohello do acesso de leitura/gravação, o diretório compartilhado e o diretório de tarefas de várias instâncias. Os dois tipos de contas tem os diretórios preparação do acesso de leitura toohello inicialização e de trabalho.

Se uma tarefa é executada em Olá mesma conta que foi usada para executar uma tarefa de início, a tarefa de saudação tem o diretório de início de tarefas de toohello de acesso de leitura-gravação. Olá mesmo da mesma forma, se uma tarefa é executada na conta que foi usada para executar uma tarefa de preparação de trabalho, a tarefa de saudação tem diretório tarefas de preparação de trabalho do acesso de leitura-gravação toohello. Se uma tarefa é executada em uma conta diferente de tarefa do saudação inicial ou tarefa de preparação de trabalho, tarefa Olá tem somente acesso de leitura toohello respectiva pasta.

Para saber mais sobre como acessar arquivos e diretórios de uma tarefa, confira [Desenvolver soluções de computação paralela em larga escala com o Lote](batch-api-basics.md#files-and-directories).

## <a name="elevated-access-for-tasks"></a>Acesso elevado para tarefas 

nível de privilégio da conta do usuário Olá indica se uma tarefa é executado com acesso com privilégios elevados. Tanto uma conta de usuário automático, quanto uma conta de usuário nomeado podem ser executadas com acesso elevado. Olá duas opções para o nível de elevação são:

- **NonAdmin:** tarefa Olá é executado como um usuário padrão sem acesso com privilégios elevados. nível de elevação saudação padrão para uma conta de usuário do lote é sempre **NonAdmin**.
- **Administração:** tarefa Olá é executado como um usuário com acesso com privilégios elevados e opera com permissões de administrador completas. 

## <a name="auto-user-accounts"></a>Contas de usuário automático

Por padrão, as tarefas são executadas no Lote em uma conta de usuário automático, como um usuário padrão sem acesso elevado e com escopo de tarefa. Quando a especificação de usuário automático Olá estiver configurada para o escopo da tarefa, o serviço de lote de saudação cria uma conta de usuário automaticamente para essa tarefa somente.

escopo de tootask alternativo de saudação é o escopo de pool. Quando a especificação de saudação do usuário de automática para uma tarefa está configurada para o escopo de pool, tarefa Olá é executado sob uma conta de usuário automático é tarefa tooany disponível no pool de saudação. Para obter mais informações sobre o escopo do pool, consulte a seção de saudação [executar uma tarefa como Olá automático de usuário com escopo de pool](#run-a-task-as-the-autouser-with-pool-scope).   

escopo padrão de saudação é diferente em nós do Windows e Linux:

- Em nós do Windows, as tarefas são executadas no escopo de tarefa por padrão.
- Nós do Linux sempre são executados no escopo de pool.

Há quatro configurações possíveis para especificação de usuário automático hello, cada uma correspondendo tooa única autoconta de usuário:

- Acesso de não-administrador com escopo de tarefa (especificação de usuário automático padrão Olá)
- Acesso de administrador (elevado) com escopo de tarefa
- Acesso de não administrador com escopo de pool
- Acesso de administrador com escopo de pool

> [!IMPORTANT] 
> Tarefas em execução no escopo da tarefa não tem acesso tooother tarefas de fato em um nó. No entanto, um usuário malintencionado com a conta de acesso de toohello pode contornar essa restrição enviando uma tarefa que é executado com privilégios de administrador e acessa outros diretórios de tarefa. Um usuário mal-intencionado também pode usar o nó de tooa tooconnect RDP ou SSH. É importante tooprotect acesso tooyour lote conta chaves tooprevent esse cenário. Se você suspeitar de que sua conta pode ter sido comprometida, ser tooregenerate-se de que suas chaves.
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a>Executar uma tarefa como um usuário automático com acesso elevado

Você pode configurar a especificação de usuário automático Olá privilégios de administrador quando precisar toorun uma tarefa com acesso com privilégios elevados. Por exemplo, uma tarefa inicial pode ser necessário software de tooinstall de acesso com privilégios elevados no nó de saudação.

> [!NOTE] 
> Em geral, é melhor toouse elevados acesso somente quando necessário. As práticas recomendadas sugerem concedendo o resultado desejado do Olá Olá privilégio mínimo necessário tooachieve. Por exemplo, se uma tarefa inicial instala o software para o usuário atual do hello, em vez de para todos os usuários, você pode ser capaz de tooavoid concedendo acesso elevado tootasks. Você pode configurar a especificação de saudação do usuário de automática para acesso de escopo e não-administrador do pool para todas as tarefas que precisam de toorun em Olá a mesma conta, incluindo Olá Iniciar tarefa. 
>
>

Olá trechos de código a seguir mostra como tooconfigure Olá especificação de usuário automático. exemplos de saudação definem nível de elevação de saudação muito`Admin` e Olá escopo muito`Task`. Escopo da tarefa é a configuração padrão de saudação, mas é incluído aqui para bem saudação do exemplo.

#### <a name="batch-net"></a>.NET no Lote

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a>Java no Lote

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a>Python no Lote

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a>Executar uma tarefa como um usuário automático com escopo de pool

Quando um nó é provisionado, duas todo o pool de autocontas de usuário são criadas em cada nó no pool hello, com acesso com privilégios elevados e sem acesso com privilégios elevados. Configuração toopool escopo Olá automática do usuário para uma determinada tarefa executa a tarefa de saudação em uma dessas duas autousuários em todo o pool de contas. 

Quando você especifica o escopo de pool de usuário Olá automática, todas as tarefas que são executados com acesso de administrador executar sob Olá mesma conta de usuário automaticamente todo o pool. Da mesma forma, as tarefas executadas sem permissões de administrador também o são em uma única conta de usuário automático em todo o pool. 

> [!NOTE] 
> Olá duas todo o pool de autocontas de usuário são contas separadas. Tarefas em execução sob a conta administrativa de todo o pool de saudação não podem compartilhar dados com tarefas em execução na conta padrão Olá e vice-versa. 
>
>

Olá toorunning vantagem em Olá a mesma conta de usuário automático é tarefas são tooshare capaz de dados com outras tarefas em execução no hello mesmo nó.

Compartilhamento de segredos entre tarefas é um cenário em que a execução de tarefas em uma saudação duas contas de usuário automaticamente todo o pool é útil. Por exemplo, suponha que uma tarefa inicial precisa tooprovision um segredo no nó de saudação que pode usar outras tarefas. Você pode usar o hello API de proteção de dados do Windows (DPAPI), mas requer privilégios de administrador. Em vez disso, você pode proteger segredo Olá no nível de saudação do usuário. Tarefas em execução em Olá a mesma conta de usuário pode acessar Olá segredo sem acesso com privilégios elevados.

Outro cenário em que convém toorun tarefas com uma conta de usuário automático com escopo de pool é um arquivo de Interface MPI (Message Passing) compartilhar. Um compartilhamento de arquivos MPI é útil quando nós Olá Olá MPI tarefa necessidade toowork em Olá mesmos dados de arquivo. nó principal Hello cria um compartilhamento de arquivos que nós filho de saudação podem acessar se eles estiverem executando em Olá mesma conta de usuário automático. 

Olá trecho de código a seguir define toopool escopo Olá automática do usuário para uma tarefa no .NET de lote. nível de elevação Olá for omitido, tarefa Olá é executado na conta de autousuário todo o pool padrão de saudação.

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a>Contas de usuário nomeado

Você pode definir contas de usuário nomeado ao criar um pool. Uma conta de usuário nomeado tem um nome e uma senha fornecidos por você. Você pode especificar o nível de elevação Olá para uma conta de usuário nomeado. Para nós Linux, você também pode fornecer uma chave privada SSH.

Uma conta de usuário nomeado existe em todos os nós no pool de saudação e está disponível tooall tarefas em execução em nós. É possível definir qualquer número de usuários nomeados para um pool. Quando você adiciona uma tarefa ou um conjunto de tarefas, você pode especificar que essa tarefa Olá é executado em uma saudação chamada contas de usuário definidas no pool de saudação.

Uma conta de usuário nomeado é útil quando você deseja toorun todas as tarefas em um trabalho em Olá a mesma conta de usuário, mas isolá-los de tarefas em execução em outros trabalhos em Olá simultaneamente. Por exemplo, é possível criar um usuário nomeado para cada trabalho e executar as tarefas de cada trabalho nessa conta de usuário nomeado. Cada trabalho pode compartilhar um segredo com suas próprias tarefas, mas não com tarefas em execução em outros trabalhos.

Você também pode usar uma conta de usuário nomeado toorun uma tarefa que define permissões de recursos externos, como compartilhamentos de arquivos. Com uma conta de usuário nomeado, você controlar a identidade do usuário hello e pode usar essa identidade tooset permissões do usuário.  

As contas de usuário nomeado permitem o SSH sem senha entre os nós Linux. Você pode usar uma conta de usuário nomeado conosco do Linux que precisam de tarefas de várias instâncias de toorun. Cada nó no pool de saudação pode executar tarefas em uma conta de usuário definida no pool inteiro hello. Para obter mais informações sobre tarefas de várias instâncias, consulte [usar várias\-instância tarefas aplicativos de MPI toorun](batch-mpi.md).

### <a name="create-named-user-accounts"></a>Criar contas de usuário nomeado

toocreate chamado contas de usuário em lote, adicionar uma coleção de pool de toohello de contas de usuário. Olá trechos de código a seguir mostram como toocreate nomeados contas de usuário no .NET, Java e Python. Esses mostrar trechos de código como toocreate chamada contas em um pool não-administrador e o administrador. exemplos de saudação criam pools usando a configuração de serviço de nuvem hello, mas use Olá mesma abordagem ao criar um pool do Windows ou Linux usando a configuração de máquina virtual de saudação.

#### <a name="batch-net-example-windows"></a>Exemplo de .NET do Lote (Windows)

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

#### <a name="batch-net-example-linux"></a>Exemplo de .NET do Lote (Linux)

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


#### <a name="batch-java-example"></a>Exemplo de Java no Lote

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

#### <a name="batch-python-example"></a>Exemplo de Python no Lote

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a>Executar uma tarefa em uma conta de usuário nomeado com acesso elevado

toorun uma tarefa como de um usuário elevado, conjunto de tarefas de saudação **UserIdentity** tooa propriedade denominada conta de usuário que foi criada com sua **ElevationLevel** propriedade definida muito`Admin`.

Este trecho de código especifica a que tarefa Olá deve executar sob uma conta de usuário nomeado. Essa conta de usuário nomeado foi definida no pool de saudação quando Olá pool foi criado. Nesse caso, Olá denominado conta de usuário foi criada com permissões de administrador:

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a>Atualizar sua biblioteca de cliente de lote mais recente do código toohello

versão do serviço de lote Olá 2017-01-01.4.0 apresenta uma alteração significativa, substituindo Olá **runElevated** propriedade disponível em versões anteriores com hello **userIdentity** propriedade. Olá tabelas a seguir fornece um simples de mapeamento que você pode usar tooupdate seu código de versões anteriores de bibliotecas de saudação do cliente.

### <a name="batch-net"></a>.NET no Lote

| Se seu código usar...                  | Atualize-o para...                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| `CloudTask.RunElevated` não especificado | Nenhuma atualização é necessária                                                                                               |

### <a name="batch-java"></a>Java no Lote

| Se seu código usar...                      | Atualize-o para...                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| `CloudTask.withRunElevated` não especificado | Nenhuma atualização é necessária                                                                                                                     |

### <a name="batch-python"></a>Python no Lote

| Se seu código usar...                      | Atualize-o para...                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | `user_identity=user`, em que <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | `user_identity=user`, em que <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| `run_elevated` não especificado | Nenhuma atualização é necessária                                                                                                                                  |


## <a name="next-steps"></a>Próximas etapas

### <a name="batch-forum"></a>Fórum do Lote

Olá [Fórum do lote do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) no MSDN é um ótimo colocar toodiscuss em lotes e fazer perguntas sobre o serviço de saudação. Acesse diretamente as postagens úteis fixadas e poste suas dúvidas conforme elas surgirem enquanto você cria suas soluções do Lote.
