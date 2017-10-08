---
title: "aaaPersist trabalhos e tarefas de saída tooAzure armazenamento com hello API do serviço de lote do Azure | Microsoft Docs"
description: "Saiba como o trabalho e tarefa de lote toopersist toouse API do serviço de lote saída tooAzure armazenamento."
services: batch
author: tamram
manager: timlt
editor: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.openlocfilehash: 71b3f7c0dda2d2a9d8eb3eef83229873c70ca22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-task-data-tooazure-storage-with-hello-batch-service-api"></a>Manter os dados de tarefa tooAzure armazenamento com hello API do serviço de lote

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Começando com a versão de 2017-05-01, Olá API do serviço de lote dá suporte a tooAzure de dados persistentes saída armazenamento de tarefas e tarefas de Gerenciador de trabalho que são executados em pools de configuração de máquina virtual de saudação. Quando você adiciona uma tarefa, você pode especificar um contêiner no armazenamento do Azure como destino Olá para a saída da tarefa hello. serviço de lote Hello, em seguida, grava qualquer contêiner de toothat de dados de saída quando Olá tarefa seja concluída.

Saudação de toousing uma vantagem em lotes é de saída da tarefa serviço API toopersist que você não precisa de aplicativo hello toomodify que Olá tarefa está em execução. Em vez disso, com poucas modificações simples tooyour aplicativo cliente, você pode persistir saída da tarefa de saudação de dentro do código de saudação que cria a tarefa de saudação.   

## <a name="when-do-i-use-hello-batch-service-api-toopersist-task-output"></a>Quando usar a saída da tarefa toopersist Olá API do serviço de lote?

Lote do Azure fornece uma maneira toopersist a saída da tarefa. Usando a API do serviço de lote de saudação é uma abordagem conveniente que é melhor cenários de toothese adequada:

- Você deseja saída da tarefa toopersist toowrite código de dentro de seu aplicativo cliente, sem modificar o aplicativo hello que a tarefa está em execução.
- Você deseja toopersist saída das tarefas de lote e o Gerenciador de tarefas em pools criados com a configuração de máquina virtual de saudação.
- Deseja que o contêiner de armazenamento do Azure de tooan toopersist saída com um nome arbitrário.
- Você deseja que o contêiner de armazenamento do Azure toopersist saída tooan chamado acordo toohello [padrão de convenções de arquivo em lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

Se seu cenário diferente daqueles listados acima, talvez seja necessário tooconsider uma abordagem diferente. Por exemplo, API de serviço de lote de saudação não atualmente suporte a streaming saída tooAzure armazenamento enquanto Olá tarefa está em execução. toostream de saída, considere o uso de biblioteca de convenções de arquivo em lotes hello, disponível para .NET. Para outros idiomas, você precisará tooimplement sua própria solução. Para obter mais informações sobre outras opções para persistir a saída da tarefa, consulte [Persist trabalhos e tarefas de saída tooAzure armazenamento](batch-task-output.md). 

## <a name="create-a-container-in-azure-storage"></a>Criar um contêiner no Armazenamento do Azure

saída da tarefa de toopersist tooAzure armazenamento, você precisará toocreate um contêiner que serve como o destino de saudação para os arquivos de saída. Crie contêiner de saudação antes de executar a tarefa, preferencialmente antes de enviar seu trabalho. contêiner de saudação toocreate, biblioteca de cliente de armazenamento do Azure apropriada do uso hello ou SDK. Para obter mais informações sobre as APIs de armazenamento do Azure, consulte Olá [documentação de armazenamento do Azure](https://docs.microsoft.com/azure/storage/).

Por exemplo, se você estiver escrevendo seu aplicativo em c#, use Olá [biblioteca de cliente de armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). Olá mostrado no exemplo a seguir como um contêiner de toocreate:

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-hello-container"></a>Obter uma assinatura de acesso compartilhado para o contêiner de saudação

Depois de criar o contêiner de hello, obtenha uma assinatura de acesso compartilhado (SAS) com acesso de gravação toohello contêiner. Uma SAS fornece um contêiner de toohello acesso delegado. Olá SAS concede acesso com um conjunto especificado de permissões e em um intervalo de tempo especificado. Olá serviço de lote precisa de uma SAS com contêiner de toohello da saída de tarefa gravação permissões toowrite. Para saber mais sobre SAS, confira [Uso de assinaturas de acesso compartilhado \(SAS\) no Armazenamento do Azure](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

Quando você receber uma SAS usando Olá APIs de armazenamento do Azure, Olá API retorna uma cadeia de caracteres de token SAS. Essa cadeia de caracteres de token inclui todos os parâmetros de saudação SAS, incluindo permissões hello e intervalo de saudação sobre quais Olá SAS é válido. toouse Olá SAS tooaccess um contêiner no armazenamento do Azure, você precisa tooappend Olá SAS caracteres token toohello URI do recurso. Olá URI recurso, junto com hello acrescentado token SAS, fornece acesso autenticado tooAzure armazenamento.

Olá exemplo a seguir mostra como cadeia de caracteres para o contêiner de saudação do token tooget um SAS somente gravação e acrescenta Olá SAS toohello URI do contêiner:

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a>Especificar arquivos de saída para a saída da tarefa

toospecify arquivos de saída para uma tarefa, criar uma coleção de [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) objetos e atribuí-la toohello [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) propriedade ao criar tarefa hello. 

exemplo de código a seguir .NET Hello cria uma tarefa que grava o arquivo de tooa de números aleatórios chamado `output.txt`. exemplo Hello cria um arquivo de saída para `output.txt` toobe gravado toohello contêiner. exemplo Hello também cria arquivos de saída para os arquivos de log que corresponde ao padrão de arquivo hello `std*.txt` (_, por exemplo,_, `stdout.txt` e `stderr.txt`). URL do contêiner Olá requer Olá SAS que foi criado anteriormente para o contêiner de saudação. Olá serviço de lote usa o contêiner de toohello do hello SAS tooauthenticate acesso: 

```csharp
new CloudTask(taskId, "cmd /v:ON /c \"echo off && set && (FOR /L %i IN (1,1,100000) DO (ECHO !RANDOM!)) > output.txt\"")
{
    OutputFiles = new List<OutputFile>
    {
        new OutputFile(
            filePattern: @"..\std*.txt",
            destination: new OutputFileDestination(
         new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId)),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
        new OutputFile(
            filePattern: @"output.txt",
            destination: 
         new OutputFileDestination(new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId + @"\output.txt")),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
}
```

### <a name="specify-a-file-pattern-for-matching"></a>Especifique um padrão de arquivo para correspondência

Quando você especificar um arquivo de saída, você pode usar o hello [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) propriedade toospecify um padrão de arquivo para correspondência. padrão de arquivo Hello pode corresponder a zero arquivos, um único arquivo ou um conjunto de arquivos que são criados pela tarefa de saudação.

Olá **FilePattern** propriedade oferece suporte a caracteres curinga do sistema de arquivos padrão como `*` (para não-recursivo corresponde) e `**` (para corresponde recursivo). Por exemplo, o exemplo de código hello acima Especifica Olá arquivo padrão toomatch `std*.txt` não recursiva: 

`filePattern: @"..\std*.txt"`

tooupload um único arquivo, especifique um padrão de arquivo sem curingas. Por exemplo, o exemplo de código hello acima Especifica Olá arquivo padrão toomatch `output.txt`:

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a>Especificar uma condição de upload

Olá [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) propriedade permite o carregamento condicional de arquivos de saída. Um cenário comum é tooupload um conjunto de arquivos se Olá tarefa tiver êxito e um conjunto diferente de arquivos se ele falhar. Por exemplo, talvez você queira arquivos de log detalhados tooupload somente quando a tarefa de saudação falhará e será encerrado com um código de saída diferente de zero. Da mesma forma, talvez você queira arquivos de resultado tooupload somente se a tarefa de saudação tiver êxito, como esses arquivos podem estar ausentes ou incompletos se Olá tarefa falhar.

exemplo de código acima Hello define Olá **UploadCondition** propriedade muito**TaskCompletion**. Essa configuração especifica que se o arquivo hello está toobe carregado após a conclusão de tarefas hello, independentemente do valor de saudação do código de saída de hello. 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

Para outras configurações, consulte Olá [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) enum.

### <a name="disambiguate-files-with-hello-same-name"></a>Desfazer a ambiguidade de arquivos com hello mesmo nome

tarefas de saudação em um trabalho podem produzir arquivos que têm Olá mesmo nome. Por exemplo, `stdout.txt` e `stderr.txt` são criados para cada tarefa que executa em um trabalho. Como cada tarefa é executada em seu próprio contexto, esses arquivos não estão em conflito no sistema de arquivos do nó hello. No entanto, quando você carrega arquivos de contêiner compartilhadas do várias tarefas tooa, você precisará toodisambiguate arquivos com hello mesmo nome.

Olá [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) propriedade especifica o blob de destino hello ou diretório virtual para arquivos de saída. Você pode usar o hello **caminho** blob de saudação do tooname de propriedade ou o diretório virtual de forma que arquivos de saída com hello mesmo nome são nomeadas exclusivamente no armazenamento do Azure. Usando a ID da tarefa Olá no caminho de saudação é uma boa maneira tooensure os nomes exclusivos e identificar facilmente os arquivos.

Se hello **FilePattern** propriedade é definida tooa expressão de caractere curinga, todos os arquivos que correspondem a saudação padrão são o diretório virtual toohello carregado, especificado pelo Olá **caminho** propriedade. Por exemplo, se hello contêiner é `mycontainer`, tarefa Olá ID é `mytask`, e é o padrão do arquivo hello `..\std*.txt`, então Olá absoluto URIs toohello arquivos de saída no armazenamento do Azure será semelhantes a:

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

Se hello **FilePattern** é toomatch de conjunto de um único nome de arquivo, em seguida, o que significa que ele não contém caracteres curinga, Olá valor Olá **caminho** propriedade especifica o nome de blob totalmente qualificado de saudação . Se você antecipar conflitos de nomes com um único arquivo de várias tarefas, em seguida, inclua nome de saudação do diretório virtual hello como parte do toodisambiguate de nome de arquivo hello esses arquivos. Por exemplo, o conjunto Olá **caminho** ID da tarefa propriedade tooinclude hello, caractere delimitador de saudação (normalmente uma barra invertida) e o nome de arquivo hello:

`path: taskId + @"/output.txt"`

Olá absoluto URIs toohello arquivos de saída para um conjunto de tarefas será semelhantes a:

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

Para obter mais informações sobre diretórios virtuais no armazenamento do Azure, consulte [lista Olá blobs em um contêiner](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).


## <a name="diagnose-file-upload-errors"></a>Diagnosticar erros de carregamento de arquivo

Se carregar saída arquivos tooAzure armazenamento falhar, tarefa Olá move toohello **concluído** estado e hello [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) está definida. Examine Olá **FailureInformation** toodetermine de propriedade, o erro. Por exemplo, aqui está um erro que ocorre no carregamento do arquivo se Olá contêiner não pode ser encontrado: 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of hello specified Azure container(s) was not found while attempting tooupload an output file
```

Em cada carregamento de arquivo em lote grava dois nós de computação de toohello de arquivos, de log `fileuploadout.txt` e `fileuploaderr.txt`. Você pode examinar esses toolearn de arquivos de log mais sobre uma falha específica. Em casos onde Olá arquivo nunca tentativa de upload, por exemplo, porque não foi possível executar a própria tarefa hello, em seguida, esses arquivos de log não existirá.

## <a name="diagnose-file-upload-performance"></a>Diagnosticar desempenho de carregamento de arquivo

Olá `fileuploadout.txt` arquivo registra em log o progresso de carregamento. Você pode examinar este toolearn de arquivo mais sobre o quanto o arquivo carrega estão demorando. Tenha em mente que há muitos fatores desempenho tooupload, incluindo o tamanho de saudação do nó hello, outra atividade no nó de saudação em tempo de saudação do carregamento de hello, se o contêiner de destino hello está em Olá mesma região que o pool do lote hello, quantos nós são Carregando a conta de armazenamento toohello em Olá ao mesmo tempo e assim por diante.

## <a name="use-hello-batch-service-api-with-hello-batch-file-conventions-standard"></a>Usar a API do serviço de lote de saudação com hello convenções padrão de arquivo de lote

Quando você mantiver a saída da tarefa com hello API do serviço de lote, você pode nomear o contêiner de destino e você quiser os blobs. Você também pode escolher tooname-los de acordo com toohello [padrão de convenções de arquivo em lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). padrão de convenções de arquivo Hello determina os nomes de saudação do contêiner de destino de saudação e blob no armazenamento do Azure para um arquivo de saída determinada com base nos nomes de saudação do hello trabalhos e tarefas. Se você usar Olá convenções de arquivo padrão de nomeação de arquivos de saída, os arquivos de saída estão disponíveis para exibição no hello [portal do Azure](https://portal.azure.com).

Se você estiver desenvolvendo em c#, você pode usar métodos de saudação incorporados Olá [biblioteca convenções de arquivo em lotes para .NET](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files). Essa biblioteca cria Olá chamados corretamente contêineres e caminhos de blob para você. Por exemplo, você pode chamar o nome correto do hello API tooget Olá para contêiner hello, com base no nome do trabalho hello:

```csharp
string containerName = job.OutputStorageContainerName();
```

Você pode usar o hello [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) método tooreturn uma URL de SAS (assinatura) de acesso compartilhado que é usado toowrite toohello contêiner. Você pode passar esse SAS toohello [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) construtor.

Se você estiver desenvolvendo em um idioma diferente do c#, você precisará padrão de convenções de arquivo hello tooimplement por conta própria.

## <a name="code-sample"></a>Exemplo de código

Olá [PersistOutputs] [ github_persistoutputs] projeto de exemplo é uma saudação [exemplos de código do Azure Batch] [ github_samples] no GitHub. Essa solução do Visual Studio demonstra como a biblioteca de cliente de lote toouse Olá para tarefas do .NET toopersist saída toodurable armazenamento. Olá toorun de exemplo, siga estas etapas:

1. Projeto aberto Olá no **Visual Studio 2015 ou mais recente**.
2. Adicionar o lote e o armazenamento **as credenciais de conta** muito**AccountSettings.settings** no projeto de Microsoft.Azure.Batch.Samples.Common hello.
3. **Criar** (mas não executam) Olá solução. Restaure todos os pacotes NuGet, se solicitado.
4. Saudação de uso do Azure tooupload portal um [pacote de aplicativo](batch-application-packages.md) para **PersistOutputsTask**. Incluir Olá `PersistOutputsTask.exe` e seus assemblies dependentes no pacote. zip de hello, ID do conjunto de aplicativo hello muito "PersistOutputsTask" e o aplicativo hello pacote versão muito "1.0".
5. **Iniciar** hello (Executar) **PersistOutputs** projeto.
6. Quando solicitadas toochoose Olá persistência tecnologia toouse para execução do exemplo hello, digite **2** exemplo hello de toorun usando a saída da tarefa toopersist Olá API do serviço de lote.
7. Se desejar, execute exemplo hello novamente, inserindo **3** toopersist saída com hello API do serviço de lote e também tooname Olá contêiner e blob de caminho de destino de acordo com o toohello convenções de arquivo padrão.

## <a name="next-steps"></a>Próximas etapas

- Para obter mais informações sobre a saída da tarefa persistentes com biblioteca de convenções de arquivo hello para .NET, consulte [Manter trabalhos e tarefas tooAzure de dados armazenamento com biblioteca de convenções de arquivo em lotes Olá para .NET toopersist ](batch-task-output-file-conventions.md).
- Para obter informações sobre outras abordagens para persistir dados de saída em lote do Azure, consulte [Persist trabalhos e tarefas de saída tooAzure armazenamento](batch-task-output.md).

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
