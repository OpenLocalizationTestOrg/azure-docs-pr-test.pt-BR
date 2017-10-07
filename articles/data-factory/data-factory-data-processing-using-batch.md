---
title: "conjuntos de dados em grande escala aaaProcess usando a fábrica de dados e lote | Microsoft Docs"
description: "Descreve como tooprocess enormes quantidades de dados em uma fábrica de dados do Azure pipeline usando o recurso de processamento paralelo de lote do Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a>Processar conjuntos de dados em larga escala usando o Data Factory e o Lote
Este artigo descreve uma arquitetura de um exemplo de solução que move e processa os conjuntos de dados em larga escala de maneira automática e agendada. Ele também fornece uma solução de saudação tooimplement passo a passo de ponta a ponta usando o Azure Data Factory e lote do Azure.

Este artigo é maior que nossos artigos comuns porque contém um passo a passo de um exemplo de solução inteira. Se você for novo tooBatch e fábrica de dados, você pode aprender sobre esses serviços e como eles funcionam juntos. Se você souber algo sobre serviços hello e está criando/arquitetura de uma solução, você pode se concentrar apenas em Olá [seção arquitetura](#architecture-of-sample-solution) do artigo hello e se você estiver desenvolvendo um protótipo ou uma solução, você também pode desejar tootry out instruções passo a passo em Olá [passo a passo](#implementation-of-sample-solution). Seus comentários sobre esse conteúdo e como usá-lo são bem-vindos.

Primeiro, vamos examinar como serviços de fábrica de dados e lote podem ajudar com o processamento de grandes conjuntos de dados na nuvem hello.     

## <a name="why-azure-batch"></a>Por que usar o Lote do Azure?
Lote do Azure permite que você toorun em larga escala paralelas e alto desempenho HPC (computação) aplicativos com eficiência na nuvem de saudação. É um serviço de plataforma que agenda o trabalho de computação intensa toorun em uma coleção gerenciada de máquinas virtuais, e pode automaticamente escala de computação necessidades de saudação toomeet recursos de seus trabalhos.

Com hello serviço de lote, você define tooexecute de recursos de computação do Azure seus aplicativos em paralelo e em escala. Você pode executar sob demanda ou agendadas trabalhos e você não precisa toomanually criar, configurar e gerenciar um cluster de HPC, máquinas virtuais, redes virtuais ou um trabalho complexo e infraestrutura de agendamento de tarefas.

Consulte Olá artigos a seguir se você não estiver familiarizado com o lote do Azure como ele ajuda com noções básicas sobre arquitetura de saudação/implementação de solução de saudação descrita neste artigo.   

* [Noções básicas de Lote do Azure](../batch/batch-technical-overview.md)
* [Visão geral do recurso de Lote](../batch/batch-api-basics.md)

(opcional) toolearn mais sobre o lote do Azure, consulte Olá [de aprendizado de lote do Azure](https://azure.microsoft.com/documentation/learning-paths/batch/).

## <a name="why-azure-data-factory"></a>Por que usar o Azure Data Factory?
Fábrica de dados é um serviço de integração de dados com base em nuvem que orquestra e automatiza a movimentação de saudação e transformação de dados. Usando o serviço da fábrica de dados hello, você pode criar pipelines de dados gerenciados que movem dados de local e na nuvem de armazenamento de dados centralizado de tooa de repositórios de dados (por exemplo: armazenamento de BLOBs do Azure) e o processo/transformar dados usando serviços como o HDInsight do Azure e o Azure Aprendizado de máquina. Você também pode agendar toorun de pipelines de dados em uma maneira agendada (por hora, diariamente, semanalmente, etc.) e o monitor e gerenciá-los em problemas de tooidentify uma visão e tomar medidas.

Consulte Olá artigos a seguir se você não estiver familiarizado com o Azure Data Factory porque isso ajuda com noções básicas sobre arquitetura de saudação/implementação de solução de saudação descrita neste artigo.  

* [Introdução ao Azure Data Factory](data-factory-introduction.md)
* [Criar seu primeiro pipeline de dados](data-factory-build-your-first-pipeline.md)   

(opcional) toolearn mais sobre o Azure Data Factory, consulte Olá [de aprendizado para o Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).

## <a name="data-factory-and-batch-together"></a>Data Factory e Lote juntos
Fábrica de dados inclui atividades internas, como dados de toocopy/movimentação de atividade de cópia de uma fonte de dados de armazenamento tooa repositório de dados de destino e dados de tooprocess de atividade de Hive usando clusters de Hadoop (HDInsight) no Azure. Confira [Atividades de transformação de dados](data-factory-data-transformation-activities.md) para obter uma lista de atividades de transformação permitidas.

Ele também permite que você toocreate .NET atividades personalizadas toomove ou processam dados com sua própria lógica e executar essas atividades em um cluster Azure HDInsight ou em um pool do Azure Batch de máquinas virtuais. Quando você usa o lote do Azure, você pode configurar a escala Olá pool tooauto (Adicionar ou remover VMs com base na carga de trabalho Olá) com base em uma fórmula que você fornecer.     

## <a name="architecture-of-sample-solution"></a>Arquitetura do exemplo de solução
Embora a arquitetura de saudação descrita neste artigo é para uma solução simples, é cenários toocomplex relevantes, como risco de modelagem, serviços financeiros, processamento de imagem e processamento e análise genoma.

diagrama de saudação ilustra 1) como o Data Factory orquestra a movimentação de dados e processamento e 2) como processa o lote do Azure Olá dados de forma paralela. Download e diagrama de impressão Olá para facilitar a referência (11 x 17 no. ou tamanho A3): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686) (HPC e orquestração de dados usando o Azure Batch e o Data Factory).

