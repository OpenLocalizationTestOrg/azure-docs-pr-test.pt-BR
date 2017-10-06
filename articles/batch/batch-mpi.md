---
title: "várias instâncias de aaaUse tarefas aplicativos de MPI toorun - lote do Azure | Microsoft Docs"
description: "Saiba como tipo de aplicativos de Interface MPI (Message Passing) tooexecute usando a tarefa de várias instâncias de saudação em lote do Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a>Usar várias instâncias tarefas toorun passando Interface aplicativos MPI (Message) em lote

Várias instâncias tarefas permitem que você toorun uma tarefa de lote do Azure em vários nós de computação simultaneamente. Essas tarefas permitem cenários de computação de alto desempenho, como aplicativos MPI (Interface de Transmissão de Mensagens) no Lote. Neste artigo, você aprenderá como tarefas de várias instâncias de tooexecute usando Olá [Batch .NET] [ api_net] biblioteca.

> [!NOTE]
> Enquanto os exemplos neste artigo Olá se concentrar no .NET de lote, MS-MPI, e nós de computação do Windows, conceitos de tarefa de várias instâncias de Olá discutidos aqui são aplicáveis tooother plataformas e tecnologias (Python e Intel MPI em nós do Linux, por exemplo).
>
>

## <a name="multi-instance-task-overview"></a>Visão geral da tarefa de várias instâncias
Em lote, cada tarefa é normalmente executada em um único nó de computação – enviar o trabalho de tooa várias tarefas e Olá serviço de lote agenda cada tarefa para execução em um nó. No entanto, ao configurar uma tarefa **configurações com várias instâncias**, informe o lote tooinstead criar uma tarefa principal e várias subtarefas que são executadas em vários nós.

![Visão geral da tarefa de várias instâncias][1]

Quando você enviar uma tarefa com o trabalho de tooa de configurações de várias instâncias, o lote executa várias tarefas de instância exclusiva de toomulti etapas:

1. Olá serviço de lote cria um **primário** e várias **subtarefas** com base nas configurações de várias instâncias de saudação. número total de saudação de tarefas (primários além de todas as subtarefas) corresponde o número de saudação do **instâncias** (nós de computação) você especificar nas configurações de várias instâncias de saudação.
2. Lote designa uma saudação nós de computação como Olá **mestre**, e agendamentos Olá tooexecute tarefa primária no mestre de saudação. Ele agenda Olá subtarefas tooexecute no restante da saudação da tarefa de várias instâncias do toohello alocado de nós de computação hello, uma subtarefa por nó.
3. Olá primária e todas as subtarefas baixar qualquer **arquivos comuns do recurso** você especificar nas configurações de várias instâncias de saudação.
4. Depois que os arquivos de recursos comuns Olá tiverem sido baixados, hello primário e subtarefas executar Olá **comando coordenação** você especificar nas configurações de várias instâncias de saudação. comando de coordenação de saudação é nós tooprepare geralmente usados para executar tarefas de saudação. Isso pode incluir serviços em segundo plano (como [Microsoft MPI][msmpi_msdn]do `smpd.exe`) e verificar se nós de saudação são mensagens do nó entre tooprocess pronto.
5. tarefa principal de saudação executa Olá **comando aplicativo** no nó mestre Olá *depois* Olá coordenação comando foi concluído com êxito pelo hello primária e todas as subtarefas. comando do aplicativo Hello Olá de linha de comando da tarefa de várias instâncias de saudação em si e é executado somente por tarefa principal de saudação. Em uma solução baseada em [MS-MPI][msmpi_msdn], é onde você executa seu aplicativo habilitado para MPI usando o `mpiexec.exe`.

> [!NOTE]
> Embora seja funcionalmente distinto, Olá "tarefa de várias instâncias" não é um tipo de exclusiva da tarefa como Olá [StartTask] [ net_starttask] ou [JobPreparationTask] [ net_jobprep]. Olá várias instâncias é simplesmente uma tarefa de lote padrão ([CloudTask] [ net_task] no lote .NET) cujas configurações de várias instâncias foram configuradas. Neste artigo, nós nos referimos toothis como Olá **tarefas de várias instâncias**.
>
>

