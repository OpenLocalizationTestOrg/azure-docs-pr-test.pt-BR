---
title: 'Cosmos do Azure DB: Desenvolver com hello API de tabela no .NET | Microsoft Docs'
description: Saiba como toodevelop com a API da Azure Cosmos banco de dados tabela usando o .NET
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a>Cosmos do Azure DB: Desenvolver com hello API de tabela no .NET

O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft. Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.

Este tutorial aborda Olá tarefas a seguir: 

> [!div class="checklist"] 
> * Criar uma conta do Azure Cosmos DB 
> * Habilitar a funcionalidade no arquivo App. config de saudação 
> * Criar uma tabela usando Olá [API tabela](table-introduction.md) (visualização)
> * Adicionar uma tabela de entidade tooa 
> * Inserir um lote de entidades 
> * Recuperar uma única entidade 
> * Consultar entidades usando índices secundários automáticos 
> * Substituir uma entidade 
> * Excluir uma entidade 
> * Excluir uma tabela
 
## <a name="tables-in-azure-cosmos-db"></a>Tabelas no Azure Cosmos DB 

Banco de dados do Azure Cosmos fornece Olá [API tabela](table-introduction.md) (visualização) para aplicativos que precisam de um repositório de chave-valor com um design sem esquema. [Armazenamento de tabela do Azure](../storage/common/storage-introduction.md) SDKs e APIs REST podem ser toowork usado com o banco de dados do Azure Cosmos. Você pode usar as tabelas do banco de dados do Azure Cosmos toocreate com requisitos de alta taxa de transferência. O Azure Cosmos DB dá suporte a tabelas com otimização de taxa de transferência (chamadas informalmente de "tabelas premium"), atualmente em visualização pública. 

Você pode continuar toouse armazenamento de tabela do Azure para tabelas com armazenamento de alta e reduzir os requisitos de taxa de transferência. Banco de dados do Azure Cosmos apresenta suporte para tabelas com otimização de armazenamento em uma atualização futura e tabela de Azure existentes e novas contas de armazenamento será perfeitamente atualizado tooAzure Cosmos DB.

Se você usar o armazenamento de tabela do Azure no momento, você ganha Olá benefícios com visualização de "tabela premium" hello a seguir:

- [Distribuição global](distribute-data-globally.md) turnkey com hospedagem múltipla e [failovers automáticos e manuais](regional-failover.md)
- Suporte para indexação agnóstica de esquema automática em relação a todas as propriedades ("índices secundários") e consultas rápidas 
- Suporte para [dimensionamento independente de armazenamento e taxa de transferência](partition-data.md), em qualquer número de regiões
- Suporte para [dedicada de taxa de transferência por tabela](request-units.md) que podem ser dimensionados de centenas toomillions de solicitações por segundo
- Suporte para [cinco níveis de consistência ajustáveis](consistency-levels.md) tootrade disponibilidade, latência e consistência com base em suas necessidades de aplicativo
- disponibilidade de 99,99% em uma única região e capacidade tooadd mais regiões para alta disponibilidade, e [SLAs abrangentes do setor](https://azure.microsoft.com/support/legal/sla/cosmos-db/) em disponibilidade geral
- Trabalhar com o armazenamento do Azure existente Olá .NET SDK e nenhum aplicativo de tooyour de alterações de código

Durante a visualização de Olá, oferece suporte a banco de dados do Azure Cosmos Olá API de tabela usando o SDK .NET de saudação. Você pode baixar Olá [SDK de visualização do armazenamento do Azure](https://aka.ms/premiumtablenuget) do NuGet, que tem Olá mesmas classes e assinaturas de método como Olá [SDK de armazenamento do Azure](https://www.nuget.org/packages/WindowsAzure.Storage), mas também pode se conectar tooAzure Cosmos DB contas usando Olá Tabela de API.

toolearn mais informações sobre tarefas complexas do armazenamento de tabela do Azure, consulte:

* [Introdução tooAzure Cosmos DB: API de tabela](table-introduction.md)
* Olá documentação de referência de serviço de tabela para obter detalhes completos sobre as APIs disponíveis [biblioteca de cliente de armazenamento para a referência do .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

### <a name="about-this-tutorial"></a>Sobre este tutorial
Este tutorial é para desenvolvedores que estão familiarizados com hello SDK de armazenamento de tabela do Azure e deseja que os recursos do premium Olá toouse disponíveis usando o banco de dados do Azure Cosmos. Ele se baseia [Introdução ao armazenamento de tabela do Azure usando o .NET](table-storage-how-to-use-dotnet.md) e mostra como tootake proveito dos recursos adicionais, como índices secundários, taxa de transferência fornecida e hospedagem múltipla. Abordaremos como toouse Olá toocreate portal do Azure uma conta de banco de dados do Azure Cosmos e, em seguida, criar e implantar um aplicativo de tabela. Também explicaremos detalhadamente os exemplos de .NET para criar e excluir uma tabela e inserir, atualizar, excluir e consultar dados de tabela. 

Se você ainda não tiver o Visual Studio de 2017 instalado, você pode baixar e usar o hello **livre** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Certifique-se de que você habilite **desenvolvimento do Azure** durante a instalação do Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Criar uma conta de banco de dados

Vamos começar criando uma conta de banco de dados do Azure Cosmos em Olá portal do Azure.  

> [!TIP]
> * Já tem uma conta do Azure Cosmos DB? Nesse caso, pular muito[configurar sua solução do Visual Studio](#SetupVS).
> * Você tinha uma conta do Azure DocumentDB? Se assim, sua conta agora é uma conta de banco de dados do Azure Cosmos e poderá pular muito[configurar sua solução do Visual Studio](#SetupVS).  
> * Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) toosetup Olá emulador e pular muito[configurar sua solução do Visual Studio](#SetupVS).
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a>Clonar um aplicativo de exemplo hello

Agora vamos, clonar um aplicativo de tabela do github, defina a cadeia de caracteres de conexão hello e executá-lo.

1. Abra uma janela de terminal de git, como git bash, e `cd` tooa diretório de trabalho.  

2. Execute Olá repositório de exemplo do comando tooclone Olá a seguir. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. Em seguida, abra o arquivo de solução de saudação no Visual Studio.

## <a name="update-your-connection-string"></a>Atualizar sua cadeia de conexão

Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.

1. Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**. Você usará botões de cópia Olá Olá direita da cadeia de conexão do hello tela toocopy Olá em arquivo App. config de saudação na próxima etapa do hello.

2. No Visual Studio, abra o arquivo App. config de saudação. 

3. Copie o valor URI do portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá o valor da chave conta Olá no App. config. Use nome de conta Olá criada anteriormente para o nome de conta no App. config.
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> toouse esse aplicativo com o armazenamento de tabela do Azure padrão, você precisa de cadeia de conexão de Olá toochange em `app.config file`. Use nome de conta do hello como o nome da conta de tabela e a chave como chave primária de armazenamento do Azure. <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a>Criar e implantar o aplicativo hello
1. No Visual Studio, clique com botão direito no projeto Olá no **Solution Explorer** e, em seguida, clique em **gerenciar pacotes NuGet**. 

2. Em Olá NuGet **procurar** , digite ***windowsazure PremiumTable***. Marque **Incluir versões de pré-lançamento**.

3. Resultados de hello, instalar Olá **windowsazure PremiumTable** e escolha a compilação de visualização de saudação `0.0.1-preview`. Essa ação instala o pacote de armazenamento de tabela do Azure hello e todas as dependências.

4. Clique em CTRL + F5 aplicativo hello de toorun. 

Agora você pode voltar tooData Explorer e consulte a consulta, modificar e trabalhar com esses dados de tabela. 

> [!NOTE]
> toouse esse aplicativo com o emulador do Azure Cosmos banco de dados, você apenas precisa de cadeia de conexão Olá toochange no `app.config file`. Saudação de uso abaixo do valor de emulador. <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a>Recursos Azure Cosmos DB
Banco de dados do Azure Cosmos dá suporte a vários recursos que não estão disponíveis no hello API de armazenamento de tabela do Azure. Olá nova funcionalidade pode ser habilitada por meio do seguinte Olá `appSettings` valores de configuração. Não apresentamos qualquer nova assinaturas ou sobrecargas toohello visualização do SDK do armazenamento do Azure. Isso permite que você tooconnect tooboth standard e premium tabelas e trabalho com outros serviços de armazenamento do Azure como Blobs e filas. 


| Chave | Descrição |
| --- | --- |
| TableConnectionMode  | O Azure Cosmos DB oferece suporte a dois modos de conectividade. Em `Gateway` modo, as solicitações sempre são feitas gateway de banco de dados do Azure Cosmos toohello, que encaminha toohello partições de dados correspondente. Em `Direct` modo de conectividade cliente Olá busca o mapeamento de saudação do toopartitions de tabelas e as solicitações são feitas diretamente em partições de dados. É recomendável `Direct`, Olá padrão.  |
| TableConnectionProtocol | O Azure Cosmos DB oferece suporte a dois protocolos de conexão - `Https` e `Tcp`. `Tcp`saudação padrão e recomendada, pois é mais simples. |
| TablePreferredLocations | A lista separada por vírgulas de locais (hospedagem múltipla) preferenciais para leituras. Cada conta do Azure Cosmos DB pode ser associada a 1 ou 30 ou mais regiões. Cada instância de cliente pode especificar um subconjunto dessas regiões Olá preferido para leituras de baixa latência. regiões de saudação devem ser nomeados usando seus [exibir nomes](https://msdn.microsoft.com/library/azure/gg441293.aspx), por exemplo, `West US`. Consulte também [APIs de hospedagem múltipla](tutorial-global-distribution-table.md).
| TableConsistencyLevel | Você pode alternar entre disponibilidade, consistência e latência escolhendo entre cinco níveis de consistência bem definidos: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` e `Eventual`. O padrão é `Session`. Escolha de saudação do nível de consistência faz diferença significativa de desempenho em configurações de várias regiões. Consulte [Níveis de consistência](consistency-levels.md) para saber detalhes. |
| TableThroughput | Taxa de transferência reservada para a tabela de saudação expressada em unidades de solicitação (RU) por segundo. Tabelas únicas podem suportar centenas de milhões de RU/s. Consulte [Unidades de solicitação](request-units.md). O padrão é `400` |
| TableIndexingPolicy | Indexação secundária consistente e automática de todas as colunas de tabelas | Toohello de conformidade de cadeia de caracteres JSON especificação da política de indexação. Consulte [política de indexação](indexing-policies.md) toosee como você pode alterar a indexação colunas específicas tooinclude/exclusão de política. | Indexação automática de todas as propriedades (hash para cadeias de caracteres e o intervalo de números) |
| TableQueryMaxItemCount | Configure o número máximo de saudação de itens retornados por consultas de tabela em uma única viagem de ida. O padrão é `-1`, que permite que o banco de dados do Azure Cosmos determinar dinamicamente o valor de saudação em tempo de execução. |
| TableQueryEnableScan | Se a consulta de saudação não pode usar índice Olá para qualquer filtro, em seguida, executá-lo assim mesmo por meio de uma verificação. O padrão é `false`.|
| TableQueryMaxDegreeOfParallelism | grau de saudação de paralelismo de execução de uma consulta entre partições. `0`serial com nenhuma pré-leitura, `1` serial com pré-leitura e valores maior taxa de saudação do aumento de paralelismo. O padrão é `-1`, que permite que o banco de dados do Azure Cosmos determinar dinamicamente o valor de saudação em tempo de execução. |

valor padrão do hello toochange, abra Olá `app.config` arquivo no Gerenciador de soluções no Visual Studio. Adicionar conteúdo Olá Olá `<appSettings>` elemento mostrado abaixo. Substituir `account-name` com o nome de saudação da sua conta de armazenamento e `account-key` com sua chave de acesso da conta. 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello. Olá abrir `Program.cs` arquivo e descobrir que essas linhas de código criam Olá recursos de tabela. 

## <a name="create-hello-table-client"></a>Crie saudação do cliente de tabela
Você inicializar um `CloudTableClient` conta de tabela toohello tooconnect.

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
Esse cliente é inicializado usando Olá `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, e `TablePreferredLocations` valores de configuração, se especificado nas configurações de aplicativo hello.
    
## <a name="create-a-table"></a>Criar uma tabela
Em seguida, você cria uma tabela usando `CloudTable`. Tabelas no banco de dados do Azure Cosmos podem dimensionada de forma independente em termos de armazenamento e a taxa de transferência e o particionamento é tratado automaticamente pelo serviço de saudação. O Azure Cosmos DB oferece suporte a tabelas ilimitadas e tamanho fixo. Consulte [Particionamento no Azure Cosmos DB](partition-data.md) para saber detalhes. 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

Há uma diferença importante em como as tabelas são criadas. O Azure Cosmos DB reserva a taxa de transferência, ao contrário do modelo baseado em consumo do armazenamento do Azure para transações. modelo de reserva Olá tem dois benefícios principais:

* A taxa de transferência é dedicada/reservada, para que você nunca sofra restrições se a taxa de solicitação está no limite ou abaixo da sua taxa de transferência provisionada
* modelo de reserva de saudação é mais [econômico para cargas de trabalho pesadas de taxa de transferência](key-value-store-cost.md)

Você pode configurar a taxa de transferência saudação padrão por configuração hello para `TableThroughput` em termos de RUS (unidades de solicitação) por segundo. 

Uma leitura de uma entidade de 1 KB é normalizada como 1 RU e outras operações são normalizada tooa RU valor com base no seu consumo de CPU, memória e IOPS fixo. Saiba mais sobre [Unidades de solicitação no Azure Cosmos DB](request-units.md).

> [!NOTE]
> Enquanto o SDK de armazenamento de tabela não oferece suporte a modificação de taxa de transferência, você pode alterar a taxa de transferência Olá instantaneamente a qualquer momento usando o portal do Azure de saudação ou CLI do Azure.

Em seguida, percorremos leitura simples hello e operações de gravação (CRUD) usando armazenamento de tabela do Azure Olá SDK. Este tutorial demonstra latências baixas de milissegundos de dígito único previsíveis e consultas rápidas fornecidas pelo Azure Cosmos DB.

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de entidade tooa
As entidades no armazenamento de tabela do Azure estendem da saudação `TableEntity` classe e deve ter `PartitionKey` e `RowKey` propriedades. Aqui está um exemplo de definição de uma entidade de cliente.

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

saudação de trecho de código a seguir mostra como tooinsert uma entidade com hello SDK de armazenamento do Azure. Banco de dados do Azure Cosmos destina-se a garantia de baixa latência em qualquer escala em Olá, mundo.

Conclusão de gravações < 15 ms em p99 e ~ 6 ms em p50 para aplicativos executados em Olá Olá conta de banco de dados do Azure Cosmos mesma região. E a duração da contas do fato de saudação que grava reconhecidas toohello back cliente somente depois que eles são replicados de maneira síncrona, forma duradoura confirmada, e todo o conteúdo foi indexado.

Olá API de tabela para o banco de dados do Azure Cosmos está em visualização. Disponibilidade geral, Olá p99 latência garantias contam com SLAs como outras APIs de banco de dados do Azure Cosmos. 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>Inserir um lote de entidades
Oferece suporte de armazenamento do Azure tabela uma API de operação em lote, que permite que você combine atualizações, exclusões e inserções em Olá a mesma operação de lote único. Banco de dados do Azure Cosmos não tem algumas das limitações de saudação na API de lote hello como armazenamento de tabela do Azure. Por exemplo, você pode executar várias leituras dentro de um lote, você pode executar várias toohello de gravações mesma entidade dentro de um lote, e não há nenhum limite no 100 operações por lote. 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a>Recuperar uma única entidade
Recupera (obtém) no Azure Cosmos DB completa < 10 ms p99 e ~ 1 ms com p50 em Olá mesma região do Azure. Você pode adicionar quantos conta tooyour de regiões para leituras de baixa latência e implantar aplicativos tooread da sua região local ("multihomed"), definindo `TablePreferredLocations`. 

Você pode recuperar uma única entidade utilizando Olá trecho de código a seguir:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> Saiba mais sobre as APIs de hospedagem múltipla em [Desenvolvendo com várias regiões](tutorial-global-distribution-table.md)
>

## <a name="query-entities-using-automatic-secondary-indexes"></a>Consultar entidades usando índices secundários automáticos
Tabelas podem ser consultadas usando Olá `TableQuery` classe. O Azure Cosmos DB tem um mecanismo de banco de dados otimizado para gravação que indexa automaticamente todas as colunas em sua tabela. A indexação no banco de dados do Azure Cosmos é tooschema desconhecido. Portanto, mesmo que seu esquema é diferente entre as linhas, ou se o esquema Olá evolui ao longo do tempo, ele será indexado automaticamente. Como o banco de dados do Azure Cosmos dá suporte a índices secundários automática, consultas em relação a qualquer propriedade podem usar índice hello e ser atendidas com eficiência.

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

Na visualização, o banco de dados do Azure Cosmos dá suporte a saudação mesma funcionalidade como armazenamento de tabela do Azure para Olá API da tabela de consulta. O Azure Cosmos DB também oferece suporte à classificação, agregações, consulta geoespacial, hierarquia e uma ampla variedade de funções internas. funcionalidade adicional Olá será fornecida em Olá API de tabela em uma atualização futura do serviço. Consulte [Consulta do Azure Cosmos DB](documentdb-sql-query.md) para uma visão geral desses recursos. 

## <a name="replace-an-entity"></a>Substituir uma entidade
tooupdate uma entidade, recuperá-lo do serviço de tabela hello, modificar o objeto de entidade hello e, em seguida, salvar as alterações de saudação fazer toohello serviço de tabela. Olá código a seguir altera o número de telefone de um cliente existente. 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
Da mesma forma, você pode executar as operações `InsertOrMerge` ou `Merge`.  

## <a name="delete-an-entity"></a>Excluir uma entidade
Você pode facilmente excluir uma entidade após recuperá-lo usando Olá mesmo padrão mostrado para a atualização de uma entidade. saudação de código a seguir recupera e exclui uma entidade customer.

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a>Excluir uma tabela
Por fim, Olá exemplo de código a seguir exclui uma tabela de uma conta de armazenamento. Você pode excluir e recriar uma tabela imediatamente com o Azure Cosmos DB.

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a>Limpar recursos 

Se você não vai toocontinue toouse esse aplicativo, use Olá seguindo as etapas toodelete todos os recursos criados por esse tutorial Olá portal do Azure.   

1. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.  
2. Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**. 

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, abordamos como tooget iniciado usando o banco de dados do Azure Cosmos com hello API de tabela e que você fez a seguir hello: 

> [!div class="checklist"] 
> * Criou uma conta do Azure Cosmos DB 
> * Funcionalidade habilitada no arquivo App. config de saudação 
> * Criou uma tabela 
> * Adicionada a uma tabela de entidade tooa 
> * Inseriu um lote de entidades 
> * Recuperou uma única entidade 
> * Consultou entidades usando índices secundários automáticos 
> * Substituiu uma entidade 
> * Excluiu uma entidade 
> * Excluiu uma tabela  

Agora você pode continuar tutorial próxima toohello e saber mais sobre como consultar dados da tabela. 

> [!div class="nextstepaction"]
> [Consultar com hello API de tabela](tutorial-query-table.md)
