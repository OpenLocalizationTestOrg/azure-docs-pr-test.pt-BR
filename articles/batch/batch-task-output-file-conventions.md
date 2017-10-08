---
title: "aaaPersist trabalhos e tarefas de saída tooAzure armazenamento com biblioteca de convenções de arquivo hello para .NET - lote do Azure | Microsoft Docs"
description: "Saiba como toouse biblioteca de convenções de arquivo de lote do Azure para .NET toopersist tarefa em lotes e tooAzure de saída do trabalho armazenamento e Olá exibição persistentes saída Olá portal do Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a>Manter o trabalho e dados tooAzure armazenamento com biblioteca de convenções de arquivo em lotes Olá para .NET toopersist de tarefas 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Dados de tarefa toopersist unidirecional são Olá toouse [biblioteca convenções de arquivo de lote do Azure para .NET][nuget_package]. Olá, biblioteca de convenções de arquivo simplifica o processo de saudação de armazenar a saída da tarefa dados tooAzure armazenamento e recuperá-los. Você pode usar Olá convenções arquivo biblioteca em código de cliente e de tarefa &mdash; no código de tarefa para manter arquivos e no cliente de código toolist e recuperá-las. O código de tarefa também pode usar Olá biblioteca tooretrieve Olá saída upstream tarefas, como em um [dependências entre tarefas](batch-task-dependencies.md) cenário. 

tooretrieve saída arquivos com biblioteca de convenções de arquivo hello, você pode localizar arquivos de saudação para um determinado trabalho ou tarefa listá-los por ID e a finalidade. Você não precisa tooknow nomes de saudação ou locais dos arquivos de saudação. Por exemplo, você pode usar toolist de biblioteca de convenções de arquivo hello todos os arquivos intermediários para uma determinada tarefa ou obter um arquivo de visualização para um determinado trabalho.

> [!TIP]
> Começando com a versão de 2017-05-01, Olá API do serviço de lote dá suporte a tooAzure de dados persistentes saída armazenamento para tarefas e tarefas do Gerenciador de trabalho que são executados em pools criados com a configuração de máquina virtual de saudação. Olá API do serviço de lote fornece um toopersist de maneira simples de saída de dentro do código de saudação que cria uma tarefa e serve como uma biblioteca de convenções de arquivo toohello alternativo. Você pode modificar a saída de toopersist de aplicativos de cliente de lote sem a necessidade de aplicativo hello tooupdate que a tarefa está em execução. Para obter mais informações, consulte [persistir dados de tarefa tooAzure armazenamento com a API do serviço de lote de saudação](batch-task-output-files.md).
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a>Quando usar o hello convenções arquivo biblioteca toopersist a saída da tarefa?

Lote do Azure fornece uma maneira toopersist a saída da tarefa. Olá convenções de arquivo é melhor cenários de toothese adequados:

- Você pode modificar facilmente o código Olá para o aplicativo hello se a tarefa está em execução toopersist arquivos usando biblioteca de convenções de arquivo hello.
- Você deseja toostream dados tooAzure armazenamento enquanto a tarefa Olá ainda está em execução.
- Você deseja toopersist dados pools criados com a configuração do serviço de nuvem hello ou configuração de máquina virtual de saudação.
- O aplicativo cliente ou outras tarefas no hello toolocate necessidades de trabalho e baixar arquivos de saída de tarefas por ID ou por finalidade. 
- Você deseja tooview saída da tarefa no hello portal do Azure.

Se seu cenário diferente daqueles listados acima, talvez seja necessário tooconsider uma abordagem diferente. Para obter mais informações sobre outras opções para persistir a saída da tarefa, consulte [Persist trabalhos e tarefas de saída tooAzure armazenamento](batch-task-output.md). 

## <a name="what-is-hello-batch-file-conventions-standard"></a>O que é Olá convenções do arquivo de lote padrão?

Olá [padrão de convenções de arquivo em lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) fornece um esquema de nomenclatura para contêineres de destino hello e toowhich de caminhos de blob, os arquivos de saída são gravados. Arquivos persistente tooAzure armazenamento que seguem toohello convenções de arquivo padrão são automaticamente disponíveis para visualização no hello portal do Azure. portal de Hello está ciente de convenção de nomenclatura hello e portanto pode exibir arquivos que seguem tooit.