## <a name="requirements-for-multi-instance-tasks"></a>Requisitos para tarefas de várias instâncias
As tarefas de várias instâncias exigem um pool com **comunicação entre nós habilitada** e com a **execução de tarefas simultâneas desabilitada**. execução de tarefas simultâneas toodisable, Olá conjunto [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) too1 de propriedade.

Este trecho de código mostra como toocreate um pool para várias instâncias tarefas usando biblioteca de lote .NET hello.

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> Se você tentar toorun uma tarefa de várias instâncias em um pool com na comunicação desabilitada ou com um *maxTasksPerNode* valor maior que 1, tarefa Olá nunca foi programada – indefinidamente, ele permanecerá no estado "ativo" hello. 
>
> As tarefas de várias instâncias poderão ser executadas somente em nós nos pools criados após 14 de dezembro de 2015.
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a>Use um tooinstall StartTask MPI
aplicativos de MPI toorun com uma tarefa de várias instâncias, você primeiro precisa tooinstall uma implementação de MPI (MS-MPI ou MPI Intel, por exemplo) em nós de computação Olá no pool de saudação. Este é um bom momento toouse um [StartTask][net_starttask], que é executado sempre que um nó une um pool ou reiniciado. Este trecho de código cria um StartTask que especifica o pacote de instalação Olá MS-MPI como um [arquivo de recurso][net_resourcefile]. linha de comando da tarefa de saudação inicial é executada após o arquivo de recurso Olá nó toohello baixado. Nesse caso, a linha de comando de saudação realiza uma instalação autônoma do MS-MPI.

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a>Acesso remoto direto à memória (RDMA)
Quando você escolhe um [tamanho compatíveis com RDMA](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) como A9 para Olá nós de computação no pool de lote, seu aplicativo MPI pode tirar proveito da rede de acesso (RDMA) de alto desempenho e baixa latência memória direta remota do Azure.

Procure os tamanhos de saudação especificados como "Compatíveis com RDMA" no hello artigos a seguir:

* Pools **CloudServiceConfiguration**

  * [Tamanhos de serviços de nuvem](../cloud-services/cloud-services-sizes-specs.md) (somente Windows)
* Pools de **VirtualMachineConfiguration**

  * [Tamanhos das máquinas virtuais no Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)
  * [Tamanhos das máquinas virtuais no Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)

> [!NOTE]
> tootake vantagem de RDMA em [nós de computação Linux](batch-linux-nodes.md), você deve usar **Intel MPI** em nós de saudação. Para obter mais informações sobre pools de CloudServiceConfiguration e VirtualMachineConfiguration, consulte Olá Olá seção Pool [visão geral do recurso de lote](batch-api-basics.md).
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a>Criar uma tarefa de várias instâncias com o .NET do Lote
Agora que falamos sobre requisitos de pool hello e instalação do pacote MPI, vamos criar tarefa de várias instâncias de saudação. Neste trecho de código, criamos uma [CloudTask][net_task] padrão e configuramos sua propriedade [MultiInstanceSettings][net_multiinstance_prop]. Como mencionado anteriormente, tarefas de várias instâncias de saudação não é um tipo distinto de tarefas, mas uma tarefa de lote padrão configurado com configurações de várias instâncias.

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a>Tarefa principal e subtarefas
Quando você cria Olá configurações com várias instâncias de uma tarefa, você especifica o número de saudação de nós de computação que são tarefas de saudação tooexecute. Ao enviar trabalho tooa hello, Olá serviço de lote cria um **primário** tarefa e suficiente **subtarefas** que corresponde o número de saudação de nós especificados juntos.

