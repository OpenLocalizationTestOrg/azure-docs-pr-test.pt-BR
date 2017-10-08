---
title: "aaaTutorial - biblioteca de cliente do uso Olá lote do Azure para .NET | Microsoft Docs"
description: "Aprenda os conceitos básicos de saudação do lote do Azure e criar uma solução simple usando o .NET."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a>Começar a criar soluções com biblioteca de cliente Olá Batch para .NET

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Aprenda noções básicas de saudação do [do Azure Batch] [ azure_batch] e hello [Batch .NET] [ net_api] biblioteca neste artigo discutir um c# exemplo aplicativo passo etapa. Vamos examinar como o aplicativo de exemplo hello aproveita tooprocess de serviço de lote Olá uma carga de trabalho paralela em nuvem hello e como ele interage com [armazenamento do Azure](../storage/common/storage-introduction.md) para preparação de arquivo e de recuperação. Você vai aprender um fluxo de trabalho de aplicativo comuns em lotes e obter uma compreensão básica de Olá principais componentes do lote, como trabalhos, tarefas, pools de e nós de computação.

![Fluxo de trabalho da solução do Lote (básico)][11]<br/>

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você tenha um conhecimento prático do C# e do Visual Studio. Ele também pressupõe que você é capaz de toosatisfy Olá conta criação requisitos especificados abaixo para o Azure e Olá lote e serviços de armazenamento.

### <a name="accounts"></a>Contas
* **Conta do Azure**: se você ainda não tiver uma assinatura do Azure, [crie uma conta gratuita do Azure][azure_free_account].
* **Conta do Lote**: quando você tiver uma assinatura do Azure, [crie uma conta do Lote do Azure](batch-account-create-portal.md).
* **Conta de armazenamento**: veja [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) em [Sobre as contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).

> [!IMPORTANT]
> Em lotes atualmente oferece suporte a *somente* Olá **geral** tipo de conta de armazenamento, conforme descrito na etapa &#5; [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) no [sobre o Azure contas de armazenamento](../storage/common/storage-create-storage-account.md).
>
>

### <a name="visual-studio"></a>Visual Studio
Você deve ter **Visual Studio 2015 ou mais recente** projeto de exemplo hello toobuild. Você pode encontrar versões de avaliação e gratuitas do Visual Studio no hello [visão geral dos produtos do Visual Studio][visual_studio].

### <a name="dotnettutorial-code-sample"></a>*DotNetTutorial* 
Olá [DotNetTutorial] [ github_dotnettutorial] exemplo é uma saudação muitos exemplos de código do lote encontrados no hello [exemplos de lote do azure] [ github_samples] repositório no GitHub. Você pode baixar todos os exemplos de saudação clicando **Clone ou download > baixar ZIP** na home page do repositório de hello, ou clicando em Olá [azure lote-exemplos master.zip] [ github_samples_zip]link de download direto. Depois de extrair o conteúdo de saudação do arquivo ZIP de Olá, você pode encontrar solução Olá Olá pasta a seguir:

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a>Gerenciador do Lote do Azure (opcional)
Olá [Gerenciador de lote do Azure] [ github_batchexplorer] é um utilitário livre que está incluído no hello [exemplos de lote do azure] [ github_samples] repositório no GitHub. Ao toocomplete não é necessária neste tutorial, ele pode ser útil ao desenvolvimento e depuração de suas soluções de lote.

## <a name="dotnettutorial-sample-project-overview"></a>Visão geral do projeto de exemplo DotNetTutorial
Olá *DotNetTutorial* código de exemplo é uma solução do Visual Studio que consiste em dois projetos: **DotNetTutorial** e **TaskApplication**.

