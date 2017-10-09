---
title: "aaaUse de atividades personalizadas em um pipeline da fábrica de dados do Azure"
description: "Saiba como atividades personalizadas toocreate e usá-los em um pipeline da fábrica de dados do Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a>Usar atividades personalizadas em um pipeline do Data Factory do Azure

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Atividade de Hive](data-factory-hive-activity.md) 
> * [Atividade Pig](data-factory-pig-activity.md)
> * [Atividade MapReduce](data-factory-map-reduce.md)
> * [Atividade de Transmissão do Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Atividade do Spark](data-factory-spark.md)
> * [Atividade de Execução em Lote do Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Atividade do Recurso de Atualização do Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Atividade de Procedimento Armazenado](data-factory-stored-proc-activity.md)
> * [Atividade do U-SQL do Data Lake Analytics](data-factory-usql-activity.md)
> * [Atividade Personalizada do .NET](data-factory-use-custom-activities.md)

Há dois tipos de atividades que você pode usar em um pipeline do Azure Data Factory.

- [As atividades de movimentação de dados](data-factory-data-movement-activities.md) toomove dados entre [suporte para armazenamentos de dados de origem e do coletor](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- [Atividades de transformação de dados](data-factory-data-transformation-activities.md) tootransform dados usando compute serviços como HDInsight do Azure, o lote do Azure e o aprendizado de máquina do Azure. 

toomove dados para/de um repositório de dados que não dão suporte a fábrica de dados, crie um **atividade personalizada** com seu próprios dados movimentação lógica e use hello atividade em um pipeline. Da mesma forma, tootransform/processar dados de forma que não é suportado pela fábrica de dados, criar uma atividade personalizada com sua própria lógica de transformação de dados e usar a atividade de saudação em um pipeline. 

Você pode configurar uma atividade personalizada toorun em uma **do Azure Batch** pool de máquinas virtuais ou baseado em Windows **HDInsight do Azure** cluster. Ao usar o Azure Batch, você só pode utilizar um pool de Lote do Azure existente. Ao passo que, ao usar o HDInsight, você pode usar um cluster HDInsight existente ou um cluster criado automaticamente para você sob demanda no tempo de execução.  

Olá, passo a passo fornece instruções passo a passo para criar uma atividade personalizada do .NET e usar atividades personalizadas Olá em um pipeline. Olá passo a passo usa um **do Azure Batch** serviço vinculado. serviço vinculado toouse um HDInsight do Azure, você cria um serviço vinculado do tipo **HDInsight** (seu próprio cluster HDInsight) ou **HDInsightOnDemand** (fábrica de dados cria um cluster HDInsight sob demanda). Em seguida, configure Olá toouse de atividade personalizada serviço vinculado do HDInsight. Consulte [serviços vinculados do uso do Azure HDInsight](#use-hdinsight-compute-service) seção para obter detalhes sobre o uso de atividade personalizada do Azure HDInsight toorun hello.

> [!IMPORTANT]
> - atividades personalizadas de .NET Olá executadas somente em clusters HDInsight baseados no Windows. Uma alternativa para essa limitação é toouse Olá mapa reduzir atividade toorun Java código personalizado em um cluster HDInsight baseados em Linux. Outra opção é toouse um pool de lote do Azure de atividades personalizadas de toorun de VMs em vez de usar um cluster HDInsight.
> - Não é possível toouse um Gateway de gerenciamento de dados de uma atividade personalizada tooaccess locais fontes de dados. Atualmente, [Data Management Gateway](data-factory-data-management-gateway.md) suporta apenas a atividade de cópia de saudação e a atividade de procedimento armazenado na fábrica de dados.   

## <a name="walkthrough-create-a-custom-activity"></a>Passo a passo: criar uma atividade personalizada
### <a name="prerequisites"></a>Pré-requisitos
* Visual Studio 2012/2013/2015
* Baixar e instalar o [SDK .NET do Azure](https://azure.microsoft.com/downloads/)

### <a name="azure-batch-prerequisites"></a>Pré-requisitos de Lote do Azure
Olá instruções passo a passo, você executa suas atividades personalizadas do .NET usando o lote do Azure como um recurso de computação. **Lote do Azure** é uma plataforma de serviço para execução paralela em grande escala e de aplicativos HPC (computação) com eficiência na nuvem de saudação de alto desempenho. Lote do Azure agenda toorun de trabalho de computação intensa no gerenciada **coleção de máquinas virtuais**, pode automaticamente escala de computação e necessidades de saudação toomeet recursos de seus trabalhos. Consulte [Noções básicas do lote do Azure] [ batch-technical-overview] artigo para uma visão geral detalhada da saudação serviço de lote do Azure.

Tutorial de hello, crie uma conta de lote do Azure com um pool de máquinas virtuais. Aqui estão as etapas de saudação:

1. Criar um **conta de lote do Azure** usando Olá [portal do Azure](http://portal.azure.com). Consulte o artigo [Criar e gerenciar uma conta do Lote do Azure][batch-create-account] para obter instruções.
2. Anote o nome da conta do Azure Batch hello, chave de conta, URI e nome do pool. É necessário que eles toocreate um serviço vinculado do Azure Batch.
    1. Na página inicial de saudação para conta de lote do Azure, você vê um **URL** em Olá formato a seguir: `https://myaccount.westus.batch.azure.com`. Neste exemplo, **myaccount** é nome de saudação do hello conta de lote do Azure. URI usado na definição de serviço vinculada de saudação é a URL de saudação sem nome hello da conta de saudação. Por exemplo: `https://<region>.batch.azure.com`.
    2. Clique em **chaves** no menu à esquerda do hello e Olá cópia **chave de acesso primário**.
    3. toouse um pool existente, clique em **Pools** no menu hello e anote Olá **ID** do pool de saudação. Se você não tiver um pool existente, mova toohello próxima etapa.     
2. Crie um pool do **Lote do Azure**.

   1. Em Olá [portal do Azure](https://portal.azure.com), clique em **procurar** no hello menus à esquerda e clique em **contas em lotes**.
   2. Selecione sua saudação do lote do Azure conta tooopen **conta em lotes** folha.
   3. Clique no bloco **Pools** .
   4. Em Olá **Pools** folha, clique no botão Adicionar na saudação da barra de ferramentas tooadd um pool.
      1. Insira uma ID para o pool de saudação (ID do Pool). Saudação de Observação **ID do pool de saudação**; é necessário ao criar a solução de fábrica de dados hello.
      2. Especifique **Windows Server 2012 R2** para configuração da família de sistemas operacionais de saudação.
      3. Selecione um **camada de preços de nó**.
      4. Digite **2** como valor para Olá **destino dedicado** configuração.
      5. Digite **2** como valor para Olá **tarefas máxima por nó** configuração.
   5. Clique em **Okey** toocreate pool de saudação.
   6. Anote Olá **ID** do pool de saudação. 



### <a name="high-level-steps"></a>Etapas de alto nível
Aqui estão Olá duas etapas de alto nível que fazem parte deste passo a passo: 

1. Crie uma atividade personalizada que contenha uma lógica simples de processamento/transformação de dados.
2. Crie uma fábrica de dados do Azure com um pipeline que usa a atividade personalizada hello.

### <a name="create-a-custom-activity"></a>Criar uma atividade personalizada
toocreate uma atividade personalizada do .NET, crie um **biblioteca de classes .NET** projeto com uma classe que implementa que **IDotNetActivity** interface. Essa interface tem apenas um método: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , e a assinatura é:

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


método Hello usa quatro parâmetros:

- **linkedServices**. Esta propriedade é uma lista enumerável de serviços de repositório de dados vinculado referenciado por conjuntos de dados de entrada/saída para a atividade de saudação.   
- **conjuntos de dados**. Esta propriedade é uma lista enumerável de conjuntos de dados de entrada/saída para a atividade de saudação. Você pode usar este locais de saudação do parâmetro tooget e esquemas definidos pelos conjuntos de dados de entrada e saídos.
- **atividade**. Esta propriedade representa a atividade atual de saudação. Ele pode ser usado tooaccess propriedades estendidas associadas com a atividade personalizada hello. Consulte [Acessar propriedades estendidas](#access-extended-properties) para obter mais detalhes.
- **logger**. Esse objeto permite que você escreva essa superfície de comentários de depuração no log de usuário Olá para o pipeline de saudação.

método Hello retorna um dicionário que pode ser atividades personalizadas toochain usados juntos em um futuro hello. Este recurso ainda não foi implementado, isso retornará um dicionário vazio do método hello.  

### <a name="procedure"></a>Procedimento
1. Crie um projeto de **Biblioteca de Classes do .NET** .
   <ol type="a">
     <li>Inicialize o <b>Visual Studio 2017</b> ou o <b>Visual Studio 2015</b> ou o <b>Visual Studio 2013</b> ou o <b>Visual Studio 2012</b>.</li>
     <li>Clique em <b>arquivo</b>, ponto muito<b>novo</b>e clique em <b>projeto</b>.</li>
     <li>Expanda <b>Modelos</b> e selecione <b>Visual C#</b>. Neste passo a passo, você pode usar c#, mas você pode usar qualquer atividade personalizada do .NET idioma toodevelop hello.</li>
     <li>Selecione <b>biblioteca de classes</b> da lista de saudação de tipos de projeto em saudação à direita. No VS 2017, escolha <b>Biblioteca de Classes (.NET Framework)</b> </li>
     <li>Digite <b>MyDotNetActivity</b> para Olá <b>nome</b>.</li>
     <li>Selecione <b>C:\ADFGetStarted</b> para Olá <b>local</b>.</li>
     <li>Clique em <b>Okey</b> toocreate projeto de saudação.</li>
   </ol>
2.Clique em **ferramentas**, ponto muito**NuGet Package Manager**e clique em **Package Manager Console**.
3. No hello Package Manager Console, execute Olá após o comando tooimport **Microsoft.Azure.Management.DataFactories**.

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Saudação de importação **armazenamento do Azure** pacote do NuGet no projeto toohello.

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > Iniciador do serviço de fábrica de dados requer a versão de hello 4.3 do windowsazure. Se você adicionar uma referência tooa versão posterior do assembly de armazenamento do Azure no seu projeto de atividade personalizada, você vê um erro quando hello atividade é executada. Erro de saudação tooresolve, consulte [Appdomain isolamento](#appdomain-isolation) seção. 
5. Adicione o seguinte Olá **usando** instruções toohello fonte arquivo hello projeto.

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Alterar o nome de saudação do hello **namespace** muito**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Alterar o nome de saudação da classe Olá muito**MyDotNetActivity** e ele derivam Olá **IDotNetActivity** interface conforme mostrado no trecho de código a seguir de saudação:

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Saudação de implementar (Adicionar) **Execute** método hello **IDotNetActivity** interface toohello **MyDotNetActivity** Olá cópia e de classe, método de toohello de código de exemplo a seguir.

    Olá exemplo a seguir conta Olá número de ocorrências do termo de pesquisa da saudação ("Microsoft") em cada blob associado a uma fatia de dados.

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass hello connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize hello continuation token before using it in hello do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get hello list of input blobs from hello input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns hello number of occurrences of
            // hello search term (“Microsoft”) in each blob associated
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload hello output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} toohello output blob", output);
        outputBlob.UploadText(output);
    
        // hello dictionary can be used toochain custom activities together in hello future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. Adicione Olá métodos auxiliares a seguir: 

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    Olá GetFolderPath método retorna Olá caminho toohello pasta que Olá dataset aponta tooand Olá GetFileName retorna Olá nome do método de saudação/arquivo de blob que Olá pontos de conjunto de dados para. Se você havefolderPath define usando variáveis como {Year}, {Month} retorna {Day} etc., método hello Olá cadeia de caracteres que é sem substituí-los com valores de tempo de execução. Confira a seção [Acessar propriedades estendidas](#access-extended-properties) para obter detalhes sobre como acessar SliceStart, SliceEnd, etc.    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    Olá método Calculate calcula o número de saudação de instâncias da palavra-chave Microsoft nos arquivos de entrada hello (blobs na pasta Olá). termo de pesquisa da saudação ("Microsoft") é embutido em código hello.
10. Compile o projeto de saudação. Clique em **criar** de saudação menu e clique em **compilar solução**.

    > [!IMPORTANT]
    > Conjunto 4.5.2 versão do .NET Framework, como o framework de destino de saudação do seu projeto: clique com botão direito hello e, em seguida, clique em **propriedades** tooset framework de destino de saudação. O Data Factory não oferece suporte a atividades personalizadas compiladas em versões do .NET Framework posteriores a 4.5.2.

11. Iniciar **Windows Explorer**e navegue muito**bin\debug** ou **bin\release** pasta dependendo do tipo de saudação da compilação.
12. Criar um arquivo zip **MyDotNetActivity.zip** que contém todos os binários de saudação em Olá <project folder>pasta \bin\Debug. Incluir Olá **MyDotNetActivity.pdb** arquivos de forma que você obter detalhes adicionais, como o número de linha no código-fonte Olá que causou o problema de saudação se houve uma falha. 

    > [!IMPORTANT]
    > Todos Olá arquivos contidos no arquivo zip Olá para atividade de saudação personalizada deve estar no hello **nível superior** com nenhuma subpastas.

    ![Arquivos de saída binários](./media/data-factory-use-custom-activities/Binaries.png)
14. Crie um contêiner de blob chamado **customactivitycontainer** se ele ainda não existir. 
15. Carregar MyDotNetActivity.zip como customactivitycontainer de toohello um blob em um **geral** armazenamento de BLOBs do Azure (armazenamento de Blob não hot/cool) que é referenciado por AzureStorageLinkedService.  

> [!IMPORTANT]
> Se você adiciona essa solução de tooa de projeto de atividade .NET no Visual Studio que contém um projeto de fábrica de dados e adicionar um projeto de atividade de too.NET de referência de projeto de aplicativo hello fábrica de dados, não é necessário tooperform Olá duas últimas etapas de criação manual arquivo zip de saudação e carregando-o armazenamento de BLOBs do Azure para fins gerais toohello. Quando você publica entidades da fábrica de dados usando o Visual Studio, essas etapas são executadas automaticamente pelo processo de publicação de saudação. Para obter mais informações, consulte a seção [projeto de Data Factory no Visual Studio](#data-factory-project-in-visual-studio).

## <a name="create-a-pipeline-with-custom-activity"></a>Criar um pipeline com atividade personalizada
Você criar uma atividade personalizada e carregar o arquivo zip de saudação com contêiner de blob tooa binários em uma **geral** conta de armazenamento do Azure. Nesta seção, você pode criar uma fábrica de dados do Azure com um pipeline que usa a atividade personalizada hello.

conjunto de dados de entrada de Hello atividade personalizado Olá representa blobs (arquivos) na pasta de customactivityinput de saudação do contêiner adftutorial no armazenamento de blob de saudação. Olá o conjunto de dados de saída para a atividade de saudação representa blobs de saída na pasta de customactivityoutput de saudação do contêiner adftutorial no armazenamento de blob de saudação.

Criar **arquivo.txt** arquivo com hello seguinte conteúdo e carregá-lo muito**customactivityinput** pasta da saudação **adftutorial** contêiner. Crie contêiner de adftutorial Olá se ele ainda não existir. 

```
test custom activity Microsoft test custom activity Microsoft
```

pasta entrada Hello corresponde tooa fatia na fábrica de dados do Azure, mesmo se a pasta de saudação tem dois ou mais arquivos. Quando cada fatia é processada pelo pipeline hello, atividade personalizada Olá itera em todos os blobs de saudação na pasta de entrada hello essa fatia.

Você verá um arquivo na pasta de adftutorial\customactivityoutput Olá de saída com uma ou mais linhas (mesmo que o número de blobs na pasta de entrada hello):

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


Aqui estão as etapas Olá que executar nesta seção:

1. Criar uma **data factory**.
2. Criar **serviços vinculados** para pool de lote do Azure Olá de VMs em qual hello atividade personalizada é executado e Olá armazenamento do Azure que contém Olá blobs de entrada/saída.
3. Criar a entrada e saída **conjuntos de dados** que representam a entrada e saída da atividade personalizada hello.
4. Criar um **pipeline** que usa a atividade personalizada hello.

> [!NOTE]
> Criar hello **arquivo.txt** e carregue-o contêiner de blob tooa se você ainda não tiver feito isso. Consulte as instruções em Olá anterior de seção.   

### <a name="step-1-create-hello-data-factory"></a>Etapa 1: Criar a fábrica de dados Olá
1. Após o logon toohello portal do Azure, Olá etapas a seguir:
   1. Clique em **novo** no menu esquerdo hello.
   2. Clique em **dados + análise** em Olá **novo** folha.
   3. Clique em **Data Factory** em Olá **análises de dados** folha.
   
    ![Novo menu do Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. Em Olá **nova fábrica de dados** folha, digite **CustomActivityFactory** para Olá nome. nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo. Se você receber o erro Olá: **"CustomActivityFactory" nome da fábrica de dados não está disponível**, alterar nome Olá Olá da fábrica de dados (por exemplo, **yournameCustomActivityFactory**) e tente criar novamente.

    ![Nova folha do Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. Clique em **NOME DO GRUPO DE RECURSOS**para selecionar um grupo de recursos existente ou criar um.
4. Verificar se você está usando Olá correto **assinatura** e **região** onde você deseja Olá toobe de fábrica de dados criado.
5. Clique em **criar** em Olá **nova fábrica de dados** folha.
6. Você verá a fábrica de dados hello está sendo criada no hello **painel** de saudação portal do Azure.
7. Depois de fábrica de dados Olá tiver sido criada com êxito, você verá a folha de fábrica de dados hello, que mostra Olá conteúdo Olá da fábrica de dados.
    
    ![Folha Data Factory](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a>Etapa 2: Criar serviços vinculados
Serviços vinculados vincular armazenamentos de dados ou de computação serviços tooan data factory do Azure. Nesta etapa, você pode vincular sua conta de armazenamento do Azure e a fábrica de dados de tooyour de conta de lote do Azure.

#### <a name="create-azure-storage-linked-service"></a>Criar o serviço vinculado do armazenamento do Azure
1. Clique em Olá **autor e implantar** bloco Olá **DATA FACTORY** folha para **CustomActivityFactory**. Você verá Olá Editor da fábrica de dados.
2. Clique em **novo repositório de dados** Olá barra de comandos e escolha **armazenamento do Azure**. Você deve ver Olá script JSON para a criação de um armazenamento do Azure vinculada serviço no editor de saudação.
    
    ![Novo armazenamento de dados – Armazenamento do Azure](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. Substituir `<accountname>` com o nome da sua conta de armazenamento do Azure e `<accountkey>` com a chave de acesso do hello conta de armazenamento do Azure. toolearn como tooget seu armazenamento acessar chave, consulte [exibir, copiar e regenerar as contas de armazenamento de chaves de acesso](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

    ![Serviço vinculado do Armazenamento do Azure](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.

#### <a name="create-azure-batch-linked-service"></a>Crie o serviço vinculado do Lote do Azure
1. No hello Editor da fábrica de dados, clique em **... Mais** na barra de comandos de saudação, clique em **nova computação**e, em seguida, selecione **do Azure Batch** menu hello.

    ![Nova computação – Lote do Azure](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. Verifique Olá alterações toohello JSON script a seguir:

   1. Especifique o nome da conta de lote do Azure para Olá **accountName** propriedade. Olá **URL** de saudação **folha de conta de lote do Azure** está em Olá formato a seguir: `http://accountname.region.batch.azure.com`. Para Olá **batchUri** propriedade Olá JSON, você precisa tooremove `accountname.` de Olá Olá URL e use `accountname` para Olá `accountName` propriedade JSON.
   2. Especifique a chave de conta de lote do Azure Olá para hello **accessKey** propriedade.
   3. Especifique o nome de saudação de pool de saudação criado como parte dos pré-requisitos para hello **poolName** propriedade. Você também pode especificar a ID de saudação do pool de saudação em vez do nome de saudação do pool de saudação de.
   4. Especifique o URI do lote do Azure para Olá **batchUri** propriedade. Exemplo: `https://westus.batch.azure.com`.  
   5. Especifique a saudação **AzureStorageLinkedService** para Olá **linkedServiceName** propriedade.

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       Para Olá **poolName** propriedade, você também pode especificar a ID de saudação do pool de saudação em vez do nome de saudação do pool de saudação de.

      > [!IMPORTANT]
      > Olá serviço da fábrica de dados não dá suporte uma opção sob demanda para o lote do Azure como faz para HDInsight. Você só pode usar seu próprio pool do Azure Batch em um Azure Data Factory.   
    

### <a name="step-3-create-datasets"></a>Etapa 3: Criar conjuntos de dados
Nesta etapa, você cria conjuntos de dados toorepresent entrada e saída de dados.

#### <a name="create-input-dataset"></a>Criar conjunto de dados de entrada
1. Em Olá **Editor** para Olá fábrica de dados, clique em **... Mais** na barra de comandos de saudação, clique em **novo conjunto de dados**e, em seguida, selecione **armazenamento de BLOBs do Azure** do menu suspenso de saudação.
2. Substitua Olá JSON no painel direito Olá Olá trecho JSON a seguir:

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   Você cria um pipeline posteriormente neste passo a passo com hora de início: 2016-11-16T00:00:00Z e final: 2016-11-16T05:00:00Z. São dados tooproduce agendado por hora, portanto, há cinco fatias de entrada/saída (entre **00**: 00:00 -> **05**: 00:00).

   Olá **frequência** e **intervalo** para o conjunto de dados de entrada hello está definido muito**hora** e **1**, que significa que Olá entrada fatia está disponível por hora. Neste exemplo, é Olá mesmo arquivo (arquivo. txt) em intputfolder hello.

   Aqui estão os horários de início de saudação de cada fatia, que é representado pela variável de sistema SliceStart no hello acima trecho JSON.
3. Clique em **implantar** Olá toocreate da barra de ferramentas e implantar Olá **InputDataset**. Confirme que você vê Olá **tabela CRIADA com êxito** mensagem na barra de título de saudação da saudação Editor.

#### <a name="create-an-output-dataset"></a>Criar um conjunto de dados de saída
1. Em Olá **editor da fábrica de dados**, clique em **... Mais** na barra de comandos de saudação, clique em **novo conjunto de dados**e, em seguida, selecione **armazenamento de BLOBs do Azure**.
2. Substitua script JSON de saudação no painel direito Olá Olá script JSON a seguir:

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     Local de saída é **adftutorial/customactivityoutput/** e o nome do arquivo de saída é AAAA-MM-dd-HH.txt onde AAAA-MM-dd-HH é ano hello, mês, data e hora da fatia Olá sendo produzida. Consulte a [Referência do Desenvolvedor][adf-developer-reference] para obter detalhes.

    Um blob/arquivo de saída é gerado para cada fatia de entrada. Aqui está como um arquivo de saída é chamado para cada fatia. Todos os arquivos de saída de hello são gerados em uma pasta de saída: **adftutorial\customactivityoutput**.

   | Fatia | Hora de início | Arquivo de saída |
   |:--- |:--- |:--- |
   | 1 |2016-11-16T00:00:00 |2016-11-16-00.txt |
   | 2 |2016-11-16T01:00:00 |2016-11-16-01.txt |
   | 3 |2016-11-16T02:00:00 |2016-11-16-02.txt |
   | 4 |2016-11-16T03:00:00 |2016-11-16-03.txt |
   | 5 |2016-11-16T04:00:00 |2016-11-16-04.txt |

    Lembre-se de que todos os arquivos de saudação em uma pasta de entrada são parte de uma fatia com horários de início da saudação mencionados acima. Quando essa fatia é processada, a atividade personalizada Olá verifica cada arquivo e produz uma linha no arquivo de saída de hello com número de saudação de ocorrências do termo de pesquisa ("Microsoft"). Se houver três arquivos na inputfolder hello, há três linhas no arquivo de saída de saudação de cada fatia por hora: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.
3. Olá toodeploy **OutputDataset**, clique em **implantar** na barra de comandos de saudação.

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a>Criar e executar um pipeline que usa a atividade personalizada Olá
1. No hello Editor da fábrica de dados, clique em **... Mais**e, em seguida, selecione **novo pipeline** na barra de comandos de saudação. 
2. Substitua Olá JSON no painel direito Olá Olá script JSON a seguir:

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    Observe Olá pontos a seguir:

   * **Simultaneidade** está definido muito**2** para que duas fatias são processadas em paralelo por 2 VMs no pool de lote do Azure hello.
   * Há uma atividade na seção de atividades de saudação e é do tipo: **DotNetActivity**.
   * **AssemblyName** é definir o nome toohello Olá DLL: **MyDotnetActivity.dll**.
   * **Ponto de entrada** está definido muito**MyDotNetActivityNS.MyDotNetActivity**.
   * **PackageLinkedService** está definido muito**AzureStorageLinkedService** que aponte toohello armazenamento de blob que contém o arquivo de zip hello atividade personalizado. Se você estiver usando diferentes contas de armazenamento do Azure para arquivos de entrada/saída e hello arquivo zip de atividade personalizada, você criar outro serviço vinculado do armazenamento do Azure. Este artigo pressupõe que você está usando Olá a mesma conta de armazenamento do Azure.
   * **PackageFile** está definido muito**customactivitycontainer/MyDotNetActivity.zip**. Formato de saudação: containerforthezip/nameofthezip.zip.
   * atividades personalizadas Olá **InputDataset** como entrada e **OutputDataset** como saída.
   * propriedade linkedServiceName Hello atividade personalizada Olá pontos toohello **AzureBatchLinkedService**, que informa ao Azure Data Factory dessa atividade personalizada Olá precisa toorun em VMs do lote do Azure.
   * **isPaused** propriedade for definida muito**false** por padrão. Olá pipeline é executado imediatamente neste exemplo como fatias Olá começam em Olá anterior. Você pode configurar o pipeline de saudação essa propriedade tootrue toopause e defina-a como toorestart toofalse back.
   * Olá **iniciar** tempo e **final** vezes são **cinco** horas separadas e fatias são produzidas por hora, para cinco fatias são produzidas pelo pipeline de saudação.
3. pipeline de saudação toodeploy, clique em **implantar** na barra de comandos de saudação.

### <a name="monitor-hello-pipeline"></a>Pipeline de saudação do monitor
1. Na folha da fábrica de dados Olá no hello portal do Azure, clique em **diagrama**.

    ![Bloco do diagrama](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. Na exibição de diagrama de Olá, agora clique Olá OutputDataset.

    ![Exibição de diagrama](./media/data-factory-use-custom-activities/diagram.png)
3. Você deve ver que cinco fatias de saída Olá estão em estado pronto do hello. Se não estiverem no estado pronto do hello, que ainda não foram produzidas ainda. 

   ![Fatias de saída](./media/data-factory-use-custom-activities/OutputSlices.png)
4. Verifique se que arquivos de saída de hello são gerados no armazenamento de blob de saudação em Olá **adftutorial** contêiner.

   ![saída de atividade personalizada][image-data-factory-ouput-from-custom-activity]
5. Se você abrir o arquivo de saída de hello, você deve ver Olá saída semelhante toohello saída a seguir:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. Saudação de uso [portal do Azure] [ azure-preview-portal] ou toomonitor de cmdlets do PowerShell do Azure sua fábrica de dados, pipelines e conjuntos de dados. Você pode ver as mensagens de saudação **ActivityLogger** no código de saudação para a atividade personalizada Olá nos logs de saudação (especificamente usuário-0.log) que você pode baixar do portal de saudação ou usando cmdlets.

   ![baixar logs de atividade personalizada][image-data-factory-download-logs-from-custom-activity]

Consulte [Monitorar e Gerenciar Pipelines](data-factory-monitor-manage-pipelines.md) para obter etapas detalhadas do monitoramento de conjuntos de dados e pipelines.      

## <a name="data-factory-project-in-visual-studio"></a>Projeto de Data Factory no Visual Studio  
Você pode criar e publicar entidades de Data Factory usando o Visual Studio, em vez de usar o portal do Azure. Para obter informações detalhadas sobre a criação e publicação de entidades da fábrica de dados usando o Visual Studio, consulte [criar seu primeiro pipeline usando o Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) e [copiar dados de Blob do Azure tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) artigos.

Olá etapas adicionais a seguir se você estiver criando o projeto de fábrica de dados no Visual Studio:
 
1. Adicione Olá Data Factory projeto toohello solução do Visual Studio que contém o projeto de atividade personalizada hello. 
2. Adicione um projeto de atividade do .NET de toohello Referência de projeto de fábrica de dados de saudação. Clique com botão direito fábrica de dados, aponte muito**adicionar**e, em seguida, clique em **referência**. 
3. Em Olá **adicionar referência** caixa de diálogo, selecione Olá **MyDotNetActivity** do projeto e clique em **Okey**.
4. Criar e publicar Olá solução.

    > [!IMPORTANT]
    > Quando você publica entidades da fábrica de dados, um arquivo zip é criado automaticamente para você e é o contêiner de blob carregado toohello: customactivitycontainer. Se o contêiner de blob Olá não existir, ela é criada automaticamente muito.  


## <a name="data-factory-and-batch-integration"></a>Integração de Data Factory e Lote
Olá serviço da fábrica de dados cria um trabalho em lote do Azure com o nome da saudação: **poolname adf: trabalho xxx**. Clique em **trabalhos** no menu esquerdo hello. 

![Trabalhos de Azure Data Factory - Lote](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

Uma tarefa é criada para cada execução de atividade da fatia. Se houver cinco toobe pronto fatias processadas, cinco tarefas são criadas no trabalho. Se houver vários nós de computação no pool do lote de saudação, duas ou mais fatias podem ser executados em paralelo. Se o conjunto de nós de computação de máximo de tarefas por Olá muito > 1, você também pode ter mais de uma fatia em execução no hello computação mesmo.

![Tarefas do trabalho de Azure Data Factory - Lote](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

Olá diagrama a seguir ilustra o relacionamento de saudação entre tarefas do Azure Data Factory e lote.

![Data Factory e lote](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a>Falhas na solução de problemas
A solução de problemas consiste em algumas técnicas básicas:

1. Se você vir Olá erro a seguir, você pode estar usando um armazenamento de blob acesso/Cool em vez de usar um armazenamento de BLOBs do Azure para fins gerais. Carregar Olá zip arquivo tooa **conta de armazenamento do Azure para fins gerais**. 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. Se você vir Olá erro a seguir, confirme que nome de saudação de classe Olá Olá CS arquivo corresponde ao Olá nome especificado para Olá **EntryPoint** propriedades em JSON de pipeline hello. Passo a passo Olá, nome da classe de saudação é: MyDotNetActivity e Olá EntryPoint no hello JSON é: MyDotNetActivityNS. **MyDotNetActivity**.

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   Se Olá correspondam, confirme se todos os binários de saudação estão em Olá **pasta raiz** do arquivo zip de saudação. Ou seja, quando você abrir o arquivo zip de saudação, você deve ver todos os arquivos de saudação na pasta raiz de hello, mas não em quaisquer subpastas.   
3. Se a fatia de entrada hello não está definida muito**pronto**, confirme se a estrutura de pasta de entrada hello está correta e **arquivo. txt** existe em pastas de entrada hello.
3. Em Olá **Execute** método de sua atividade personalizada, use Olá **IActivityLogger** informações toolog do objeto que ajuda você a solucionar problemas. mensagens de saudação conectada aparecem nos arquivos de log de usuário hello (um ou mais arquivos nomeados: usuário 0.log, 1.log de usuário, usuário 2.log, etc.).

   Em Olá **OutputDataset** folha, clique em Olá fatia toosee Olá **FATIA de dados** folha para essa fatia. Você vê as **execuções de atividade** para essa fatia. Você deve ver uma atividade executar fatia hello. Se você clicar em executar na barra de comandos hello, você pode iniciar outra atividade executada para Olá mesma fatia.

   Quando você clica em execução da atividade hello, você vê Olá **detalhes de execução da atividade** folha com uma lista de arquivos de log. Você ver as mensagens registradas no arquivo de user_0.log hello. Quando ocorre um erro, você verá três execuções de atividade porque a contagem de repetição de saudação é definida too3 Olá pipeline/atividade JSON. Quando você clica em execução da atividade Olá, você ver arquivos de log de saudação que você pode examinar o erro de saudação tootroubleshoot.

   Na lista de saudação de arquivos de log, clique em Olá **0.log usuário**. No painel direito da saudação são resultados de saudação do uso Olá **IActivityLogger.Write** método. Se não ver todas as mensagens, verifique se você terá mais arquivos de log chamados: user_1.log, user_2.log, etc. Caso contrário, o código de saudação pode ter falhado depois Olá registrado última mensagem.

   Verifique **system-0.log** para quaisquer mensagens de erro e exceções do sistema.
4. Incluir Olá **PDB** no arquivo zip de saudação do arquivo para que os detalhes do erro Olá contêm informações como **pilha de chamadas** quando ocorre um erro.
5. Todos Olá arquivos contidos no arquivo zip Olá para atividade de saudação personalizada deve estar no hello **nível superior** com nenhuma subpastas.
6. Certifique-se de que Olá **assemblyName** (MyDotNetActivity.dll) **entryPoint**(MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip), e **packageLinkedService** (deve apontar toohello **geral**armazenamento de BLOBs do Azure que contém o arquivo zip de saudação) são definidos valores toocorrect.
7. Se você fixa uma fatia de saudação tooreprocess erro e quiser, clique com botão direito fatia Olá Olá **OutputDataset** folha e clique em **executar**.
8. Se você vir Olá erro a seguir, você está usando o pacote do armazenamento do Azure Olá de versão > 4.3.0. Iniciador do serviço de fábrica de dados requer a versão de hello 4.3 do windowsazure. Consulte [Appdomain isolamento](#appdomain-isolation) seção para uma solução alternativa se você precisar usar Olá versão posterior do assembly de armazenamento do Azure. 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    Se você pode usar a versão de hello 4.3.0 do pacote do armazenamento do Azure, remova Olá referência tooAzure armazenamento pacote existente de versão > 4.3.0. Em seguida, execute Olá após o comando NuGet Package Manager Console. 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    Compile o projeto de saudação. Exclua Azure.Storage assembly de versão > 4.3.0 Olá bin\Debug pasta. Crie um arquivo zip com binários e o arquivo PDB hello. Substitua o arquivo zip da antiga Olá por no contêiner de blob da saudação (customactivitycontainer). Olá execute fatias com falha (com o botão direito fatia e clique em Executar).   
8. atividade personalizada Olá não usa Olá **App. config** arquivo do seu pacote. Portanto, se seu código lê qualquer cadeia de caracteres de conexão do arquivo de configuração hello, ele não funciona em tempo de execução. Olá prática recomendada ao usar o lote do Azure é toohold qualquer segredos em um **Azure KeyVault**, use uma saudação tooprotect principal de serviço com base em certificado **keyvault**e distribuir certificados Olá tooAzure pool do lote. Hello atividade personalizada do .NET pode acessar segredos de saudação KeyVault em tempo de execução. Essa solução é uma solução genérica e pode ser dimensionado tooany tipo de segredo, não apenas a cadeia de conexão.

   Há uma solução mais fácil (mas não é uma prática recomendada): você pode criar um **serviço vinculado do SQL Azure** com configurações de cadeia de caracteres de conexão, criar um conjunto de dados que usa Olá serviço vinculado e cadeia Olá conjunto de dados como um conjunto de dados de entrada fictício toohello atividade personalizada de .NET. Você pode então Olá acesso vinculado cadeia de caracteres de conexão do serviço no código do hello atividade personalizado.  

## <a name="update-custom-activity"></a>Atualize a atividade personalizada
Se você atualizar o código de hello atividade personalizado hello, compile-o e carregue o arquivo hello. zip que contém o novo armazenamento de blob toohello binários.

## <a name="appdomain-isolation"></a>Isolamento de Appdomain
Consulte [entre AppDomain exemplo](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) que mostra como toocreate uma atividade personalizada que não é restrita versões tooassembly usadas pelo iniciador da fábrica de dados de saudação (exemplo: v 4.3.0 do windowsazure v6.0.x newtonsoft. JSON, etc.).

## <a name="access-extended-properties"></a>Acessar propriedades estendidas
Você pode declarar propriedades estendidas na atividade de saudação JSON conforme Olá exemplo a seguir:

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


Exemplo hello, há duas propriedades estendidas: **SliceStart** e **DataFactoryName**. valor Olá SliceStart baseia-se a variável de sistema SliceStart hello. Consulte [Variáveis de Sistema](data-factory-functions-variables.md) para obter uma lista das variáveis de sistema com suporte. valor Olá DataFactoryName é tooCustomActivityFactory embutida.

tooaccess essas propriedades estendidas de em Olá **Execute** método, use código semelhante toohello, código a seguir:

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a>Dimensionamento automático do Lote do Azure
Você também pode criar um pool de Lotes do Azure com o recurso **autoscale** . Por exemplo, você pode criar um pool de lote do azure com 0 VMs dedicadas e uma fórmula de dimensionamento automático com base no número de saudação de tarefas pendentes. 

fórmula de exemplo Hello aqui alcança Olá comportamento a seguir: quando o pool de saudação inicialmente é criado, ele começa com 1 VM. Métrica de $PendingTasks define o número de saudação de tarefas em execução + ativo (na fila) estado.  fórmula de saudação localiza Olá média de tarefas pendentes no hello Últimos 180 segundos e define TargetDedicated adequadamente. Isso garante que TargetDedicated nunca ultrapasse 25 VMs. Assim, como novas tarefas forem enviadas, pool cresce automaticamente e como tarefas concluídas, as VMs se tornam livre uma e hello autoscaling reduz as VMs. startingNumberOfVMs e maxNumberofVMs podem ser ajustadas tooyour necessidades.

Fórmula de dimensionamento automático:

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

Consulte [Dimensionar automaticamente os nós de computação em um pool de Lotes do Azure](../batch/batch-automatic-scaling.md) para obter detalhes.

Se estiver usando o pool de saudação padrão Olá [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), Olá serviço de lote pode levar 15 a 30 minutos tooprepare Olá VM antes de executar a atividade personalizada hello.  Se o pool de saudação está usando um autoScaleEvaluationInterval diferente, Olá serviço de lote pode levar autoScaleEvaluationInterval + 10 minutos.

## <a name="use-hdinsight-compute-service"></a>Use o serviço de computação do HDInsight
Olá explicação passo a passo, você usou a atividade personalizada do lote do Azure computação toorun Olá. Você pode também usar seu próprio cluster HDInsight baseados em Windows ou fábrica de dados criar uma cluster baseado no Windows HDInsight sob demanda e ter atividade personalizada Olá executados no cluster do HDInsight hello. Aqui estão as etapas de alto nível Olá para usar um cluster HDInsight.

> [!IMPORTANT]
> atividades personalizadas de .NET Olá executadas somente em clusters HDInsight baseados no Windows. Uma alternativa para essa limitação é toouse Olá mapa reduzir atividade toorun Java código personalizado em um cluster HDInsight baseados em Linux. Outra opção é toouse um pool de lote do Azure de atividades personalizadas de toorun de VMs em vez de usar um cluster HDInsight.
 

1. Criar um serviço vinculado do Azure HDInsight.   
2. Serviço em vez de vinculado do HDInsight de uso **AzureBatchLinkedService** em Olá JSON de pipeline.

Se você quiser tootest com hello passo a passo, alteração **iniciar** e **final** horas para o pipeline de hello, de modo que você pode testar o cenário de saudação com hello serviço HDInsight do Azure.

#### <a name="create-azure-hdinsight-linked-service"></a>Criar o serviço vinculado do Azure HDInsight
Olá serviço fábrica de dados do Azure oferece suporte à criação de um cluster sob demanda e use-a como dados de saída tooprocess tooproduce de entrada. Você também pode usar seu próprio cluster tooperform Olá mesmo. Quando você usa o cluster HDInsight sob demanda, um cluster é criado para cada fatia. Por outro lado, se você usar seu próprio cluster HDInsight, cluster hello está pronto tooprocess Olá fatia imediatamente. Portanto, quando você usa um cluster sob demanda, você não verá os dados de saída de hello mais rápido quando você usa seu próprio cluster.

> [!NOTE]
> Em tempo de execução, uma instância de uma atividade de .NET é executado somente em um nó de trabalho no cluster do HDInsight Olá; ele não pode ser dimensionado toorun em vários nós. Várias instâncias de atividade .NET podem ser executados em paralelo em diferentes nós de cluster do HDInsight hello.
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a>toouse um cluster do HDInsight sob demanda
1. Em Olá **portal do Azure**, clique em **criar e implantar** na home page do hello fábrica de dados.
2. No hello Editor da fábrica de dados, clique em **nova computação** do comando Olá barra e selecione **cluster HDInsight sob demanda** menu hello.
3. Verifique Olá alterações toohello JSON script a seguir:

   1. Para Olá **clusterSize** propriedade, especificar o tamanho de saudação do cluster do HDInsight hello.
   2. Para Olá **timeToLive** propriedade, especifique quanto tempo Prezado cliente pode ficar ocioso antes de ser excluído.
   3. Para Olá **versão** propriedade, especificar a versão do HDInsight Olá deseja toouse. Se você excluir essa propriedade, a versão mais recente da saudação é usado.  
   4. Para Olá **linkedServiceName**, especifique **AzureStorageLinkedService**.

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > atividades personalizadas de .NET Olá executadas somente em clusters HDInsight baseados no Windows. Uma alternativa para essa limitação é toouse Olá mapa reduzir atividade toorun Java código personalizado em um cluster HDInsight baseados em Linux. Outra opção é toouse um pool de lote do Azure de atividades personalizadas de toorun de VMs em vez de usar um cluster HDInsight.

4. Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.

##### <a name="toouse-your-own-hdinsight-cluster"></a>toouse seu próprio cluster HDInsight:
1. Em Olá **portal do Azure**, clique em **criar e implantar** na home page do hello fábrica de dados.
2. Em Olá **Editor da fábrica de dados**, clique em **nova computação** do comando Olá barra e selecione **cluster HDInsight** menu hello.
3. Verifique Olá alterações toohello JSON script a seguir:

   1. Para Olá **clusterUri** propriedade, digite a URL de saudação para o HDInsight. Por exemplo: https://<clustername>.azurehdinsight.net/     
   2. Para Olá **UserName** propriedade, digite nome de usuário Olá quem tem acesso toohello HDInsight cluster.
   3. Para Olá **senha** propriedade, digite a senha de saudação do usuário de saudação.
   4. Para Olá **LinkedServiceName** propriedade, digite **AzureStorageLinkedService**.
4. Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.

Consulte os [Serviços vinculados de computação](data-factory-compute-linked-services.md) para obter detalhes.

Em Olá **JSON de pipeline**, use HDInsight (sob demanda ou seu próprio) serviço vinculado:

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a>Criar uma atividade personalizada usando o SDK do .NET
Olá passo a passo neste artigo, você pode criar uma fábrica de dados com um pipeline que usa a atividade personalizada hello usando Olá portal do Azure. saudação de código a seguir mostra como toocreate Olá fábrica de dados usando o SDK do .NET em vez disso. Você pode encontrar mais detalhes sobre como usar o SDK tooprogrammatically criar pipelines no hello [criar um pipeline com atividade de cópia usando API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md) artigo. 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a>Depurar atividade personalizada no Visual Studio
Olá [do Azure Data Factory - ambiente local](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) exemplo no GitHub inclui uma ferramenta que permite a você toodebug atividades personalizadas de .NET dentro do Visual Studio.  


## <a name="sample-custom-activities-on-github"></a>Exemplo de atividades personalizadas no GitHub
| Amostra | Qual atividade personalizada realiza |
| --- | --- |
| [HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample). |Baixa os dados de um armazenamento de Blob usando c# atividade personalizada na fábrica de dados de tooAzure do ponto de extremidade HTTP. |
| [Exemplo de análise de opinião no Twitter](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Invoca um modelo ML do Azure e faz análise de opinião, contagem de pontos, previsão, etc. |
| [Executar Script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample). |Invoca o script de R executando o RScript.exe no seu cluster do HDInsight que já tem o R instalado nele. |
| [Atividade cruzada do .NET no AppDomain](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Usa versões de assembly diferente daquelas usadas pelo iniciador da fábrica de dados de saudação |
| [Reprocessar um modelo no Azure Analysis Services](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  Reprocessar um modelo no Azure Analysis Services. |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
