---
title: aaaCreate pipelines de dados usando o SDK .NET do Azure | Microsoft Docs
description: "Saiba como tooprogrammatically criar, monitorar e gerenciar as fábricas de dados do Azure usando o SDK de fábrica de dados."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a>Criar, monitorar e gerenciar data factories do Azure usando o SDK do .NET do Azure Data Factory
## <a name="overview"></a>Visão geral
Você pode criar, monitorar e gerenciar as Data Factory do Azure programaticamente usando o SDK do .NET da Data Factory. Este artigo contém uma explicação passo a passo que você pode seguir toocreate um aplicativo de console .NET de exemplo que cria e monitora uma fábrica de dados. 

> [!NOTE]
> Este artigo não aborda Olá todos os dados de fábrica .NET API. Consulte [Referência da API do .NET do Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) para obter uma documentação abrangente sobre a API do .NET do de Data Factory. 

## <a name="prerequisites"></a>Pré-requisitos
* Visual Studio 2012 ou 2013 ou 2015.
* Baixe e instale o [Azure .NET SDK](http://azure.microsoft.com/downloads/).
* PowerShell do Azure. Siga as instruções em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo tooinstall PowerShell do Azure no seu computador. Use o Azure PowerShell toocreate um aplicativo do Active Directory do Azure.

### <a name="create-an-application-in-azure-active-directory"></a>Criar um aplicativo no Azure Active Directory
Criar um aplicativo do Active Directory do Azure, criar uma entidade de serviço para o aplicativo hello e atribuí-la toohello **colaborador da fábrica de dados** função.

1. Inicie o **PowerShell**.
2. Execute Olá comando a seguir e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Execute Olá tooview de comando a seguir todas as assinaturas de saudação para esta conta.

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. Execute Olá assinatura de saudação do comando tooselect que você deseja toowork com a seguir. Substituir  **&lt;NameOfAzureSubscription** &gt; com o nome da saudação de sua assinatura do Azure.

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > Anote **SubscriptionId** e **TenantId** da saída de hello desse comando.

5. Criar um grupo de recursos do Azure denominado **ADFTutorialResourceGroup** executando Olá comando de saudação do PowerShell a seguir.

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    Se o grupo de recursos Olá já existe, especifique se tooupdate-lo (Y) ou mantê-lo como (N).

    Se você usar um grupo de recursos diferentes, você precisa toouse nome de saudação do seu grupo de recursos no lugar de ADFTutorialResourceGroup neste tutorial.
6. Criar um aplicativo do Azure Active Directory.

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    Se você obtiver Olá erro a seguir, especifique uma URL diferente e execute o comando Olá novamente.
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. Crie hello entidade de serviço do AD.

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. Adicionar toohello principal do serviço **colaborador da fábrica de dados** função.

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. Obter a ID do aplicativo hello.

    ```PowerShell
    $azureAdApplication 
    ```
    Anote a ID do aplicativo hello (applicationID) de saída de hello.

Você deve ter quatro valores após estas etapas:

* ID do locatário
* ID da assinatura
* ID do aplicativo
* Senha (especificada no comando primeiro Olá)

## <a name="walkthrough"></a>Passo a passo
Olá instruções passo a passo, você criará uma fábrica de dados com um pipeline que contém uma atividade de cópia. Olá, atividade de cópia copia dados de uma pasta na sua pasta de tooanother do armazenamento de BLOBs do Azure no hello mesmo armazenamento de blob. 

Hello atividade de cópia realiza a movimentação de dados Olá na fábrica de dados do Azure. atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável. Consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo para obter detalhes sobre hello atividade de cópia.

1. Usando o Visual Studio 2012/2013/2015, crie um aplicativo de console C# .NET.
   1. Inicie o **Visual Studio** 2012/2013/2015.
   2. Clique em **arquivo**, ponto muito**novo**e clique em **projeto**.
   3. Expanda **Modelos** e selecione **Visual C#**. Neste passo a passo, você usa C#, mas você pode usar qualquer linguagem .NET.
   4. Selecione **aplicativo de Console** da lista de saudação de tipos de projeto em saudação à direita.
   5. Digite **DataFactoryAPITestApp** para Olá nome.
   6. Selecione **C:\ADFGetStarted** para Olá local.
   7. Clique em **Okey** toocreate projeto de saudação.
2. Clique em **ferramentas**, ponto muito**NuGet Package Manager**e clique em **Package Manager Console**.
3. Em Olá **Package Manager Console**, Olá seguintes etapas:
   1. Execute Olá pacote do comando tooinstall fábrica de dados a seguir:`Install-Package Microsoft.Azure.Management.DataFactories`
   2. Execute Olá pacote de Active Directory do Azure tooinstall de comando (use a API do Active Directory em código Olá) a seguir:`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`
4. Substitua o conteúdo de saudação do **App. config** arquivo no projeto de saudação com hello conteúdo a seguir: 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. No arquivo App. config de hello, atualizar os valores de  **&lt;ID do aplicativo&gt;**,  **&lt;senha&gt;**,  **&lt; ID da assinatura&gt;**, e  **&lt;ID do locatário&gt;**  com seus próprios valores.
6. Adicione o seguinte Olá **usando** instruções toohello **Program.cs** arquivo no projeto de saudação.

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. Adicionar Olá seguindo o código que cria uma instância de **DataPipelineManagementClient** classe toohello **principal** método. Você usar esse objeto toocreate uma fábrica de dados, um serviço vinculado, conjuntos de dados de entrada e saídos e um pipeline. Você também pode usar este fatias de toomonitor de objeto de um conjunto de dados em tempo de execução.

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Substituir valor de saudação do **resourceGroupName** com nome de saudação do seu grupo de recursos do Azure. Você pode criar um grupo de recursos usando Olá [AzureResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.
   >
   > Atualize o nome da saudação dados fábrica (dataFactoryName) toobe exclusivo. Nome da fábrica de dados Olá deve ser globalmente exclusivo. Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.
7. Adicionar Olá seguindo o código que cria um **fábrica de dados** toohello **principal** método.

    ```csharp
    // create a data factory
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
    ```
8. Adicionar Olá seguindo o código que cria um **serviço vinculado do armazenamento do Azure** toohello **principal** método.

   > [!IMPORTANT]
   > Substitua **storageaccountname** e **accountkey** pelo nome e pela chave da sua conta de Armazenamento do Azure.

    ```csharp
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
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. Adicionar Olá código que cria a seguir **conjuntos de dados de entrada e saídos** toohello **principal** método.

    Olá **FolderPath** para o blob de entrada hello está definido muito**adftutorial /** onde **adftutorial** é Olá nome do contêiner de saudação em seu armazenamento de blob. Se este contêiner não existe em seu armazenamento de BLOBs do Azure, crie um contêiner com este nome: **adftutorial** e carregar um contêiner de toohello do arquivo de texto.

    Olá FolderPath para saudação de saída blob é definido como: **adftutorial/apifactoryoutput / {Slice}** onde **fatia** é calculado dinamicamente Olá com base no valor de **SliceStart**(Iniciar data e hora de cada fatia).

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
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
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
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
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
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
    ```
10. Adicione o código a seguir de saudação que **cria e ativa um pipeline** toohello **principal** método. Essa pipeline tem uma **CopyActivity** que usa **BlobSource** como fonte e **BlobSink** como coletor.

    Hello atividade de cópia realiza a movimentação de dados Olá na fábrica de dados do Azure. atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável. Consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo para obter detalhes sobre hello atividade de cópia.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
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
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. Adicionar Olá toohello de código a seguir **principal** conjunto de dados de saída do status de saudação do método tooget de uma fatia de dados de saudação. Apenas uma fatia é esperada neste exemplo.

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. **(opcional)**  Tooget executar detalhes para um toohello da fatia de dados de código a seguir de saudação adicionar **principal** método.

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. Adicionar Olá após o método auxiliar usado pelo Olá **principal** método toohello **programa** classe. Esse método será exibida uma caixa de diálogo que permite que você forneça **nome de usuário** e **senha** que você use toolog no portal de tooAzure.

    ```csharp
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
    ```

15. No hello Gerenciador de soluções, expanda o projeto Olá: **DataFactoryAPITestApp**, clique com botão direito **referências**e clique em **adicionar referência**. Selecione caixa de seleção para o assembly `System.Configuration` e clique em **OK**.
15. Crie um aplicativo de console hello. Clique em **criar** no menu de saudação e clique em **compilar solução**.
16. Confirme se há pelo menos um arquivo no contêiner de adftutorial Olá em seu armazenamento de BLOBs do Azure. Caso contrário, crie Emp.txt arquivo no bloco de notas com hello seguindo conteúdo e carregá-lo toohello adftutorial contêiner.

    ```
    John, Doe
    Jane, Doe
    ```
17. Execute o exemplo hello clicando **depurar** -> **iniciar depuração** no menu de saudação. Quando você vir Olá **obtendo detalhes de uma fatia de dados da execução**, aguarde alguns minutos e pressione **ENTER**.
18. Use Olá tooverify portal do Azure essa fábrica de dados Olá **APITutorialFactory** é criada com hello artefatos a seguir:
    * Serviço vinculado: **AzureStorageLinkedService**
    * Conjunto de dados: **DatasetBlobSource** e **DatasetBlobDestination**.
    * Pipeline: **PipelineBlobSample**
19. Verificar se um arquivo de saída é criado no hello **apifactoryoutput** pasta Olá **adftutorial** contêiner.

## <a name="get-a-list-of-failed-data-slices"></a>Obter uma lista de fatias de dados com falha 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a>Próximas etapas
Consulte Olá seguinte exemplo para a criação de um pipeline usando o SDK .NET que copia dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure: 

- [Criar um pipeline de dados de toocopy do armazenamento de Blob tooSQL banco de dados](data-factory-copy-activity-tutorial-using-dotnet-api.md)