Essas tarefas são atribuídas a uma id de inteiro no intervalo 0 Olá muito*numberOfInstances* - 1. Olá tarefa com id 0 é Olá primário e todos os outros ids são subtarefas. Por exemplo, se você criar hello configurações com várias instâncias de uma tarefa a seguir, tarefa primária Olá teria uma id 0 e subtarefas Olá teria ids de 1 a 9.

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a>Nó mestre
Quando você envia uma tarefa de várias instâncias, Olá serviço de lote designa uma saudação nós de computação como nó de "mestre" hello e agendas Olá tooexecute tarefa primária no nó mestre hello. Olá subtarefas são agendada tooexecute no restante Olá Olá nós alocada toohello tarefa de várias instâncias.

## <a name="coordination-command"></a>comando de coordenação
Olá **comando coordenação** é executado pelo Olá primário e subtarefas.

bloqueio de invocação de saudação do comando de coordenação hello – lote não executar comando de saudação do aplicativo até que o comando de coordenação de saudação retornou com êxito para todas as subtarefas. comando de coordenação Hello, portanto, deve iniciar todos os serviços necessários em segundo plano, verifique que estão prontos para uso e saia. Por exemplo, este comando coordenação para uma solução usando o MS-MPI versão 7 inicia o serviço SMPD de saudação no nó hello e será encerrado:

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

Observe o uso de saudação do `start` nesse comando de coordenação. Isso é necessário porque Olá `smpd.exe` aplicativo não retorna imediatamente após a execução. Sem o uso de saudação de saudação [iniciar] [ cmd_start] de comando, esse comando de coordenação não retornaria e, portanto, seria bloqueada Olá aplicativo execução do comando.

## <a name="application-command"></a>Comando de aplicativo
Quando Olá primário e todos os subtarefas terminarem de executar o comando de coordenação de saudação, linha de comando da tarefa de várias instâncias de saudação é executada pela tarefa primária Olá *somente*. Chamamos essa Olá **comando aplicativo** toodistinguish do comando de coordenação de saudação.