biblioteca de convenções de arquivo Hello para .NET nomeia automaticamente seus contêineres de armazenamento e arquivos de saída de tarefa de acordo com o toohello convenções de arquivo padrão. biblioteca de convenções de arquivo Hello também fornece métodos tooquery arquivos de saída no armazenamento do Azure toojob ID, ID da tarefa ou finalidade de acordo com.   

Se você estiver desenvolvendo com um idioma diferente do .NET, você pode implementar Olá convenções de arquivo padrão por conta própria em seu aplicativo. Para obter mais informações, consulte [sobre padrão de convenções de arquivo em lotes Olá](batch-task-output.md#about-the-batch-file-conventions-standard).

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a>Vincular uma conta de armazenamento do Azure tooyour conta em lotes

dados de saída de toopersist tooAzure armazenamento usando a biblioteca de convenções de arquivo hello, primeiro você deve vincular uma conta de armazenamento do Azure tooyour conta do lote. Se você ainda não tiver feito isso, vincular uma conta de armazenamento tooyour conta em lotes usando Olá [portal do Azure](https://portal.azure.com):

1. Navegue tooyour conta de lote no hello portal do Azure. 
2. Em **Configurações**, selecione **Conta de Armazenamento**.
3. Se você ainda não tiver uma conta de Armazenamento associada à sua conta do Lote, clique em **Conta de Armazenamento (Nenhuma)**.
4. Selecione uma conta de armazenamento na lista Olá para sua assinatura. Para melhor desempenho, use uma conta de armazenamento do Azure que está em Olá mesma região Olá conta do lote onde as tarefas estão em execução.

## <a name="persist-output-data"></a>Manter os dados de saída

tarefa toopersist trabalho de saída de dados com a biblioteca de convenções de arquivo hello, criar um contêiner no armazenamento do Azure e salvar o contêiner de toohello Olá saída. Saudação de uso [biblioteca de cliente de armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage) em seu contêiner de toohello tarefa código tooupload Olá tarefa saída. 

Para obter mais informações sobre como trabalhar com contêineres e blobs no Armazenamento do Azure, consulte [Introdução ao armazenamento de Blobs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

> [!WARNING]
> Todas as saídas de trabalho e tarefa persistentes Olá convenções de arquivo de biblioteca são armazenados no mesmo contêiner de hello. Se um grande número de tarefas tente toopersist arquivos no hello mesmo tempo, [redução dos limites de armazenamento](../storage/common/storage-performance-checklist.md#blobs) pode ser imposta.
> 
> 

### <a name="create-storage-container"></a>Criar um contêiner de armazenamento

tooAzure de saída de tarefa toopersist armazenamento, primeiro crie um contêiner chamando [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync]. Esse método de extensão usa um objeto [CloudStorageAccount][net_cloudstorageaccount] como parâmetro. Ele cria um contêiner nomeado acordo toohello convenções de arquivo padrão, para que seu conteúdo é detectável pelo Olá métodos de recuperação de portal e hello Azure discutidos posteriormente no artigo de saudação.

Você normalmente colocar Olá código toocreate um contêiner em seu aplicativo cliente &mdash; Olá aplicativo que cria o pools, trabalhos e tarefas.

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a>Armazenar saídas de tarefas

Agora que você preparou um contêiner no armazenamento do Azure, tarefas podem salvar o contêiner de toohello de saída usando Olá [TaskOutputStorage] [ net_taskoutputstorage] classe encontrada na biblioteca de convenções de arquivo hello.

Em seu código de tarefa, primeiro crie um [TaskOutputStorage] [ net_taskoutputstorage] do objeto, em seguida, quando a tarefa de saudação concluiu seu trabalho, chame Olá [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] método toosave tooAzure sua saída armazenamento.

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

Olá `kind` parâmetro hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) método categoriza Olá persistente de arquivos. Há quatro tipos predefinidos de [TaskOutputKind][net_taskoutputkind]: `TaskOutput`, `TaskPreview`, `TaskLog` e `TaskIntermediate.`. Você também pode definir as categorias personalizadas da saída.

Esses tipos de saída permitem que você toospecify qual tipo de saídas toolist quando você consulta posteriormente em lotes para Olá persistentes saídas de uma determinada tarefa. Em outras palavras, quando você lista Olá saídas para uma tarefa, você pode filtrar a lista de saudação em um dos tipos de saída de hello. Por exemplo, "Envie-me Olá *visualização* de saída de tarefa *109*." Mais informações sobre a listagem e recuperando saídas aparece na [recuperar a saída](#retrieve-output) posteriormente Olá artigo.

> [!TIP]
> Olá tipo de saída também determina onde no hello Azure portal um determinado arquivo aparece: *TaskOutput*-arquivos categorizados aparecem sob **arquivos de saída de tarefa**, e *TaskLog*arquivos aparecem sob **tarefa logs**.
> 
> 

### <a name="store-job-outputs"></a>Armazenar saídas de trabalhos

Além disso gera toostoring tarefa, você pode armazenar saídas Olá associadas a um trabalho inteiro. Por exemplo, na tarefa de mesclagem de saudação de um trabalho de processamento de filme, você pode persistir filme Olá totalmente processado como uma saída de trabalho. Quando o trabalho for concluído, seu aplicativo cliente pode listar recuperar Olá saídas de trabalho hello e não precisa tooquery Olá tarefas individuais.

Armazenar a saída de trabalho por chamada hello [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] método e especifique Olá [JobOutputKind] [ net_joboutputkind] e nome de arquivo:

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

Assim como acontece com hello **TaskOutputKind** tipo para saídas de tarefa, você usar Olá [JobOutputKind] [ net_joboutputkind] tipo toocategorize um trabalho da mantidas arquivos. Esse parâmetro permite consultar toolater (lista) de um tipo específico de saída. Olá **JobOutputKind** tipo inclui as categorias de saída e visualização e oferece suporte à criação de categorias personalizadas.

### <a name="store-task-logs"></a>Armazenar logs de tarefas

Além disso toopersisting que um armazenamento de toodurable arquivo quando uma tarefa ou trabalho conclui, talvez você precise toopersist arquivos que são atualizados durante a execução de uma tarefa Olá &mdash; arquivos de log ou `stdout.txt` e `stderr.txt`, por exemplo. Para essa finalidade, biblioteca de convenções de arquivo de lote do Azure Olá fornece Olá [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] método. Com [SaveTrackedAsync][net_savetrackedasync], você pode rastrear o arquivo de tooa de atualizações no nó de saudação (em um intervalo que você especificar) e manter esses tooAzure atualizações armazenamento.

Olá trecho de código a seguir, usamos [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` no armazenamento do Azure durante a execução de saudação da tarefa de saudação a cada 15 segundos:

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

seção de comentários Olá `Code tooprocess data and produce output file(s)` é um espaço reservado para o código de saudação que normalmente executará a tarefa. Por exemplo, você pode ter código que baixa dados do Armazenamento do Azure e executa uma transformação ou um cálculo neles. parte importante Olá este trecho de código é demonstrar como você pode encapsular esse código em um `using` tooperiodically bloco atualizar um arquivo com [SaveTrackedAsync][net_savetrackedasync].

agente do nó de saudação é um programa que é executado em cada nó no pool de saudação e fornece a interface de comando e controle de saudação entre nó hello e serviço de lote de saudação. Olá `Task.Delay` chamada é necessária no final da saudação deste `using` tooensure de bloco que Olá agente nó tem tempo tooflush Olá conteúdo padrão toohello stdout.txt arquivo no nó de saudação. Sem esse atraso, é possível toomiss Olá últimos segundos de saída. Esse atraso pode não ser necessário para todos os arquivos.

> [!NOTE]
> Quando você habilita o arquivo de controle com **SaveTrackedAsync**, apenas *acrescenta* arquivo rastreado toohello são persistente tooAzure armazenamento. Use esse método somente para rastrear arquivos de log não girando ou outros arquivos que são gravados toowith acrescentar a fim de toohello operações de arquivo hello.
> 
> 

## <a name="retrieve-output-data"></a>Recuperar dados de saída

Quando você recupera a saída persistente usando Olá convenções de arquivo de lote do Azure biblioteca, você pode fazer isso de forma centralizada em tarefas e trabalho. Você pode solicitar a saudação de saída para determinada tarefa ou trabalho sem a necessidade de tooknow seu caminho no armazenamento do Azure ou o mesmo nome de arquivo. Em vez disso, você pode solicitar os arquivos de saída pela ID de tarefa ou trabalho.

Hello trecho de código a seguir itera por meio de tarefas do trabalho, imprime algumas informações sobre os arquivos de saída Olá para tarefa hello e baixa os arquivos de armazenamento.

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a>Exibir arquivos de saída no hello portal do Azure

portal do Azure Hello exibe os arquivos de saída de tarefa e logs que são persistente tooa vinculado conta de armazenamento do Azure usando Olá [padrão de convenções de arquivo em lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). Você pode implementar essas convenções em Olá um idioma de sua escolha, ou você pode usar a biblioteca de convenções de arquivo hello em seus aplicativos .NET.

exibição de saudação tooenable dos seus arquivos de saída no portal de Olá, é preciso atender Olá requisitos a seguir:

1. [Vincular uma conta de armazenamento do Azure](#requirement-linked-storage-account) tooyour conta do lote.
2. Aderir toohello predefinido convenções de nomenclatura para arquivos e contêineres de armazenamento quando a persistência de saídas. Você pode encontrar a definição de saudação essas convenções na biblioteca de convenções de arquivo hello [Leiame][github_file_conventions_readme]. Se você usar o hello [convenções de arquivo de lote do Azure] [ nuget_package] toopersist biblioteca sua saída, os arquivos são mantidos toohello convenções de arquivo padrão de acordo com.

a saída da tarefa tooview arquivos e os logs na Olá portal do Azure, navegue até a tarefa toohello cuja saída você está interessado, em seguida, clique em **arquivos de saída salvo** ou **registros salvos**. Esta imagem mostra Olá **arquivos de saída salvo** para tarefa de saudação com ID "007":

![Saídas de tarefas folha em Olá portal do Azure][2]

## <a name="code-sample"></a>Exemplo de código

Olá [PersistOutputs] [ github_persistoutputs] projeto de exemplo é uma saudação [exemplos de código do Azure Batch] [ github_samples] no GitHub. Essa solução do Visual Studio demonstra como armazenamento toodurable de saída da tarefa de toopersist de biblioteca do toouse Olá convenções de arquivo de lote do Azure. Olá toorun de exemplo, siga estas etapas:

1. Projeto aberto Olá no **Visual Studio 2015 ou mais recente**.
2. Adicionar o lote e o armazenamento **as credenciais de conta** muito**AccountSettings.settings** no projeto de Microsoft.Azure.Batch.Samples.Common hello.
3. **Criar** (mas não executam) Olá solução. Restaure todos os pacotes NuGet, se solicitado.
4. Saudação de uso do Azure tooupload portal um [pacote de aplicativo](batch-application-packages.md) para **PersistOutputsTask**. Incluir Olá `PersistOutputsTask.exe` e seus assemblies dependentes no pacote. zip de hello, ID do conjunto de aplicativo hello muito "PersistOutputsTask" e o aplicativo hello pacote versão muito "1.0".
5. **Iniciar** hello (Executar) **PersistOutputs** projeto.
6. Quando solicitadas toochoose Olá persistência tecnologia toouse para execução do exemplo hello, digite **1** toorun Olá exemplo hello convenções arquivo biblioteca toopersist a saída da tarefa. 

## <a name="next-steps"></a>Próximas etapas

### <a name="get-hello-batch-file-conventions-library-for-net"></a>Obter a biblioteca de convenções de arquivo em lotes de saudação para .NET

Olá convenções de arquivo em lotes biblioteca para .NET estão disponível no [NuGet][nuget_package]. estende a biblioteca de Olá Olá [CloudJob] [ net_cloudjob] e [CloudTask] [ net_cloudtask] classes com novos métodos. Consulte também Olá [documentação de referência](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) para a biblioteca de convenções de arquivo hello.

Olá [código-fonte] [ github_file_conventions] para Olá convenções do arquivo de biblioteca está disponível no GitHub no hello SDK do Microsoft Azure para o repositório do .NET. 

### <a name="explore-other-approaches-for-persisting-output-data"></a>Explorar outras abordagens para manter dados de saída

- Consulte [Persist trabalhos e tarefas de saída tooAzure armazenamento](batch-task-output.md) para obter uma visão geral de persistir dados de tarefa e o trabalho.
- Consulte [persistir dados de tarefa tooAzure armazenamento com a API do serviço de lote de saudação](batch-task-output-files.md) toolearn como toouse Olá API do serviço de lote toopersist dados de saída.

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "Arquivos de saída salvos e Seletores de logs salvos no portal"
[2]: ./media/batch-task-output/task-output-02.png "Saídas de tarefas folha em Olá portal do Azure"