* **DotNetTutorial** é o aplicativo cliente hello que interage com tooexecute de serviços de lote e armazenamento Olá uma carga de trabalho paralela em nós de computação (máquinas virtuais). O DotNetTutorial é executado em sua estação de trabalho local.
* **TaskApplication** é Olá programa que é executado em nós de computação no trabalho do Azure tooperform Olá real. No exemplo hello, `TaskApplication.exe` analisa Olá texto em um arquivo baixado do armazenamento do Azure (arquivo de entrada hello). Em seguida, ele produz um arquivo de texto (arquivo de saída de hello) que contém uma lista de palavras de três principais Olá que aparecem no arquivo de entrada hello. Depois que ele cria o arquivo de saída de hello, TaskApplication carrega Olá arquivo tooAzure armazenamento. Isso torna aplicativo de cliente toohello disponível para download. TaskApplication é executado em paralelo em vários nós de computação Olá serviço de lote.

Olá, diagrama a seguir ilustra operações principais de saudação que são executadas pelo aplicativo de cliente hello, *DotNetTutorial*e o aplicativo hello executado pelas tarefas de saudação *TaskApplication*. Esse fluxo de trabalho básico é típico de muitas soluções de computação criadas com o Lote. Embora não demonstra todos os recursos disponíveis no serviço de lote de hello, quase todos os cenários de lote incluem partes desse fluxo de trabalho.

![Fluxo de trabalho de exemplo do Lote][8]<br/>