Para aplicativos do MS-MPI, use Olá aplicativo comando tooexecute seu aplicativo habilitado para MPI com `mpiexec.exe`. Por exemplo, eis um comando do aplicativo para uma solução usando o MS-MPI versão 7:

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> Como MS-MPI `mpiexec.exe` usa Olá `CCP_NODES` variável por padrão (consulte [variáveis de ambiente](#environment-variables)) exemplo hello acima da linha de comando de aplicativo exclui-lo.
>
>

## <a name="environment-variables"></a>Variáveis de ambiente
Lote cria várias [variáveis de ambiente] [ msdn_env_var] tarefas específicas da instância de toomulti Olá nós alocada tooa tarefa de várias instâncias de computação. As linhas de comando coordenação e o aplicativo pode fazer referência a essas variáveis de ambiente, que pode Olá scripts e programas que foram executadas.

Olá seguintes variáveis de ambiente são criados pelo serviço de lote Olá para uso pelas tarefas de várias instâncias:

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

Para obter detalhes completos sobre eles e hello outras variáveis de ambiente de nó da computação de lote, incluindo o conteúdo e a visibilidade, consulte [variáveis de ambiente do nó de computação][msdn_env_var].

> [!TIP]
> exemplo de código do lote Linux MPI Olá contém um exemplo de como vários dessas variáveis de ambiente podem ser usados. Olá [coordenação cmd] [ coord_cmd_example] Bash script faz o download de aplicativos comuns e arquivos de entrada do armazenamento do Azure, permite que um compartilhamento de sistema de arquivos de rede (NFS) no nó mestre hello e configura Olá outros nós alocada a tarefa de várias instâncias de toohello como clientes NFS.
>
>

## <a name="resource-files"></a>Arquivos de recurso
Há dois conjuntos de tooconsider de arquivos de recursos para tarefas de várias instâncias: **arquivos comuns do recurso** que *todos os* tarefas baixar (principal e subtarefas) e hello **arquivosderecurso** especificado para hello várias instâncias de tarefas em si, que *somente Olá primário* downloads de tarefas.

Você pode especificar um ou mais **arquivos comuns do recurso** nas configurações de várias instâncias de saudação para uma tarefa. Esses arquivos de recursos comuns são baixados de [armazenamento do Azure](../storage/common/storage-introduction.md) em cada nó **diretório compartilhado de tarefa** Olá primária e todas as subtarefas. Você pode acessar o diretório compartilhado de tarefa de saudação do aplicativo e a coordenação de linhas de comando usando Olá `AZ_BATCH_TASK_SHARED_DIR` variável de ambiente. Olá `AZ_BATCH_TASK_SHARED_DIR` caminho é idêntico em todas as tarefas de várias instâncias do nó toohello alocado, assim, você pode compartilhar um comando único coordenação entre hello primária e todas as subtarefas. Lote não "compartilhar" hello diretório em um sentido de acesso remoto, mas você pode usá-lo como uma montagem ou compartilhar um ponto, conforme mencionado anteriormente na ponta de saudação em variáveis de ambiente.

Arquivos de recursos que você especificar para a própria tarefa de várias instâncias hello são diretório de trabalho da tarefa toohello baixado, `AZ_BATCH_TASK_WORKING_DIR`, por padrão. Conforme mencionado, por outro lado toocommon arquivos de recursos, somente tarefa principal de saudação baixa arquivos de recurso especificados para tarefa de várias instâncias de saudação em si.

> [!IMPORTANT]
> Sempre use variáveis de ambiente Olá `AZ_BATCH_TASK_SHARED_DIR` e `AZ_BATCH_TASK_WORKING_DIR` toorefer diretórios toothese as linhas de comando. Não tente caminhos de saudação tooconstruct manualmente.
>
>

## <a name="task-lifetime"></a>Tempo de vida da tarefa
tempo de vida de saudação do tempo de vida do hello tarefa primária controles Olá da tarefa de toda a multi-instância Olá. Quando Olá primário for encerrada, todas as subtarefas Olá são encerradas. código de saída de saudação do hello primário é Olá código de saída da tarefa de saudação e é, portanto, toodetermine usado Olá êxito ou falha da tarefa Olá para fins de repetição.

Se qualquer Olá subtarefas falhar, sair com um código de retorno diferente de zero, por exemplo, Olá toda multi-instância de tarefa falhará. tarefa de várias instâncias de saudação é encerrada e repetida, o limite de tentativas de tooits.

Quando você exclui uma tarefa de várias instâncias, hello primária e todas as subtarefas também são excluídas pelo serviço de lote de saudação. Todos os diretórios de subtarefa e seus arquivos são excluídos de nós de computação hello, como uma tarefa padrão.

[TaskConstraints] [ net_taskconstraints] para uma tarefa de várias instâncias, como Olá [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], e [RetentionTime] [ net_taskconstraint_retention] propriedades, são respeitadas conforme elas são para uma tarefa padrão e aplicam toohello primário e todas as subtarefas. No entanto, se você alterar Olá [RetentionTime] [ net_taskconstraint_retention] propriedade depois de adicionar Olá várias instâncias toohello trabalho, essa alteração é aplicada toohello somente principal tarefa. Todas as subtarefas Olá continuam toouse Olá original [RetentionTime][net_taskconstraint_retention].

Lista de tarefas recentes de um nó de computação reflete id Olá uma subtarefa se tarefa recente Olá fizer parte de uma tarefa de várias instâncias.

## <a name="obtain-information-about-subtasks"></a>Obtenha informações sobre subtarefas
informações de tooobtain subtarefas usando biblioteca de lote .NET hello, chamada hello [CloudTask.ListSubtasks] [ net_task_listsubtasks] método. Esse método retorna informações sobre todas as subtarefas e informações sobre Olá computação nó Olá tarefas executadas. Essas informações, você pode determinar o diretório raiz de cada da subtarefa, id do pool hello, seu estado atual, código de saída e muito mais. Você pode usar essas informações em combinação com hello [PoolOperations.GetNodeFile] [ poolops_getnodefile] arquivos da subtarefa do método tooobtain hello. Observe que esse método não retorna informações de tarefa principal de saudação (id 0).

> [!NOTE]
> A menos que indicado o contrário, os métodos do .NET em lotes que operam em Olá várias instâncias [CloudTask] [ net_task] se aplicar *somente* toohello principal tarefa. Por exemplo, quando você chama Olá [CloudTask.ListNodeFiles] [ net_task_listnodefiles] método em uma tarefa de várias instâncias, somente os arquivos da tarefa primária Olá são retornados.
>
>

Olá trecho de código a seguir mostra como tooobtain subtarefa informações, bem como solicitar o conteúdo do arquivo de nós Olá na qual eles executado.

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a>Exemplo de código
Olá [MultiInstanceTasks] [ github_mpi] exemplo de código no GitHub demonstra como toouse uma instância de várias tarefas toorun um [MS-MPI] [ msmpi_msdn] aplicativo em nós de computação do lote. Siga as etapas de saudação em [preparação](#preparation) e [execução](#execution) exemplo hello de toorun.

### <a name="preparation"></a>Preparação
1. Execute as duas primeiras etapas Olá no [como toocompile e executar um programa simple do MS-MPI][msmpi_howto]. Isso atende etapa prerequesites Olá para Olá a seguir.
2. Criar um *versão* versão do hello [MPIHelloWorld] [ helloworld_proj] programa MPI de exemplo. Este é o programa de saudação que será executado em nós de computação pela tarefa de várias instâncias de saudação.
3. Criar um arquivo zip contendo `MPIHelloWorld.exe` (compilado na etapa 2) e `MSMpiSetup.exe` (baixado na etapa 1). Você carregará o arquivo zip como um pacote de aplicativo na próxima etapa do hello.
4. Saudação de uso [portal do Azure] [ portal] toocreate um lote [aplicativo](batch-application-packages.md) chamado "MPIHelloWorld" e especifique o arquivo zip de saudação criado na etapa anterior hello como "1.0" da versão do pacote de aplicativo Hello. Veja [Carregar e gerenciar aplicativos](batch-application-packages.md#upload-and-manage-applications) para saber mais.

> [!TIP]
> Criar um *versão* versão do `MPIHelloWorld.exe` para que você não tenha tooinclude dependências adicionais (por exemplo, `msvcp140d.dll` ou `vcruntime140d.dll`) em seu pacote de aplicativo.
>
>

### <a name="execution"></a>Execução
1. Baixar Olá [exemplos de lote do azure] [ github_samples_zip] do GitHub.
2. Abra Olá MultiInstanceTasks **solução** no Visual Studio 2015 ou mais recente. Olá `MultiInstanceTasks.sln` arquivo de solução está localizado em:

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. Insira suas credenciais de conta de lote e armazenamento em `AccountSettings.settings` em Olá **Microsoft.Azure.Batch.Samples.Common** projeto.
4. **Compilar e executar** Olá MultiInstanceTasks solução tooexecute Olá exemplo aplicativo MPI em nós de computação em um pool de lote.
5. *Opcional*: Olá Use [portal do Azure] [ portal] ou hello [Explorer lote] [ batch_explorer] tooexamine pool de exemplo hello, trabalho, e tarefa ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") antes de excluir os recursos de saudação.

> [!TIP]
> Você pode baixar o [Visual Studio Community][visual_studio] gratuitamente se não tiver o Visual Studio.
>
>

Saída de `MultiInstanceTasks.exe` é a seguir toohello semelhante:

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>Próximas etapas
* blog da equipe de lote do Azure e Microsoft HPC Olá discute [MPI suporte para Linux em lote do Azure][blog_mpi_linux]e inclui informações sobre como usar [OpenFOAM] [ openfoam] com o lote. Você pode encontrar exemplos de código do Python para Olá [OpenFOAM exemplo no GitHub][github_mpi].
* Saiba como muito[criar pools de nós de computação Linux](batch-linux-nodes.md) para uso em suas soluções MPI de lote do Azure.

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "Visão geral de várias instâncias"