[![Diagrama de processamento de dados em larga escala](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)

Olá lista a seguir fornece etapas básicas de saudação do processo de saudação. solução de saudação inclui código e explicações sobre solução de ponta a ponta de saudação toobuild.

1. **Configure o Lote do Azure com um pool de nós de computação (VMs)**. Você pode especificar o número de saudação de nós e o tamanho de cada nó.
2. **Crie uma instância do Azure Data Factory** que está configurada com entidades que representam o armazenamento de blobs do Azure, serviço de computação do Lote do Azure, dados de entrada/saída e um fluxo de trabalho/pipeline com atividades que movem e transformam dados.
3. **Criar uma atividade personalizada do .NET no pipeline da fábrica de dados Olá**. atividade de saudação é o código do usuário que é executado em Olá pool do lote do Azure.
4. **Armazene grandes quantidades de dados de entrada como blobs no armazenamento do Azure**. Os dados são divididos em fatias lógicas (geralmente, por hora).
5. **Fábrica de dados copia os dados que são processados em paralelo** local secundário toohello.
6. **Fábrica de dados é executado usando Olá pool alocada por lote de atividade personalizada do hello**. O Data Factory pode executar atividades simultaneamente. Cada atividade processa uma fatia de dados. Olá resultados são armazenados no armazenamento do Azure.
7. **Fábrica de dados move terceiro local do hello resultados finais tooa**, para distribuição por meio de um aplicativo ou para processamento adicional por outras ferramentas.

## <a name="implementation-of-sample-solution"></a>Implementação da solução de exemplo
solução de exemplo Hello é intencionalmente simple e é tooshow você como toouse conjuntos de dados de tooprocess juntos de fábrica de dados e lote. solução de saudação simplesmente conta o número de saudação de ocorrências de um termo de pesquisa ("Microsoft") nos arquivos de entrada, organizados em uma série de tempo. Ele produz arquivos de toooutput de contagem de saudação.

**Tempo**: se você estiver familiarizado com conceitos básicos do Azure, a fábrica de dados e o lote e tem pré-requisitos concluída Olá listados abaixo, estimamos que esta solução usa toocomplete de 1 a 2 horas.

### <a name="prerequisites"></a>Pré-requisitos
#### <a name="azure-subscription"></a>Assinatura do Azure
Se você não tiver uma assinatura do Azure, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Veja [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="azure-storage-account"></a>Conta de Armazenamento do Azure
Você pode usar uma conta de armazenamento do Azure para armazenar dados de saudação neste tutorial. Se você não tiver uma conta de armazenamento do Azure, consulte o artigo [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account). solução de exemplo Hello usa o armazenamento de blob.

#### <a name="azure-batch-account"></a>Conta do Lote do Azure
Criar uma conta de lote do Azure usando Olá [portal do Azure](http://manage.windowsazure.com/). Consulte [Criar e gerenciar uma conta do Lote do Azure](../batch/batch-account-create-portal.md). Anote a chave de nome e uma conta de conta de lote do Azure do hello. Você também pode usar [AzureRmBatchAccount novo](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate uma conta de lote do Azure. Consulte [Introdução aos cmdlets do PowerShell do Lote do Azure](../batch/batch-powershell-cmdlets-get-started.md) para obter instruções detalhadas sobre como usar esse cmdlet.

solução de exemplo Hello usa dados de tooprocess de lote do Azure (indiretamente por meio de um pipeline da fábrica de dados do Azure) de forma paralela em um pool de nós de computação (uma coleção de máquinas virtuais gerenciada).

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a>Pool de VMs (máquinas virtuais) do Lote do Azure
Crie um **pool de Lote do Azure** com pelo menos dois nós de computação.

1. Em Olá [portal do Azure](https://portal.azure.com), clique em **procurar** no hello menus à esquerda e clique em **contas em lotes**.
2. Selecione sua saudação do lote do Azure conta tooopen **conta em lotes** folha.
3. Clique no bloco **Pools** .
4. Em Olá **Pools** folha, clique no botão Adicionar na saudação da barra de ferramentas tooadd um pool.
   1. Insira uma ID para o pool de saudação (**ID do Pool**). Saudação de Observação **ID do pool de saudação**; é necessário ao criar a solução de fábrica de dados hello.
   2. Especifique **Windows Server 2012 R2** para configuração da família de sistemas operacionais de saudação.
   3. Selecione um **camada de preços de nó**.
   4. Digite **2** como valor para Olá **destino dedicado** configuração.
   5. Digite **2** como valor para Olá **tarefas máxima por nó** configuração.
   6. Clique em **Okey** toocreate pool de saudação.

#### <a name="azure-storage-explorer"></a>Gerenciador de Armazenamento do Azure
[Azure Storage Explorer 6 (ferramenta)](https://azurestorageexplorer.codeplex.com/) ou [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (da ClumsyLeaf Software). Você pode usar essas ferramentas para inspecionar e alterar dados de saudação em seus projetos de armazenamento do Azure, incluindo os logs de saudação de seus aplicativos hospedados em nuvem.

1. Crie um contêiner chamado **mycontainer** com acesso privado (sem acesso anônimo)
2. Se você estiver usando **CloudXplorer**, criar pastas e subpastas com hello estrutura a seguir:

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   `Inputfolder` e `outputfolder` são pastas de nível superior no `mycontainer`. Olá `inputfolder` tem subpastas com carimbos de data e hora (AAAA-MM-DD-HH).

   Se você estiver usando **Azure Storage Explorer**, na próxima etapa de saudação, você precisa de arquivos tooupload com nomes: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` e assim por diante. Esta etapa cria automaticamente as pastas de saudação.
3. Criar um arquivo de texto **arquivo.txt** em seu computador com o conteúdo com a palavra-chave de saudação **Microsoft**. Por exemplo: "testar a atividade personalizada Microsoft testar atividade personalizada Microsoft".
4. Carregar Olá arquivo toohello pastas entradas no armazenamento de BLOBs do Azure, a seguir.

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   Se você estiver usando **Azure Storage Explorer**, carregue o arquivo hello **arquivo.txt** muito**mycontainer**. Clique em **cópia** em Olá barra de ferramentas toocreate uma cópia de blob de saudação. Em Olá **cópia Blob** caixa de diálogo, alteração Olá **nome de blob de destino** muito`inputfolder/2015-11-16-00/file.txt`. Repita essa etapa toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` e assim por diante. Essa ação cria automaticamente as pastas de saudação.
5. Crie outro contêiner chamado `customactivitycontainer`. Carregar o contêiner do toothis de arquivos zip hello atividade personalizada.

#### <a name="visual-studio"></a>Visual Studio
Instale o Microsoft Visual Studio 2012 ou posterior toocreate Olá personalizado lote atividade toobe usado em Olá solução da fábrica de dados.

### <a name="high-level-steps-toocreate-hello-solution"></a>Solução de saudação toocreate etapas de alto nível
1. Crie uma atividade personalizada que contém a lógica de processamento de dados de saudação.
2. Crie uma fábrica de dados do Azure que usa a atividade personalizada hello:

### <a name="create-hello-custom-activity"></a>Criar atividade personalizada Olá
Hello atividade personalizada de fábrica de dados é o núcleo de saudação desta solução de exemplo. solução de exemplo Hello usa uma atividade personalizada do lote do Azure toorun hello. Consulte [usar atividades personalizadas em um pipeline da fábrica de dados do Azure](data-factory-use-custom-activities.md) para atividades personalizadas do toodevelop Olá informações básicas e use-os no Azure Data Factory pipelines.

toocreate uma atividade personalizada do .NET que podem ser usados em um pipeline da fábrica de dados do Azure, você precisa toocreate um **biblioteca de classes .NET** projeto com uma classe que implementa que **IDotNetActivity** interface. Essa interface tem apenas um método: **Execute**. Aqui está a assinatura de saudação do método hello:

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

método Hello tem alguns componentes principais que você precisa toounderstand.

* método Hello usa quatro parâmetros:

  1. **linkedServices**. Uma lista enumerável de serviços vinculados que vinculam fontes de dados de entrada/saída (por exemplo: armazenamento de BLOBs do Azure) toohello fábrica de dados. Neste exemplo, há apenas um serviço vinculado do tipo armazenamento do Azure usado para entrada e saída.
  2. **conjuntos de dados**. É uma lista enumerável de conjuntos de dados. Você pode usar este locais de saudação do parâmetro tooget e esquemas definidos pelos conjuntos de dados de entrada e saídos.
  3. **atividade**. Esse parâmetro representa Olá computação entidade atual - nesse caso, um serviço de lote do Azure.
  4. **logger**. permite a agente Olá para que escrever comentários de depuração essa superfície como hello "Usuário" fazer logon Olá pipeline.
* método Hello retorna um dicionário que pode ser atividades personalizadas toochain usados juntos em um futuro hello. Este recurso ainda não foi implementado, isso retornará um dicionário vazio do método hello.

#### <a name="procedure-create-hello-custom-activity"></a>Procedimento: Criar atividade personalizada Olá
1. Crie um projeto de Biblioteca de Classes .NET no Visual Studio.

   1. Inicie o **Visual Studio 2012**/**2013/2015**.
   2. Clique em **arquivo**, ponto muito**novo**e clique em **projeto**.
   3. Expanda **Modelos** e selecione **Visual C\#**. Neste passo a passo, você pode usar C\#, mas você pode usar qualquer atividade personalizada do .NET idioma toodevelop hello.
   4. Selecione **biblioteca de classes** da lista de saudação de tipos de projeto em saudação à direita.
   5. Digite **MyDotNetActivity** para Olá **nome**.
   6. Selecione **c:\\ADF** para Olá **local**. Criar pasta Olá **ADF** se ele não existe.
   7. Clique em **Okey** toocreate projeto de saudação.
2. Clique em **ferramentas**, ponto muito**NuGet Package Manager**e clique em **Package Manager Console**.
3. Em Olá **Package Manager Console**, execute Olá após o comando tooimport **Microsoft.Azure.Management.DataFactories**.

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Saudação de importação **armazenamento do Azure** pacote do NuGet no projeto toohello. Você precisa deste pacote porque você usar a API de armazenamento de Blob Olá neste exemplo.

    ```powershell
    Install-Package Azure.Storage
    ```
5. Adicione o seguinte Olá **usando** diretivas toohello fonte arquivo hello projeto.

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Alterar o nome de saudação do hello **namespace** muito**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Alterar o nome de saudação da classe Olá muito**MyDotNetActivity** e ele derivam Olá **IDotNetActivity** interface conforme mostrado abaixo.

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Saudação de implementar (Adicionar) **Execute** método hello **IDotNetActivity** interface toohello **MyDotNetActivity** Olá cópia e de classe, método de toohello de código de exemplo a seguir. Consulte Olá [executar método](#execute-method) seção para obter explicação para lógica de saudação usada nesse método.

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
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
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
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
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
9. Adicione Olá classe do auxiliar métodos toohello a seguir. Esses métodos são chamados pelo Olá **Execute** método. Mais importante, Olá **Calculate** método isola código Olá que itera por meio de cada blob.

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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    Olá **GetFolderPath** método retorna a pasta de toohello de caminho de saudação que Olá dataset pontos tooand Olá **GetFileName** método retorna o nome de Olá Olá/do arquivo de blob que Olá pontos de conjunto de dados.

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    Olá **Calculate** método calcula o número de saudação de instâncias da palavra-chave **Microsoft** nos arquivos de entrada hello (blobs na pasta Olá). termo de pesquisa da saudação ("Microsoft") é embutido em código hello.

1. Compile o projeto de saudação. Clique em **criar** de saudação menu e clique em **compilar solução**.
2. Iniciar **Windows Explorer**e navegue muito**bin\\depurar** ou **bin\\versão** pasta dependendo do tipo de saudação da compilação.
3. Criar um arquivo zip **MyDotNetActivity.zip** que contém todos os binários de saudação em Olá  **\\bin\\depurar** pasta. Talvez você queira Olá tooinclude MyDotNetActivity. **pdb** arquivos de forma que você obter detalhes adicionais, como o número da linha no código-fonte Olá que causou o problema de saudação quando ocorre uma falha.

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. Carregar **MyDotNetActivity.zip** como um contêiner de blob do blob toohello: `customactivitycontainer` em hello Azure armazenamento de blob que Olá **StorageLinkedService** serviço em Olá vinculado  **ADFTutorialDataFactory** usa. Criar contêiner de blob Olá `customactivitycontainer` se ele ainda não existir.

#### <a name="execute-method"></a>Método Execute
Esta seção fornece mais detalhes e observações sobre o código Olá Olá método Execute.

1. membros de saudação para iteração pela coleção de entrada hello são encontrados em Olá [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace. Iteração pela coleção de blob Olá requer o uso de saudação **BlobContinuationToken** classe. Em essência, você deve usar um, faça-durante o loop com token hello como mecanismo de saudação para sair do loop de saudação. Para obter mais informações, consulte [como toouse armazenamento de BLOBs no .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Um loop básico é mostrado aqui:

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   Consulte a documentação para Olá Olá [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) método para obter detalhes.
2. Olá código para trabalhar com o conjunto de saudação de blobs logicamente fica dentro de saudação fazer-loop while. Em Olá **Execute** método, proceda de saudação-enquanto o loop passa a lista de saudação de blobs método tooa chamado **Calculate**. método Hello retorna uma variável de cadeia de caracteres denominada **saída** que é resultado de saudação de ter iteração de todos os blobs Olá no segmento de saudação.

   Retorna Olá número de ocorrências do termo de pesquisa da saudação (**Microsoft**) no blob Olá passada toohello **Calculate** método.

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. Uma vez Olá **Calculate** método trabalhou hello, ele deve ser escrito tooa novo blob. Portanto, para cada conjunto de blobs processados, um novo blob pode ser gravado com resultados de saudação. toowrite tooa novo blob, o primeiro conjunto de saída de saudação de localizar.

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. código de saudação também chama um método auxiliar: **GetFolderPath** caminho da pasta tooretrieve hello (nome do contêiner de armazenamento Olá).

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   Olá **GetFolderPath** conversões Olá tooan de objeto do conjunto de dados AzureBlobDataSet, que tem uma propriedade denominada FolderPath.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. saudação de chamadas de código Olá **GetFileName** método tooretrieve Olá arquivo nome (blob). código de saudação é semelhante toohello acima caminho da pasta código tooget hello.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. nome de saudação do arquivo hello é escrito, criando um objeto URI. construtor URI Olá usa Olá **BlobEndpoint** nome da propriedade tooreturn Olá contêiner. nome de arquivo e caminho da pasta de saudação são adicionados tooconstruct o URI do blob de saída de hello.  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. nome de saudação do arquivo hello foi gravado e agora você pode criar a cadeia de caracteres de saída de saudação do hello **Calculate** novo blob tooa do método:

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a>Criar hello fábrica de dados
Em Olá [Criar atividade personalizada Olá](#create-the-custom-activity) seção, você criou uma atividade personalizada e arquivo zip de saudação carregado com binários e hello PDB arquivo tooan contêiner de BLOBs do Azure. Nesta seção, você cria um Azure **fábrica de dados** com um **pipeline** que usa Olá **atividade personalizada**.

Olá conjunto de dados de entrada para atividade personalizada Olá representa blobs hello (arquivos) na pasta de entrada hello (`mycontainer\\inputfolder`) no armazenamento de blob. conjunto de dados de saída Hello atividade Olá representa Olá blobs de saída na pasta de saída de hello (`mycontainer\\outputfolder`) no armazenamento de blob.

Remova um ou mais arquivos em pastas de entrada hello:

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

Por exemplo, remova um arquivo (arquivo. txt) com hello após o conteúdo em cada uma das pastas de saudação.

```
test custom activity Microsoft test custom activity Microsoft
```

Cada pasta de entrada corresponde tooa fatia na fábrica de dados do Azure, mesmo se a pasta de saudação tem 2 ou mais arquivos. Quando cada fatia é processada pelo pipeline hello, atividade personalizada Olá itera em todos os blobs de saudação na pasta de entrada hello essa fatia.

Você verá cinco arquivos de saída com hello mesmo conteúdo. Por exemplo, o arquivo de saída de saudação do processamento de arquivo hello na pasta Olá 2015-11-16-00 tem Olá conteúdo a seguir:

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

Se você remover vários arquivos (arquivo. txt, file2.txt, file3.txt) com hello mesmo conteúdo pasta entrada toohello, consulte Olá conteúdo no arquivo de saída de hello a seguir. Cada pasta (2015-11-16-00, etc.) corresponde a fatia tooa neste exemplo, embora pasta Olá tem vários arquivos de entrada.

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

arquivo de saída Olá tem três linhas agora, uma para cada arquivo de entrada (blob) na pasta Olá associado a fatia de saudação (2015-11-16-00).

Uma tarefa é criada para cada execução de atividade. Neste exemplo, há apenas uma atividade no pipeline de saudação. Quando uma fatia é processada pelo pipeline Olá, atividade personalizada Olá é executado na fatia da saudação tooprocess lote do Azure. Uma vez que há cinco intervalos (cada fatia pode ter vários blobs ou arquivos), há cinco tarefas criadas no Azure Batch. Quando uma tarefa é executada em lote, é realmente hello atividade personalizada que está sendo executado.

Olá, seguindo as instruções passo a passo fornece detalhes adicionais.

#### <a name="step-1-create-hello-data-factory"></a>Etapa 1: Criar a fábrica de dados Olá
1. Depois de fazer logon em toohello [portal do Azure](https://portal.azure.com/), Olá seguintes etapas:

   1. Clique em **novo** no menu esquerdo hello.
   2. Clique em **dados + análise** em Olá **novo** folha.
   3. Clique em **Data Factory** em Olá **análises de dados** folha.
2. Em Olá **nova fábrica de dados** folha, digite **CustomActivityFactory** para Olá nome. nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo. Se você receber o erro Olá: **"CustomActivityFactory" nome da fábrica de dados não está disponível**, alterar nome Olá Olá da fábrica de dados (por exemplo, **yournameCustomActivityFactory**) e tente criar novamente.
3. Clique em **NOME DO GRUPO DE RECURSOS**para selecionar um grupo de recursos existente ou criar um.
4. Verifique se que você está usando a assinatura correta hello e região onde você deseja Olá toobe de fábrica de dados criado.
5. Clique em **criar** em Olá **nova fábrica de dados** folha.
6. Você verá a fábrica de dados hello está sendo criada no hello **painel** de saudação portal do Azure.
7. Depois de fábrica de dados Olá tiver sido criada com êxito, você ver a página de fábrica de dados hello, que mostra Olá conteúdo Olá da fábrica de dados.

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a>Etapa 2: Criar serviços vinculados
Serviços vinculados vincular armazenamentos de dados ou de computação serviços tooan data factory do Azure. Nesta etapa, você vincular seu **armazenamento do Azure** conta e **do Azure Batch** fábrica de dados de tooyour de conta.

#### <a name="create-azure-storage-linked-service"></a>Criar o serviço vinculado do armazenamento do Azure
1. Clique em Olá **autor e implantar** bloco Olá **DATA FACTORY** folha para **CustomActivityFactory**. Você verá Olá Editor da fábrica de dados.
2. Clique em **novo repositório de dados** Olá barra de comandos e escolha **armazenamento do Azure.** Você deve ver Olá script JSON para a criação de um armazenamento do Azure vinculada serviço no editor de saudação.

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. Substituir **nome da conta** com nome de saudação da sua conta de armazenamento do Azure e **chave de conta** com a chave de acesso de saudação do Olá conta de armazenamento do Azure. toolearn como tooget seu armazenamento acessar chave, consulte [exibir, copiar e regenerar as contas de armazenamento de chaves de acesso](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

4. Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a>Crie o serviço vinculado do Lote do Azure
Nesta etapa, você cria um serviço vinculado para o **do Azure Batch** conta que seja usada toorun Olá fábrica de dados personalizado de atividades.

1. Clique em **nova computação** Olá barra de comandos e escolha **lote do Azure.** Você deve ver Olá script JSON para a criação de um lote do Azure vinculado de serviço no editor de saudação.
2. No script JSON da saudação:

   1. Substituir **nome da conta** com nome de saudação da sua conta de lote do Azure.
   2. Substituir **chave de acesso** com chave de acesso de saudação do hello conta de lote do Azure.
   3. Insira a ID de saudação do pool de saudação para hello **poolName** propriedade**.** Para essa propriedade, você pode especificar o nome do pool ou o ID do pool.
   4. Insira o URI de lote de saudação para Olá **batchUri** propriedade JSON.

      > [!IMPORTANT]
      > Olá **URL** de saudação **folha de conta de lote do Azure** está em Olá formato a seguir: \<accountname\>.\< região\>. batch.azure.com. Para Olá **batchUri** propriedade no hello JSON, é necessário muito**remover "accountname".** de URL hello. Exemplo: `"batchUri": "https://eastus.batch.azure.com"`.
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      Para Olá **poolName** propriedade, você também pode especificar a ID de saudação do pool de saudação em vez do nome de saudação do pool de saudação de.

      > [!NOTE]
      > Olá serviço da fábrica de dados não dá suporte uma opção sob demanda para o lote do Azure como faz para HDInsight. Você só pode usar seu próprio pool do Azure Batch em um Azure Data Factory.
      >
      >
   5. Especifique **StorageLinkedService** para Olá **linkedServiceName** propriedade. Você criou esse serviço vinculado na etapa anterior hello. Esse armazenamento é usado como uma área de preparação para arquivos e logs.
3. Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.

#### <a name="step-3-create-datasets"></a>Etapa 3: Criar conjuntos de dados
Nesta etapa, você cria conjuntos de dados toorepresent entrada e saída de dados.

#### <a name="create-input-dataset"></a>Criar conjunto de dados de entrada
1. Em Olá **Editor** para Olá fábrica de dados, clique em **novo conjunto de dados** botão na barra de ferramentas hello e clique em **armazenamento de BLOBs do Azure** do menu suspenso de saudação.
2. Substitua Olá JSON no painel direito Olá Olá trecho JSON a seguir:

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
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

    Você cria um pipeline posteriormente neste passo a passo com hora de início: 2015-11-16T00:00:00Z e final: 2015-11-16T05:00:00Z. São dados agendados tooproduce **por hora**, portanto, há 5 intervalos de entrada/saída (entre **00**: 00:00 -\> **05**: 00:00).

    Olá **frequência** e **intervalo** para o conjunto de dados de entrada hello está definido muito**hora** e **1**, que significa que Olá entrada fatia está disponível por hora.

    Aqui estão os horários de início de saudação de cada fatia, que são representados por **SliceStart** variável do sistema em Olá acima trecho JSON.

    | **Fatia** | **Hora de início**          |
    |-----------|-------------------------|
    | 1         | 2015-11-16T**00**:00:00 |
    | 2         | 2015-11-16T**01**:00:00 |
    | 3         | 2015-11-16T**02**:00:00 |
    | 4         | 2015-11-16T**03**:00:00 |
    | 5         | 2015-11-16T**04**:00:00 |

    Olá **folderPath** é calculado usando a parte de ano, mês, dia e hora Olá Olá fatia da hora de início (**SliceStart**). Portanto, aqui está como uma pasta de entrada é mapeada tooa fatia.

    | **Fatia** | **Hora de início**          | **Pasta de entrada**  |
    |-----------|-------------------------|-------------------|
    | 1         | 2015-11-16T**00**:00:00 | 2015-11-16-**00** |
    | 2         | 2015-11-16T**01**:00:00 | 2015-11-16-**01** |
    | 3         | 2015-11-16T**02**:00:00 | 2015-11-16-**02** |
    | 4         | 2015-11-16T**03**:00:00 | 2015-11-16-**03** |
    | 5         | 2015-11-16T**04**:00:00 | 2015-11-16-**04** |

1. Clique em **implantar** Olá toocreate da barra de ferramentas e implantar Olá **InputDataset** tabela.

#### <a name="create-output-dataset"></a>Criar conjunto de dados de saída
Nesta etapa, você deve criar outro conjunto de dados de tipo de dados de saída AzureBlob toorepresent hello.

1. Em Olá **Editor** para Olá fábrica de dados, clique em **novo conjunto de dados** botão na barra de ferramentas hello e clique em **armazenamento de BLOBs do Azure** do menu suspenso de saudação.
2. Substitua Olá JSON no painel direito Olá Olá trecho JSON a seguir:

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
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

    Um blob/arquivo de saída é gerado para cada fatia de entrada. Aqui está como um arquivo de saída é chamado para cada fatia. Todos os arquivos de saída de hello são gerados em uma pasta de saída: `mycontainer\\outputfolder`.

    | **Fatia** | **Hora de início**          | **Arquivo de saída**       |
    |-----------|-------------------------|-----------------------|
    | 1         | 2015-11-16T**00**:00:00 | 2015-11-16-**00.txt** |
    | 2         | 2015-11-16T**01**:00:00 | 2015-11-16-**01.txt** |
    | 3         | 2015-11-16T**02**:00:00 | 2015-11-16-**02.txt** |
    | 4         | 2015-11-16T**03**:00:00 | 2015-11-16-**03.txt** |
    | 5         | 2015-11-16T**04**:00:00 | 2015-11-16-**04.txt** |

    Lembre-se de que todos os arquivos em uma pasta de entrada de hello (por exemplo: 2015-11-16-00) fazem parte de uma fatia com hora de início da saudação: 2015-11-16-00. Quando essa fatia é processada, a atividade personalizada Olá verifica cada arquivo e produz uma linha no arquivo de saída de hello com número de saudação de ocorrências do termo de pesquisa ("Microsoft"). Se houver três arquivos na pasta Olá 2015-11-16-00, há três linhas no arquivo de saída de hello: 00.txt 2015-11-16.

1. Clique em **implantar** Olá toocreate da barra de ferramentas e implantar Olá **OutputDataset**.

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a>Etapa 4: Criar e executar o pipeline de saudação com atividade personalizada
Nesta etapa, você pode criar um pipeline com uma atividade, atividade personalizada de saudação criado anteriormente.

> [!IMPORTANT]
> Se você ainda não carregou Olá **arquivo.txt** tooinput pastas no contêiner de blob hello, fazer isso antes de criar o pipeline de saudação. Olá **isPaused** propriedade é definida toofalse no pipeline Olá JSON, para o pipeline de saudação seja executada imediatamente como Olá **iniciar** data estiver no hello anterior.
>
>

1. No hello Editor da fábrica de dados, clique em **novo pipeline** na barra de comandos de saudação. Se você não vir o comando hello, clique em **... (Reticências)**  toosee-lo.
2. Substitua Olá JSON no painel direito Olá Olá script JSON a seguir:

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   Observe Olá pontos a seguir:

   * Há apenas uma atividade no pipeline hello e que é do tipo: **DotNetActivity**.
   * **AssemblyName** é definir o nome toohello Olá DLL: **MyDotNetActivity.dll**.
   * **Ponto de entrada** está definido muito**MyDotNetActivityNS.MyDotNetActivity**. Ele é basicamente \<namespace\>.\<classname\> em seu código.
   * **PackageLinkedService** está definido muito**StorageLinkedService** que aponte toohello armazenamento de blob que contém o arquivo de zip hello atividade personalizado. Se você estiver usando diferentes contas de armazenamento do Azure para arquivos de entrada/saída e o arquivo de zip hello atividade personalizada, você tem toocreate outro armazenamento do Azure serviço vinculado. Este artigo pressupõe que você está usando Olá a mesma conta de armazenamento do Azure.
   * **PackageFile** está definido muito**customactivitycontainer/MyDotNetActivity.zip**. Formato de saudação: \<containerforthezip\>/\<nameofthezip.zip\>.
   * atividades personalizadas Olá **InputDataset** como entrada e **OutputDataset** como saída.
   * Olá **linkedServiceName** propriedade de atividade personalizada Olá aponta toohello **AzureBatchLinkedService**, que informa ao Azure Data Factory dessa atividade personalizada Olá precisa toorun em lote do Azure.
   * Olá **simultaneidade** configuração é importante. Se você usar o valor padrão de saudação, que é 1, mesmo se você tiver 2 ou mais nós de computação no pool de lote do Azure hello, fatias de saudação são processadas uma após a outra. Portanto, você não está aproveitando as vantagens da capacidade de processamento paralelo de saudação do lote do Azure. Se você definir **simultaneidade** tooa maior valor, digamos que 2, isso significa que dois fatias (corresponde tootwo tarefas em lote do Azure) podem ser processadas em Olá a mesma hora, nesse caso, as duas máquinas virtuais de saudação de saudação do Azure Batch pool são utilizados. Portanto, defina a propriedade de simultaneidade de saudação adequadamente.
   * Apenas uma tarefa (fatia) é executada em uma VM a qualquer momento por padrão. Olá razão é que, por padrão, hello **máximo de tarefas por VM** é definir too1 para um pool de lote do Azure. Como parte dos pré-requisitos, você criou um pool com too2 de definir essa propriedade, para dois intervalos de fábrica de dados podem ser executados em uma VM em Olá simultaneamente.

    -   **isPaused** propriedade está definida toofalse por padrão. Olá pipeline é executado imediatamente neste exemplo como fatias Olá começam em Olá anterior. Você pode configurar o pipeline de saudação essa propriedade tootrue toopause e defina-a como toorestart toofalse back.

    -   Olá **iniciar** tempo e **final** vezes são separadas de cinco horas e fatias são produzidas por hora, para cinco fatias são produzidas pelo pipeline de saudação.

1. Clique em **implantar** no pipeline de saudação toodeploy da barra de comandos de saudação.

#### <a name="step-5-test-hello-pipeline"></a>Etapa 5: Testar o pipeline de saudação
Nesta etapa, você pode testar pipeline Olá soltando arquivos em pastas de entrada hello. Vamos começar com o pipeline de saudação de teste com um arquivo por uma pasta de entrada.

1. Na folha da fábrica de dados Olá no hello portal do Azure, clique em **diagrama**.

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. No modo de exibição de diagrama hello, clique duas vezes no conjunto de dados de entrada: **InputDataset**.

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. Você deve ver Olá **InputDataset** folha com todas as cinco frações pronta. Saudação de aviso **hora de início da FATIA** e **hora de término da FATIA** para cada fatia.

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. Em Olá **exibição de diagrama**, agora clique **OutputDataset**.
5. Você deve ver cinco fatias de saída Olá estão em estado pronto do hello se já foi produzidos.

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. Saudação de tooview portal do Azure Use **tarefas** associado Olá **fatias** e ver quais VM cada fatia foi executada. Confira a seção [Integração de Data Factory e Lote](#data-factory-and-batch-integration) para obter detalhes.
7. Você deve ver arquivos de saída de saudação em Olá `outputfolder` de `mycontainer` no seu Azure armazenamento de blob.

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   Você deve ver cinco arquivos de saída, um para cada fatia de entrada. Cada saudação de saída de arquivo deve ter conteúdo toohello semelhante de saída a seguir:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   Olá diagrama a seguir ilustra como fatias da fábrica de dados de saudação mapeiam tootasks em lote do Azure. Neste exemplo, uma fatia tem apenas uma execução.

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. Agora, vamos tentar com vários arquivos em uma pasta. Criar arquivos: **file2.txt**, **file3.txt**, **file4.txt**, e **file5.txt** com hello mesmo conteúdo como arquivo. txt na pasta hello: **2015-11-06-01**.
9. Na pasta de saída de hello, **excluir** arquivo de saída de hello: **2015-11-16-01.txt**.
10. Agora, em Olá **OutputDataset** folha, a fatia de saudação atalho com **hora de início da FATIA** definido muito**16/11/2015 01:00:00 AM**e clique em **executar**fatia Olá toorerun/re-process. Agora, a fatia Olá tem cinco arquivos em vez de um arquivo.

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. Após a execução de fatia hello e seu status é **pronto**, verificar Olá conteúdo no arquivo de saída Olá para esta fatia (**2015-11-16-01.txt**) no hello `outputfolder` de `mycontainer` em seu armazenamento de blob. Deve haver uma linha para cada arquivo de fatia hello.

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> Se você não tiver excluído 2015 de arquivo de saída Olá-11-16-01.txt antes de tentar com cinco arquivos de entrada, você verá uma linha da fatia anterior de saudação executar e cinco linhas de fatia atual de saudação executar. Por padrão, o conteúdo de saudação é toooutput acrescentados arquivo se ele já existe.
>
>

#### <a name="data-factory-and-batch-integration"></a>Integração de Data Factory e Lote
Olá serviço da fábrica de dados cria um trabalho em lote do Azure com o nome da saudação: `adf-poolname:job-xxx`.

![Trabalhos de Azure Data Factory - Lote](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

Uma tarefa no trabalho de saudação é criada para cada execução de atividade de uma fatia. Se houver 10 toobe pronto fatias processadas, 10 tarefas são criadas no trabalho de saudação. Você pode ter mais de uma fatia em execução em paralelo, se você tiver vários nós de computação no pool de saudação. Se o máximo de tarefas por hello computação de conjunto de nós é muito > 1, pode haver mais de uma fatia em execução no hello computação mesmo.

Neste exemplo, há cinco fatias, então cinco tarefas no Azure Batch. Com hello **simultaneidade** definido muito**5** em Olá pipeline JSON no Azure Data Factory e **máximo de tarefas por VM** definido muito**2** em lote do Azure pool com **2** VMs, Olá tarefas é executada rápida (Verifique as horas de início e término para tarefas).

Use o trabalho em lotes do hello tooview portal hello e suas tarefas associadas a saudação **fatias** e ver quais VM cada fatia foi executada.

![Tarefas do trabalho de Azure Data Factory - Lote](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a>Depurar pipeline Olá
A depuração consiste em algumas técnicas básicas:

1. Se a fatia de entrada hello não está definida muito**pronto**, confirme se a estrutura de pasta de entrada hello está correta e arquivo. txt existe em pastas de entrada hello.

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. Em Olá **Execute** método de sua atividade personalizada, use Olá **IActivityLogger** informações toolog do objeto que ajuda você a solucionar problemas. mensagens de saudação conectada aparecem no usuário Olá\_0. arquivo de log.

   Em Olá **OutputDataset** folha, clique em Olá fatia toosee Olá **FATIA de dados** folha para essa fatia. Você vê as **execuções de atividade** para essa fatia. Você deve ver uma atividade executar fatia hello. Se você clicar em **executar** na barra de comandos hello, você pode iniciar outra atividade executada para Olá mesma fatia.

   Quando você clica em execução da atividade hello, você vê Olá **detalhes de execução da atividade** folha com uma lista de arquivos de log. Consulte as mensagens registradas no hello **usuário\_0. log** arquivo. Quando ocorre um erro, você verá três execuções de atividade porque a contagem de repetição de saudação é definida too3 Olá pipeline/atividade JSON. Quando você clica em execução da atividade Olá, você ver arquivos de log de saudação que você pode examinar o erro de saudação tootroubleshoot.

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   Na lista de saudação de arquivos de log, clique em Olá **0.log usuário**. No painel direito da saudação são resultados de saudação do uso Olá **IActivityLogger.Write** método.

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   Verifique o system-0.log para quaisquer mensagens de erro e exceções do sistema.

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. Incluir Olá **PDB** no arquivo zip de saudação do arquivo para que os detalhes do erro Olá contêm informações como **pilha de chamadas** quando ocorre um erro.
4. Todos Olá arquivos contidos no arquivo zip Olá para atividade de saudação personalizada deve estar no hello **nível superior** sem subpastas.

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. Certifique-se de que Olá **assemblyName** (MyDotNetActivity.dll) **entryPoint** (MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip), e **packageLinkedService** (deve Azure ponto toohello armazenamento de blob que contém o arquivo zip de saudação) são definidos valores toocorrect.
6. Se você fixa uma fatia de saudação tooreprocess erro e quiser, clique com botão direito fatia Olá Olá **OutputDataset** folha e clique em **executar**.

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > Você verá um **contêiner** no Armazenamento de blobs do Azure chamado `adfjobs`. Este contêiner não é excluído automaticamente, mas você poderá excluí-la com segurança depois de concluir a solução de saudação testes. Da mesma forma, a saudação solução da fábrica de dados cria um lote do Azure **trabalho** denominado: `adf-\<pool ID/name\>:job-0000000001`. Você pode excluir esse trabalho depois de você testar a solução de saudação se desejar.
   >
   >
7. atividade personalizada Olá não usa Olá **App. config** arquivo do seu pacote. Portanto, se seu código lê qualquer cadeia de caracteres de conexão do arquivo de configuração hello, ele não funciona em tempo de execução. Olá prática recomendada ao usar o lote do Azure é toohold qualquer segredos em um **KeyVault Azure**, use um keyvault do serviço com base em certificado principal tooprotect hello e distribuir o pool do lote Olá certificado tooAzure. Hello atividade personalizada do .NET pode acessar segredos de saudação KeyVault em tempo de execução. Essa solução é um arquivo genérico e pode ser dimensionado tooany tipo de segredo, não apenas a cadeia de conexão.

    Há uma solução mais fácil (mas não é uma prática recomendada): você pode criar um **serviço vinculado do SQL Azure** com configurações de cadeia de caracteres de conexão, criar um conjunto de dados que usa Olá serviço vinculado e cadeia Olá conjunto de dados como um conjunto de dados de entrada fictício toohello atividade personalizada de .NET. Você pode então Olá de acesso vinculadas cadeia de caracteres de conexão do serviço no código do hello atividade personalizada e deve funcionar bem em tempo de execução.  

#### <a name="extend-hello-sample"></a>Estender o exemplo hello
Você pode estender esse exemplo toolearn mais sobre os recursos do Azure Data Factory e lote do Azure. Por exemplo, tooprocess fatias em um intervalo de tempo diferentes, Olá etapas a seguir:

1. Adicionar Olá seguintes subpastas Olá `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 e coloque arquivos de entrada nessas pastas. Altere a hora de término Olá para o pipeline de saudação do `2015-11-16T05:00:00Z` muito`2015-11-16T10:00:00Z`. Em Olá **exibição de diagrama**, clique duas vezes em Olá **InputDataset**e confirme que as fatias de entrada hello estão prontas. Clique duas vezes em **OuptutDataset** toosee estado de saudação de fatias de saída. Se eles estiverem no estado pronto, verifique Olá a pasta de saída para arquivos de saída de hello.
2. Aumentar ou diminuir Olá **simultaneidade** configuração toounderstand como ele afeta o desempenho de saudação da sua solução, especialmente Olá processamento que ocorre em lote do Azure. (Consulte a etapa 4: criar e executar o pipeline de saudação para saber mais sobre Olá **simultaneidade** configuração.)
3. Crie um pool com **Máximo de tarefas por VM**maior/menor. toouse Olá novo pool é criado, saudação de atualização de serviço vinculado do Azure Batch na solução de fábrica de dados hello. (Consulte a etapa 4: criar e executar o pipeline de saudação para saber mais sobre Olá **máximo de tarefas por VM** configuração.)
4. Crie um pool do Lote do Azure com o recurso **dimensionar automaticamente** . Dimensionar automaticamente nós de computação em um pool de lote do Azure é o ajuste dinâmico de saudação de energia usada por seu aplicativo de processamento. 

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
5. Solução de exemplo hello, Olá **Execute** método invoca Olá **Calculate** método que processa uma fatia de dados de entrada tooproduce uma fatia de dados de saída. Você pode escrever seu próprio método tooprocess dados de entrada e substitua a chamada de método hello Calculate no método de execução de saudação com um método de tooyour de chamada.

### <a name="next-steps-consume-hello-data"></a>Próximas etapas: consumir dados Olá
Depois de processar dados, é possível consumi-lo com ferramentas online como o **Microsoft Power BI**. Aqui estão os links toohelp entender o Power BI e como toouse-lo no Azure:

* [Explorar um conjunto de dados no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [Guia de Introdução com hello Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [Atualizar dados no Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [Azure e Power BI - visão geral básica](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a>Referências
* [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)

  * [Introdução tooAzure serviço da fábrica de dados](data-factory-introduction.md)
  * [Introdução ao Data Factory do Azure](data-factory-build-your-first-pipeline.md)
  * [Usar atividades personalizadas em um pipeline do Data Factory do Azure](data-factory-use-custom-activities.md)
* [Lote do Azure](https://azure.microsoft.com/documentation/services/batch/)

  * [Noções básicas de Lote do Azure](../batch/batch-technical-overview.md)
  * [Visão geral dos recursos do Lote do Azure](../batch/batch-api-basics.md)
  * [Criar e gerenciar conta de lote do Azure no portal do Azure de saudação](../batch/batch-account-create-portal.md)
  * [Introdução ao .NET da Biblioteca de Lote do Azure](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