[**Etapa 1.**](#step-1-create-storage-containers) Crie **contêineres** no Armazenamento de Blobs do Azure.<br/>
[**Etapa 2.**](#step-2-upload-task-application-and-data-files) Arquivos de aplicativo de tarefa de carregamento e toocontainers de arquivos de entrada.<br/>
[**Etapa 3.**](#step-3-create-batch-pool) Criar um **pool** do Lote.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Olá pool **StartTask** downloads Olá tarefa arquivos binários (TaskApplication) toonodes ao entrarem pool hello.<br/>
[**Etapa 4.**](#step-4-create-batch-job) Crie um **trabalho** do Lote.<br/>
[**Etapa 5.**](#step-5-add-tasks-to-job) Adicionar **tarefas** toohello trabalho.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** tarefas de saudação são agendado tooexecute em nós.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Cada tarefa baixa seus dados de entrada do Armazenamento do Azure e então inicia a execução.<br/>
[**Etapa 6.**](#step-6-monitor-tasks) Monitore as tarefas.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Como as tarefas são concluídas, carregar seu dados de saída tooAzure armazenamento.<br/>
[**Etapa 7.**](#step-7-download-task-output) Baixe a saída da tarefa do Armazenamento.

Conforme mencionado, não todas as soluções em lotes executa essas etapas e podem incluir muitas, mas Olá *DotNetTutorial* aplicativo de exemplo demonstra processos comuns encontrados em uma solução de lote.

## <a name="build-hello-dotnettutorial-sample-project"></a>Criar hello *DotNetTutorial* projeto de exemplo
Antes de executar com êxito exemplo hello, você deve especificar credenciais de conta de armazenamento e de lote no hello *DotNetTutorial* do projeto `Program.cs` arquivo. Se você não tiver feito isso, abra a solução Olá no Visual Studio clicando duas vezes Olá `DotNetTutorial.sln` arquivo de solução. Ou abri-lo de dentro do Visual Studio usando Olá **arquivo > Abrir > projeto/solução** menu.

Abra `Program.cs` em Olá *DotNetTutorial* projeto. Adicione as credenciais conforme especificado superior de saudação do arquivo hello:

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> Conforme mencionado acima, você deve especificar atualmente credenciais Olá para um **geral** conta de armazenamento no armazenamento do Azure. Seus aplicativos de lote usam armazenamento de blob em Olá **geral** conta de armazenamento. Não especifique credenciais Olá para uma conta de armazenamento que foi criado selecionando Olá *armazenamento de Blob* tipo de conta.
>
>

Você pode encontrar suas credenciais de conta de lote e armazenamento na folha da conta de saudação de cada serviço em Olá [portal do Azure][azure_portal]:

![As credenciais no portal de saudação do lote][9]
![credenciais de armazenamento no portal de saudação][10]<br/>

Agora que você atualizou o projeto Olá com suas credenciais, clique com botão direito solução Olá no Gerenciador de soluções e clique em **compilar solução**. Confirme restauração de saudação de todos os pacotes NuGet, se você for solicitado.

> [!TIP]
> Se os pacotes do NuGet Olá não são restaurados automaticamente ou se você encontrar erros sobre os pacotes de saudação de toorestore uma falha, certifique-se de que você tenha Olá [NuGet Package Manager] [ nuget_packagemgr] instalado. Em seguida, habilite Olá de download de pacotes ausentes. Consulte [habilitar pacote restaurar durante a compilação] [ nuget_restore] tooenable download do pacote.
>
>

Olá seções a seguir, é dividir o aplicativo de exemplo hello em etapas de saudação que ela seja executada tooprocess uma carga de trabalho no serviço de lote de saudação e discutem em detalhes essas etapas. Recomendamos que você toorefer toohello abrir solução no Visual Studio enquanto você trabalha até rest Olá deste artigo, pois nem toda linha de código no exemplo hello é discutida.

Navegue toohello superior de saudação `MainAsync` método hello *DotNetTutorial* do projeto `Program.cs` arquivo toostart com a etapa 1. Cada etapa abaixo e aproximadamente chamadas de maneira Olá progressão de método em `MainAsync`.

## <a name="step-1-create-storage-containers"></a>Etapa 1: Criar contêineres do Armazenamento
![Criar contêineres no Armazenamento do Azure][1]
<br/>

O Lote inclui suporte interno para a interação com o Armazenamento do Azure. Contêineres em sua conta de armazenamento fornecerá arquivos Olá necessários para tarefas de saudação que são executados em sua conta do lote. contêineres de saudação também fornecem um lugar toostore Olá dados da saída tarefas Olá produzem. primeiro Olá Olá *DotNetTutorial* aplicativo cliente é criar três contêineres [armazenamento de BLOBs do Azure](../storage/common/storage-introduction.md):

* **aplicativo**: este contêiner armazena aplicativo hello executando tarefas hello, bem como qualquer uma de suas dependências, como DLLs.
* **entrada**: tarefas baixarão tooprocess de arquivos de dados de saudação do hello *entrada* contêiner.
* **saída**: quando tarefas concluir o processamento do arquivo de entrada, eles carregará Olá resultados toohello *saída* contêiner.

Em ordem toointeract com um armazenamento de conta e criar contêineres, usamos Olá [biblioteca de cliente de armazenamento do Azure para .NET][net_api_storage]. Podemos criar uma conta de toohello de referência com [CloudStorageAccount][net_cloudstorageaccount]e do que criar um [CloudBlobClient][net_cloudblobclient]:

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

Usamos Olá `blobClient` referência em todo o aplicativo hello e passá-lo como um parâmetro tooseveral métodos. É um exemplo no bloco de código Olá que segue imediatamente Olá acima, onde podemos chamar `CreateContainerIfNotExistAsync` tooactually criar contêineres de saudação.

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

Depois que criar contêineres de hello, aplicativo hello agora pode carregar arquivos de saudação que serão usados pelas tarefas de saudação.

> [!TIP]
> [Como toouse armazenamento de BLOBs no .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) fornece uma boa visão geral de como trabalhar com contêineres de armazenamento do Azure e blobs. Como começar a trabalhar com o lote, ele deve ser superior Olá da sua lista de leitura.
>
>

## <a name="step-2-upload-task-application-and-data-files"></a>Etapa 2: carregar aplicativos e de tarefa e arquivos de dados 
![Toocontainers de arquivos de tarefa de carregamento de aplicativo e de entrada (dados)][2]
<br/>

Operação, de carregamento no arquivo hello *DotNetTutorial* primeiro define coleções de **aplicativo** e **entrada** caminhos de arquivo que existem no computador local hello. Em seguida, ele carrega esses contêineres de toohello de arquivos que você criou na etapa anterior hello.

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

Há dois métodos em `Program.cs` que estão envolvidos no processo de carregamento de saudação:

* `UploadFilesToContainerAsync`: Esse método retorna uma coleção de [ResourceFile] [ net_resourcefile] objetos (abordados abaixo) e internamente chamadas `UploadFileToContainerAsync` tooupload cada arquivo que é passado Olá *filePaths* parâmetro.
* `UploadFileToContainerAsync`: Este é o método hello que realmente executa o carregamento do arquivo hello e cria Olá [ResourceFile] [ net_resourcefile] objetos. Depois de carregar o arquivo hello, ele obtém uma assinatura de acesso compartilhado (SAS) para o arquivo hello e retorna um objeto de ResourceFile que o representa. As assinaturas de acesso compartilhado também são discutidas abaixo.

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a>ResourceFiles
Um [ResourceFile] [ net_resourcefile] fornece tarefas em lote com o arquivo de tooa URL Olá no armazenamento do Azure que é baixado tooa nó de computação para que essa tarefa seja executada. Olá [ResourceFile.BlobSource] [ net_resourcefile_blobsource] propriedade especifica a URL completa do arquivo Olá Olá conforme ela existe no armazenamento do Azure. Olá URL também pode incluir uma assinatura de acesso compartilhado (SAS) que fornece acesso seguro toohello arquivo. A maioria dos tipos de tarefas no .NET do Lote inclui uma propriedade *ResourceFiles* , incluindo:

* [CloudTask][net_task]
* [StartTask][net_pool_starttask]
* [JobPreparationTask][net_jobpreptask]
* [JobReleaseTask][net_jobreltask]

Olá DotNetTutorial aplicativo de exemplo não usa Olá JobPreparationTask ou tipos de tarefa JobReleaseTask, mas você pode ler mais sobre eles em [nós de computação de tarefas de preparação e conclusão de trabalho de execução em lote do Azure](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Assinatura de acesso compartilhado (SAS)
Acesso compartilhado, as assinaturas são cadeias de caracteres que, quando incluído como parte de uma URL — forneça acesso seguro toocontainers e blobs no armazenamento do Azure. Olá DotNetTutorial aplicativo usa ambos os BLOBs e contêiner compartilhadas URLs de assinatura de acesso e demonstra como tooobtain esses compartilhado acessar cadeias de caracteres de assinatura de saudação serviço de armazenamento.

* **Assinaturas de acesso compartilhado de blob**: StartTask do pool de saudação em DotNetTutorial usa assinaturas de acesso compartilhado de blob ao baixar arquivos de dados de entrada e binários do aplicativo hello do armazenamento (consulte a etapa 3 abaixo). Olá `UploadFileToContainerAsync` do DotNetTutorial método `Program.cs` contém código Olá que obtém a assinatura de acesso compartilhado de cada blob. Isso é feito chamando [CloudBlob.GetSharedAccessSignature][net_sas_blob].
* **Assinaturas de acesso compartilhado do contêiner**: como cada tarefa termina o trabalho no nó de computação hello, ele carrega sua toohello do arquivo de saída *saída* contêiner no armazenamento do Azure. toodo assim, TaskApplication usa uma assinatura de acesso compartilhado do contêiner que fornece acesso de gravação toohello contêiner como parte do caminho de saudação quando ele carrega o arquivo hello. Obter assinatura de acesso compartilhado do contêiner Olá é feita de maneira semelhante, como quando o blob de saudação obter assinatura de acesso compartilhado. DotNetTutorial, você encontrará esse Olá `GetContainerSasUrl` chamadas de método auxiliar [GetSharedAccessSignature] [ net_sas_container] toodo para. Você poderá ler mais sobre como TaskApplication usa o contêiner de saudação compartilhado assinatura de acesso na "etapa 6: monitorar tarefas."

> [!TIP]
> Check-out da série de duas partes da saudação em assinaturas de acesso compartilhado, [parte 1: Olá Noções básicas sobre compartilhado modelo de assinatura (SAS) de acesso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) e [parte 2: criar e usar uma assinatura de acesso compartilhado (SAS) com o armazenamento de Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn mais sobre como fornecer acesso seguro toodata na sua conta de armazenamento.
>
>

## <a name="step-3-create-batch-pool"></a>Etapa 3: Criar pool do Lote
![Criar um pool do Lote][3]
<br/>

Um **pool** do Lote é uma coleção de nós de computação (máquinas virtuais) nos quais o Lote executa as tarefas de um trabalho.

Depois de carregar o aplicativo hello e arquivos de dados toohello conta de armazenamento com APIs de armazenamento do Azure, *DotNetTutorial* começa a fazer chamadas toohello o serviço de lote com APIs fornecidas pela biblioteca de saudação do .NET em lotes. Olá código cria primeiro um [BatchClient][net_batchclient]:

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

Em seguida, exemplo hello cria um conjunto de nós de computação na conta do lote Olá com uma chamada muito`CreatePoolIfNotExistsAsync`. `CreatePoolIfNotExistsAsync`Olá usa [BatchClient.PoolOperations.CreatePool] [ net_pool_create] método toocreate um novo pool de saudação serviço de lote:

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

Quando você cria um pool com [CreatePool][net_pool_create], você especificar vários parâmetros, como número de saudação de nós de computação, hello [tamanho de nós Olá](../cloud-services/cloud-services-sizes-specs.md), e Olá operacional de nós sistema. Em *DotNetTutorial*, usamos [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 de [serviços de nuvem](../cloud-services/cloud-services-guestos-update-matrix.md). 

Você também pode criar pools de nós de computação que são máquinas virtuais (VMs) Azure especificando Olá [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] para o pool. Você pode criar um conjunto de nós de computação de VM de [imagens Linux](batch-linux-nodes.md) ou Windows. fonte de saudação para as imagens VM pode ser:

- Olá [Marketplace de máquinas virtuais do Azure][vm_marketplace], que fornece imagens do Windows e Linux que estão prontos para uso. 
- Uma imagem personalizada preparada e fornecida por você. Para obter mais detalhes sobre imagens personalizadas, confira [Desenvolver soluções de computação paralela em grande escala com o Lote](batch-api-basics.md#pool).

> [!IMPORTANT]
> Você é cobrado pelos recursos de computação no Lote. toominimize custos, você pode reduzir `targetDedicatedComputeNodes` too1 antes de executar o exemplo hello.
>
>

Com essas propriedades de nó físico, você também pode especificar um [StartTask] [ net_pool_starttask] para pool de saudação. Olá StartTask executa em cada nó como nó une pool Olá, e cada vez que um nó é reiniciado. Olá StartTask é especialmente útil para instalar aplicativos em execução de toohello anterior de nós de computação de tarefas. Por exemplo, se suas tarefas de processam os dados por meio de scripts de Python, você poderá usar um tooinstall StartTask Python em nós de computação hello.

Neste aplicativo de exemplo, Olá StartTask copia arquivos de saudação que baixa de armazenamento (que são especificados usando Olá [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] propriedade) do diretório compartilhado do toohello de diretório de trabalho do hello StartTask que *todos os* tarefas em execução no nó Olá podem acessar. Essencialmente, isso copia `TaskApplication.exe` e sua dependências toohello diretório compartilhado em cada nó como nó Olá une pool hello, para que as tarefas que são executados no nó Olá podem acessá-lo.

> [!TIP]
> Olá **pacotes de aplicativos** recurso de lote do Azure fornece tooget de outra maneira seu aplicativo em nós de computação de saudação em um pool. Consulte [implantar aplicativos toocompute nós com pacotes de aplicativos de lote](batch-application-packages.md) para obter detalhes.
>
>

Também notável no trecho de código Olá acima é use Olá das duas variáveis de ambiente no hello *CommandLine* propriedade Olá StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` e `%AZ_BATCH_NODE_SHARED_DIR%`. Cada nó de computação em um pool de lote é automaticamente configurado com diversas variáveis de ambiente que são tooBatch específico. Qualquer processo que é executado por uma tarefa tem acesso toothese as variáveis de ambiente.

> [!TIP]
> toofind mais informações sobre variáveis de ambiente Olá que estão disponíveis em nós de computação em um pool de lote e obter informações sobre pastas de trabalho de tarefas, consulte Olá [configurações de ambiente para tarefas](batch-api-basics.md#environment-settings-for-tasks) e [arquivos e diretórios ](batch-api-basics.md#files-and-directories) seções Olá [visão geral do recurso de lote para desenvolvedores](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Etapa 4: Criar o trabalho do Lote
![Criar trabalho do Lote][4]<br/>

Um **trabalho** do Lote é uma coleção de tarefas associadas a um pool de nós de computação. tarefas de saudação em um trabalho executar em nós de computação do pool Olá associado.

Você pode usar um trabalho, não apenas para a organização e controle de tarefas em cargas de trabalho relacionadas, mas também para impor certas restrições – como Olá tempo de execução máximo para o trabalho de saudação (e, por extensão, suas tarefas), bem como a prioridade do trabalho em trabalhos de tooother de relação no lote de saudação conta. No entanto, neste exemplo, o trabalho de saudação é associado apenas ao pool de saudação que foi criado na etapa &#3;. Nenhuma propriedade adicional será configurada.

Todos os trabalhos do Lotes estão associados a um pool específico. Essa associação indica quais nós tarefas saudação do trabalho serão executado em. Você pode especificar isso usando Olá [CloudJob.PoolInformation] [ net_job_poolinfo] propriedade, conforme mostrado no trecho de código Olá abaixo.

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

Agora que um trabalho tiver sido criado, as tarefas são adicionadas tooperform trabalho de saudação.

## <a name="step-5-add-tasks-toojob"></a>Etapa 5: Adicionar tarefas toojob
![Adicionar tarefas toojob][5]<br/>
*(1) as tarefas são adicionadas toohello trabalho, tarefas de saudação (2) são agendado toorun em nós e tarefas de saudação (3) Baixar Olá tooprocess de arquivos de dados*

Lote **tarefas** são nós de computação Olá unidades individuais de trabalho que executam em hello. Uma tarefa tem uma linha de comando e executa os scripts de saudação ou executáveis que você especificar na linha de comando.

tooactually executar o trabalho, tarefas devem ser adicionadas tooa trabalho. Cada [CloudTask] [ net_task] é configurada por meio de uma propriedade de linha de comando e [ResourceFiles] [ net_task_resourcefiles] (assim como acontece com StartTask do pool Olá) que tarefa Olá baixa toohello nó antes de sua linha de comando é executada automaticamente. Em Olá *DotNetTutorial* projeto de exemplo, cada tarefa processa apenas um arquivo. Portanto, sua coleção ResourceFiles contém um único elemento.

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> Quando eles acessar variáveis de ambiente, como `%AZ_BATCH_NODE_SHARED_DIR%` ou executar um aplicativo não encontrado no nó de saudação `PATH`, linhas de comando de tarefa devem ser prefixadas com `cmd /c`. Isso explicitamente executar o interpretador de comandos hello e instruí-la tooterminate depois de executar o comando. Esse requisito é desnecessário se suas tarefas de executar um aplicativo no nó de saudação `PATH` (como *robocopy.exe* ou *powershell.exe*) e nenhuma variável de ambiente é usados.
>
>

Dentro de saudação `foreach` loop no trecho de código Olá acima, você pode ver que linha de comando Olá para tarefa de saudação é construída, de modo que três argumentos de linha de comando são passados muito*TaskApplication.exe*:

1. Olá **primeiro argumento** é o caminho de saudação de tooprocess de arquivo hello. Este é o arquivo de toohello de caminho local do hello existente no nó de saudação. Olá quando o objeto ResourceFile no `UploadFileToContainerAsync` foi criado acima, o nome do arquivo hello foi usado para esta propriedade (como um construtor de ResourceFile do parâmetro toohello). Isso indica que esse arquivo hello pode ser encontrado no hello mesmo diretório como *TaskApplication.exe*.
2. Olá **segundo argumento** Especifica que superior Olá *N* palavras devem ser escritas toohello arquivo de saída. No exemplo hello, isso é embutido para que as palavras de três principais Olá são gravadas toohello arquivo de saída.
3. Olá **terceiro argumento** é a assinatura de acesso compartilhado da saudação (SAS) que fornece acesso de gravação toohello **saída** contêiner no armazenamento do Azure. *TaskApplication.exe* Use isso compartilhado URL de assinatura de acesso quando ele carrega tooAzure de arquivo de saída de hello armazenamento. Você pode encontrar o código de saudação para isso no hello `UploadFileToContainer` método no projeto Olá TaskApplication `Program.cs` arquivo:

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a>Etapa 6: Monitorar tarefas
![Monitorar tarefas][6]<br/>
*Olá cliente (1) os monitores Olá tarefas para conclusão e o status de êxito e aplicativos (2) Olá tarefas carregamento resultado dados tooAzure armazenamento*

Quando tarefas são adicionadas tooa trabalho, eles são automaticamente na fila e agendados para execução em nós de computação no pool de saudação associado ao trabalho hello. Com base nas configurações de saudação que você especificar, lote trata enfileiramento de mensagens todas as tarefas, agendamento, repetir e outras tarefas de administração de tarefa para você.

Há muitas abordagens toomonitoring a execução da tarefa. O DotNetTutorial mostra um exemplo simples que relata apenas a conclusão e a falha de tarefas ou os estados de êxito. Dentro de saudação `MonitorTasks` do DotNetTutorial método `Program.cs`, há três conceitos de lote .NET que garantem a discussão. Eles são listados na ordem em que aparecem:

1. **ODATADetailLevel**: a especificação de um [ODATADetailLevel][net_odatadetaillevel] na lista de operações (como a obtenção de uma lista de tarefas do trabalho) é essencial para garantir o desempenho do aplicativo do Lote. Adicionar [consultar o serviço de lote do Azure Olá com eficiência](batch-efficient-list-queries.md) tooyour ler lista se você planeja fazer qualquer tipo de monitoramento de status em seus aplicativos de lote.
2. **TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] fornece aplicativos .NET do Lote com utilitários auxiliares para monitorar estados da tarefa. Em `MonitorTasks`, *DotNetTutorial* aguarda tooreach de todas as tarefas [TaskState.Completed] [ net_taskstate] dentro de um limite de tempo. Em seguida, encerra o trabalho de saudação.
3. **TerminateJobAsync**: encerrando um trabalho com [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (ou Olá bloqueando JobOperations.TerminateJob) marca trabalho como concluído. É essencial toodo se sua solução de lote usa um [JobReleaseTask][net_jobreltask]. Esse é um tipo especial de tarefa, descrita em [Tarefas de preparação e de conclusão do trabalho](batch-job-prep-release.md).

Olá `MonitorTasks` método de *DotNetTutorial*do `Program.cs` é exibida abaixo:

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a>Etapa 7: Baixar a saída da tarefa
![Baixar a saída da tarefa do Armazenamento][7]<br/>

Agora que hello trabalho é concluído, saída de hello das tarefas de saudação pode ser baixada do armazenamento do Azure. Isso é feito com uma chamada muito`DownloadBlobsFromContainerAsync` na *DotNetTutorial*do `Program.cs`:

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> Olá chamada muito`DownloadBlobsFromContainerAsync` em Olá *DotNetTutorial* aplicativo especifica que arquivos Olá devem ser baixado tooyour `%TEMP%` pasta. Sinta-se livre toomodify este local de saída.
>
>

## <a name="step-8-delete-containers"></a>Etapa 8: Excluir contêineres
Como você é cobrado pelos dados que residem no armazenamento do Azure, é sempre blobs de tooremove uma boa ideia que não são mais necessários para seus trabalhos em lotes. Do DotNetTutorial `Program.cs`, isso é feito com o método de auxiliar três chamadas toohello `DeleteContainerAsync`:

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

método Hello em si simplesmente obtém um contêiner de toohello de referência e, em seguida, chama [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Etapa 9: Excluir trabalho hello e pool Olá
Na etapa final do hello, você está toodelete solicitadas Olá trabalho Olá pool e que foram criados pelo aplicativo de DotNetTutorial hello. Embora você não seja cobrado pelos trabalhos e pelas tarefas, *será* cobrado pelos nós de computação. Portanto, recomendamos que você aloque os nós conforme necessário. A exclusão de pools não utilizados pode fazer parte de seu processo de manutenção.

Olá BatchClient [JobOperations] [ net_joboperations] e [PoolOperations] [ net_pooloperations] têm métodos correspondentes de exclusão, que são chamados se usuário de saudação Confirmar exclusão:

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> Tenha em mente que você será cobrado pelos recursos de computação, a exclusão dos pools não utilizados reduzirá o custo. Além disso, esteja ciente que a exclusão do pool de exclui todos os nós de computação no pool, e que os dados em nós hello serão irrecuperáveis depois Olá pool é excluído.
>
>

## <a name="run-hello-dotnettutorial-sample"></a>Executar Olá *DotNetTutorial* exemplo
Quando você executa o aplicativo de exemplo hello, saída de console hello será a seguir toohello semelhante. Durante a execução, você terá uma pausa em `Awaiting task completion, timeout in 00:30:00...` enquanto nós de computação do pool de saudação são iniciados. Saudação de uso [portal do Azure] [ azure_portal] toomonitor seu pool, nós de computação, trabalhos e tarefas durante e após a execução. Saudação de uso [portal do Azure] [ azure_portal] ou hello [Azure Storage Explorer] [ storage_explorers] tooview Olá recursos de armazenamento (contêineres e blobs) que são criado por um aplicativo hello.

Tempo de execução típico é **aproximadamente 5 minutos** quando você executa o aplicativo hello em sua configuração padrão.

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>Próximas etapas
Sinta-se livre toomake alterações muito*DotNetTutorial* e *TaskApplication* tooexperiment com diferentes cenários de computação. Por exemplo, tente adicionar um atraso de execução muito*TaskApplication*, tal como com [Sleep][net_thread_sleep], toosimulate demoradas tarefas e monitorá-los no portal de saudação. Tente adicionar mais tarefas ou ajustar Olá número de nós de computação. Adicionar lógica toocheck para e permitir o uso de saudação de um tempo de execução toospeed pool existente (*dica*: check-out `ArticleHelpers.cs` em Olá [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] project no [exemplos de lote do azure][github_samples]).

Agora que você está familiarizado com o fluxo de trabalho básico de uma solução de lote Olá, é hora toodig em toohello de recursos adicionais do serviço de lote de saudação.

* Saudação de revisão [recursos de visão geral do Azure Batch](batch-api-basics.md) artigo, que é recomendável que você confirme o novo serviço toohello.
* Início na Olá outros artigos de desenvolvimento de lote em **desenvolvimento detalhado** em Olá [de aprendizado em lotes][batch_learning_path].
* Check-out de uma implementação diferente de processamento de carga de trabalho hello "top N palavras" usando o lote em Olá [TopNWords] [ github_topnwords] exemplo.
* Saudação de revisão .NET em lotes [notas de versão](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) para alterações mais recentes de saudação na biblioteca de saudação.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Criar contêineres no Armazenamento do Azure"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Toocontainers de arquivos de tarefa de carregamento de aplicativo e de entrada (dados)"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Criar pool do Lote"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Criar trabalho em lotes"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Adicionar tarefas toojob"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Monitorar tarefas"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Baixar a saída da tarefa do Armazenamento"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Fluxo de trabalho da solução do Lote (diagrama completo)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Credenciais do Lote no Portal"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Credenciais do Armazenamento no Portal"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Fluxo de trabalho da solução do Lote (diagrama mínimo)"
