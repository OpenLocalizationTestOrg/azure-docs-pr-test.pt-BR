---
title: "ferramenta de migração de aaaDatabase para o banco de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba como Olá toouse Abrir fonte Azure Cosmos DB dados migração ferramentas tooimport dados tooAzure Cosmos banco de dados de várias fontes, incluindo arquivos MongoDB, SQL Server, armazenamento tabela, Amazon DynamoDB, CSV e JSON. Conversão de tooJSON CSV."
keywords: "CSV toojson, ferramentas de migração do banco de dados, converter toojson csv"
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a>Como tooimport dados no banco de dados do Azure Cosmos para Olá API DocumentDB?

Este tutorial fornece instruções sobre como usar o hello Azure Cosmos DB: ferramenta de migração de dados de API de documentos, que pode importar dados de várias fontes, incluindo arquivos JSON, arquivos CSV, SQL, MongoDB, armazenamento de tabela do Azure, DynamoDB Amazon e documentos de banco de dados do Azure Cosmos Conjuntos de API em conjuntos para usam com o banco de dados do Azure Cosmos e hello API DocumentDB. ferramenta de migração de dados de saudação também pode ser usada ao migrar de uma única partição tooa várias partições coleção para Olá API DocumentDB.

ferramenta de migração de dados Olá só funciona quando a importação de dados no banco de dados do Azure Cosmos para usa com hello API DocumentDB. Não há suporte para a importação de dados para uso com hello API de tabela ou a API do Graph neste momento. 

dados tooimport para uso com hello MongoDB API, consulte [o banco de dados do Azure Cosmos: como dados toomigrate Olá MongoDB API?](mongodb-migrate.md).

Este tutorial aborda Olá tarefas a seguir:

> [!div class="checklist"]
> * Instalação da ferramenta de migração de dados Olá
> * Importação de dados de diferentes fontes de dados
> * Exportação do banco de dados do Azure Cosmos tooJSON

## <a id="Prerequisites"></a>Pré-requisitos
Antes de seguir as instruções neste artigo hello, certifique-se de que você tenha a seguinte Olá instalado:

* [Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) ou superior.

## <a id="Overviewl"></a>Visão geral da ferramenta de migração de dados Olá
ferramenta de migração de dados de saudação é uma solução de software livre que importa dados tooAzure Cosmos banco de dados de uma variedade de fontes, incluindo:

* Arquivos JSON
* MongoDB
* SQL Server
* Arquivos CSV
* Armazenamento da tabela do Azure
* Amazon DynamoDB
* HBase
* Coleções do Azure Cosmos DB

Enquanto a ferramenta de importação de saudação inclui uma interface gráfica do usuário (dtui.exe), ele também pode ser controlado pela linha de comando da saudação (dt.exe). Na verdade, há um comando de saudação associado toooutput opção depois de configurar uma importação por meio de saudação da interface do usuário. Dados de origem em tabela (por exemplo, arquivos do SQL Server ou CSV) podem ser transformados, de forma que relações hierárquicas (subdocumentos) podem ser criadas durante a importação. Manter toolearn de ler mais sobre as opções de fonte, tooimport de linhas de comando de exemplo de cada fonte, opções de destino e a exibição de resultados de importação.

## <a id="Install"></a>Instalar a ferramenta de migração de dados Olá
código-fonte Olá migração ferramenta está disponível no GitHub no [este repositório](https://github.com/azure/azure-documentdb-datamigrationtool) e uma versão compilada está disponível em [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d). Você pode compilar solução hello ou simplesmente baixar e extrair o diretório de tooa Olá versão compilada de sua escolha. Em seguida, execute um:

* **Dtui.exe**: versão de interface gráfica da ferramenta de saudação
* **DT.exe**: versão de linha de comando da ferramenta de saudação

## <a name="import-data"></a>Importar dados

Depois de instalar a ferramenta Olá, é hora tooimport seus dados. O tipo de dados você deseja tooimport?

* [Arquivos JSON](#JSON)
* [MongoDB](#MongoDB)
* [Arquivos de exportação do MongoDB](#MongoDBExport)
* [SQL Server](#SQL)
* [Arquivos CSV](#CSV)
* [Armazenamento de Tabelas do Azure](#AzureTableSource)
* [Amazon DynamoDB](#DynamoDBSource)
* [Blob](#BlobImport)
* [Coleções do Azure Cosmos DB](#DocumentDBSource)
* [HBase](#HBaseSource)
* [Importação em massa do Azure Cosmos DB](#DocumentDBBulkImport)
* [Importação de registro sequencial do Azure Cosmos DB](#DocumentDSeqTarget)


## <a id="JSON"></a>arquivos JSON tooimport
opção de Importador de fonte de arquivo JSON de saudação permite que você tooimport um ou mais arquivos JSON único documento ou arquivos JSON que contêm uma matriz de documentos JSON. Ao adicionar pastas que contêm tooimport de arquivos JSON, você tem a opção de saudação do recursivamente procurando arquivos em subpastas.

![Captura de tela das opções de origem do arquivo JSON — ferramentas de migração de banco de dados](./media/import-data/jsonsource.png)

Aqui estão alguns arquivos JSON de tooimport de exemplos de linha de comando:

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <a id="MongoDB"></a>tooimport do MongoDB

> [!IMPORTANT]
> Se você estiver importando tooan Azure Cosmos DB conta com suporte para o MongoDB, siga estas [instruções](mongodb-migrate.md).
> 
> 

Olá opção de Importador de origem do MongoDB permite tooimport de uma coleção do MongoDB individual e opcionalmente filtre documentos usando uma consulta e/ou modificar a estrutura do documento hello usando uma projeção.  

![Captura de tela das opções de fonte do MongoDB](./media/import-data/mongodbsource.png)

cadeia de caracteres de conexão Hello está no formato de MongoDB padrão da saudação:

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> Use Olá Verifique se o comando tooensure que Olá MongoDB instância especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.
> 
> 

Digite o nome de saudação de coleção de saudação do qual os dados serão importados. Você pode opcionalmente especificar ou fornecer um arquivo para uma consulta (por exemplo, {pop: {$gt: 5000}}) e/ou projeção (por exemplo, {loc:0}) tooboth filtro e forma Olá dados toobe importado.

Aqui estão alguns tooimport de exemplos de linha de comando do MongoDB:

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <a id="MongoDBExport"></a>arquivos de exportação do MongoDB tooimport

> [!IMPORTANT]
> Se você estiver importando tooan Azure Cosmos DB conta com suporte para o MongoDB, siga estas [instruções](mongodb-migrate.md).
> 
> 

Olá opção importador fonte de arquivo do MongoDB exportação JSON permite que você tooimport um ou mais arquivos JSON produzida do utilitário de mongoexport hello.  

![Captura de tela das opções de fonte de exportação do MongoDB](./media/import-data/mongodbexportsource.png)

Ao adicionar pastas que contêm arquivos de JSON do MongoDB exportação para importação, você tem a opção de saudação do procurando arquivos em subpastas de forma recursiva.

Aqui está um tooimport de exemplo de linha de comando de exportação do MongoDB arquivos JSON:

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <a id="SQL"></a>tooimport do SQL Server
Olá opção de Importador de origem do SQL permite que você tooimport de um banco de dados individual do SQL Server e opcionalmente filtros Olá registros toobe importado usando uma consulta. Além disso, você pode modificar a estrutura do documento hello especificando um separador de aninhamento (mais detalhes em breve).  

![Captura de tela das opções de origem do SQL — ferramentas de migração de banco de dados](./media/import-data/sqlexportsource.png)

Olá formato de cadeia de caracteres de conexão de saudação é saudação padrão SQL conexão cadeia de caracteres.

> [!NOTE]
> Use Olá Verifique se o comando tooensure que Olá a instância do SQL Server especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.
> 
> 

Olá aninhamento propriedade separator é usado toocreate as relações hierárquicas (subdocumentos) durante a importação. Considere Olá consulta SQL a seguir:

*Selecione CAST (BusinessEntityID como varchar) como ID, Nome, AddressType como [Address.AddressType], AddressLine1 como [Address.AddressLine1], City como [Address.Location.City], StateProvinceName como [Address.Location.StateProvinceName], PostalCode como [Address.PostalCode], CountryRegionName como [Address.CountryRegionName] de Sales.vStoreWithAddresses WHERE AddressType='Main Office'*

Que retorna Olá resultados (parciais) a seguir:

![Captura de tela dos resultados de consulta do SQL](./media/import-data/sqlqueryresults.png)

Observe os aliases hello como Address.AddressType e Address.Location.StateProvinceName. Especificando um separador de aninhamento de '.', ferramenta de importação de saudação cria endereço e importar subdocumentos Address.Location durante a saudação. Este é um exemplo de um documento resultante no Azure Cosmos DB:

*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*

Aqui estão alguns tooimport de exemplos de linha de comando do SQL Server:

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <a id="CSV"></a>os arquivos CSV tooimport e converter CSV tooJSON
Olá opção de Importador de fonte de arquivo CSV permite que você tooimport um ou mais arquivos CSV. Ao adicionar pastas que contêm arquivos CSV para importar, você tem a opção de saudação do procurando arquivos em subpastas de forma recursiva.

![Opções de fonte de captura de tela de CSV - tooJSON CSV](media/import-data/csvsource.png)

Fonte SQL toohello semelhante, Olá aninhamento propriedade separator pode ser relações hierárquicas de toocreate usado (subdocumentos) durante a importação. Considere Olá a linha de cabeçalho CSV e linhas de dados a seguir:

![Registros de exemplo de captura de tela de CSV - tooJSON CSV](./media/import-data/csvsample.png)

Observe os aliases hello como DomainInfo.Domain_Name e RedirectInfo.Redirecting. Especificando um separador de aninhamento de '.', a ferramenta de importação de saudação criará DomainInfo e importar subdocumentos RedirectInfo durante a saudação. Este é um exemplo de um documento resultante no Azure Cosmos DB:

*{"DomainInfo": {"Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www. ACUS.GOV"},"Órgão Federal":"Administrativa conferência de saudação dos Estados Unidos","RedirectInfo": {"Redirecionar":"0","Redirect_Destination":" "},"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*

ferramenta de importação de saudação tentará tooinfer informações de tipo de valores sem aspas em arquivos CSV (valores entre aspas sempre são tratados como cadeias de caracteres).  Tipos são identificados em ordem de saudação: número, datetime, booleano.  

Há dois outros toonote coisas sobre importação de CSV:

1. Por padrão, os valores sem aspas sempre são cortados para tabulações e espaços, enquanto os valores entre aspas são preservados como estão. Esse comportamento pode ser substituído por hello que Trim entre aspas a opção de linha de comando de /s.TrimQuoted de caixa de seleção ou saudação de valores.
2. Por padrão, um nulo sem aspas é tratado como um valor nulo. Esse comportamento pode ser substituído (isto é, trate um null sem aspas como uma cadeia de caracteres "null") com hello tratar sem aspas NULL como a opção de linha de comando de /s.NoUnquotedNulls de caixa de seleção ou saudação de cadeia de caracteres.

Aqui está um exemplo de linha de comando para importação de CSV:

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <a id="AzureTableSource"></a>tooimport do armazenamento de tabela do Azure
Olá opção de Importador de origem de armazenamento de tabela do Azure permite que você tooimport de uma tabela de armazenamento de tabela do Azure individual e opcionalmente filtros Olá toobe de entidades de tabela importada. Observe que você não pode usar dados de armazenamento de tabela do Azure ferramenta tooimport do hello migração de dados no banco de dados do Azure Cosmos para uso com hello API de tabela. Importação só tooAzure Cosmos banco de dados para uso com hello API DocumentDB é suportada no momento.

![Captura de tela das opções de origem de armazenamento da tabela do Azure](./media/import-data/azuretablesource.png)

formato Olá Olá cadeia de conexão de armazenamento de tabela do Azure é:

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> Use Olá Verifique se o comando tooensure que Olá instância de armazenamento de tabela do Azure especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.
> 
> 

Insira nome de saudação do hello Azure tabela da qual os dados serão importados. Opcionalmente, você pode especificar um [filtro](https://msdn.microsoft.com/library/azure/ff683669.aspx).

Olá opção de Importador de origem de armazenamento de tabela do Azure tem Olá opções adicionais a seguir:

1. Incluir campos internos
   1. Todos - incluir todos os campos internos (PartitionKey, RowKey e Timestamp)
   2. Nenhum - excluir todos os campos internos
   3. RowKey - incluir apenas o campo de RowKey Olá
2. Selecionar colunas
   1. Filtros de armazenamento de tabela do Azure não dão suporte a projeções. Se você quiser importar tooonly propriedades da entidade específicas tabela do Azure, adicione lista de colunas selecione toohello. Todas as outras propriedades da entidade serão ignoradas.

Aqui está um tooimport de exemplo de linha de comando do armazenamento de tabela do Azure:

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <a id="DynamoDBSource"></a>tooimport do Amazon DynamoDB
Olá Amazon DynamoDB opção de Importador de origem permite tooimport de uma tabela individual do Amazon DynamoDB e opcionalmente filtre Olá entidades toobe importado. Vários modelos são fornecidos para que a configuração de uma importação seja tão fácil quanto possível.

![Captura de tela das opções de origem do Amazon DynamoDB — ferramentas de migração de banco de dados](./media/import-data/dynamodbsource1.png)

![Captura de tela das opções de origem do Amazon DynamoDB — ferramentas de migração de banco de dados](./media/import-data/dynamodbsource2.png)

formato Olá Olá Amazon DynamoDB cadeia de caracteres de conexão é:

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> Use Olá Verifique se o comando tooensure que Olá Amazon DynamoDB instância especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.
> 
> 

Aqui está um tooimport de exemplo de linha de comando do Amazon DynamoDB:

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <a id="BlobImport"></a>arquivos de tooimport do armazenamento de BLOBs do Azure
Olá arquivo JSON, arquivo de exportação do MongoDB e as opções de Importador de fonte de arquivo CSV permitem que você tooimport um ou mais arquivos de armazenamento de BLOBs do Azure. Depois de especificar uma URL de contêiner de Blob e a chave de conta, basta fornece um tooimport de arquivo (s) expressão regular tooselect hello.

![Captura de tela das opções de origem de arquivo de blob](./media/import-data/blobsource.png)

Aqui está o arquivos de JSON de tooimport de exemplo de linha de comando do armazenamento de BLOBs do Azure:

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <a id="DocumentDBSource"></a>tooimport de uma coleção de API do Azure Cosmos banco de dados DocumentDB
Olá opção do banco de dados do Azure Cosmos fonte importador permite tooimport dados de uma ou mais coleções de banco de dados do Azure Cosmos e opcionalmente filtre documentos usando uma consulta.  

![Captura de tela das opções de fonte do Azure Cosmos DB](./media/import-data/documentdbsource.png)

formato Olá Olá cadeia de caracteres de conexão de banco de dados do Azure Cosmos é:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

saudação de cadeia de caracteres de conexão do banco de dados do Azure Cosmos conta pode ser recuperada da folha de chaves de saudação do hello portal do Azure, conforme descrito em [como toomanage uma conta de banco de dados do Azure Cosmos](manage-account.md), no entanto, Olá o nome do banco de dados de saudação deve toohello toobe anexado cadeia de caracteres de conexão no hello formato a seguir:

    Database=<CosmosDB Database>;

> [!NOTE]
> Use Olá Verifique se o comando tooensure que Olá instância de banco de dados do Azure Cosmos especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.
> 
> 

tooimport de uma coleção de banco de dados do Azure Cosmos único, digite o nome de saudação de coleção de saudação do qual os dados serão importados. tooimport de várias coleções de banco de dados do Azure Cosmos, forneça uma expressão regular toomatch um ou mais nomes de coleção (por exemplo, collection01 | collection02 | collection03). Você pode opcionalmente especificar, ou fornecer um arquivo para um filtro de consulta tooboth e Olá toobe de dados importado de forma.

> [!NOTE]
> Desde que o campo de coleção Olá aceita expressões regulares, se você estiver importando de uma única coleção cujo nome contém caracteres de expressão regular, em seguida, esses caracteres devem ser substituídas adequadamente.
> 
> 

Olá opção do banco de dados do Azure Cosmos fonte importador tem seguintes Olá opções avançadas:

1. Incluir campos internos: Especifica se ou não tooinclude Azure Cosmos DB documento propriedades do sistema Olá exportar (por exemplo, RID, TS).
2. Número de novas tentativas em caso de falha: especifica Olá número de vezes tooretry Olá conexão tooAzure Cosmos banco de dados no caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).
3. Intervalo de repetição: Especifica quanto tempo toowait entre repetindo Olá conexão tooAzure Cosmos banco de dados no caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).
4. Modo de Conexão: Especifica Olá toouse de modo de conexão com o banco de dados do Azure Cosmos. opções disponíveis de saudação são DirectTcp, DirectHttps e Gateway. modos de conexão direta de saudação são mais rapidamente, enquanto o modo de gateway Olá é firewall mais amigável pois ele usa apenas a porta 443.

![Captura de tela das opções avançadas de fonte do Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> Olá importar do modo DirectTcp tooconnection ferramenta padrões. Se você enfrentar problemas de firewall, alterne o modo de tooconnection Gateway, pois exige apenas a porta 443.
> 
> 

Aqui estão alguns tooimport de exemplos de linha de comando do banco de dados do Azure Cosmos:

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> Olá, ferramenta de importação de dados do Azure Cosmos DB também oferece suporte à importação de dados de saudação [emulador de banco de dados do Azure Cosmos](local-emulator.md). Ao importar dados de um emulador local, defina o ponto de extremidade de saudação muito`https://localhost:<port>`. 
> 
> 

## <a id="HBaseSource"></a>tooimport do HBase
Olá HBase opção de Importador de origem permite tooimport dados de uma tabela do HBase e opcionalmente filtre dados saudação. Vários modelos são fornecidos para que a configuração de uma importação seja tão fácil quanto possível.

![Captura de tela das opções de origem do HBase](./media/import-data/hbasesource1.png)

![Captura de tela das opções de origem do HBase](./media/import-data/hbasesource2.png)

formato Olá Olá HBase Stargate cadeia de caracteres de conexão é:

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> Use Olá Verifique se o comando tooensure que Olá HBase instância especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.
> 
> 

Aqui está um tooimport de exemplo de linha de comando do HBase:

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <a id="DocumentDBBulkTarget"></a>tooimport toohello API DocumentDB (importação em massa)
Importador do Hello Azure Cosmos DB Bulk permite tooimport de qualquer uma das opções de origem disponível hello, usando um procedimento armazenado do Azure Cosmos DB para a eficiência. ferramenta de saudação oferece suporte a importação tooone particionada único banco de dados do Azure Cosmos coleção, bem como importação fragmentada no qual os dados são particionados em vários conjuntos de banco de dados do Azure Cosmos particionada único. Para obter mais informações sobre o particionamento de dados, consulte [Particionamento e escala no Azure Cosmos DB](partition-data.md). ferramenta de saudação criar, executar e, em seguida, excluir procedimento armazenado de saudação do hello collection(s) de destino.  

![Captura de tela das opções em massa do Azure Cosmos DB](./media/import-data/documentdbbulk.png)

formato Olá Olá cadeia de caracteres de conexão de banco de dados do Azure Cosmos é:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

saudação de cadeia de caracteres de conexão do banco de dados do Azure Cosmos conta pode ser recuperada da folha de chaves de saudação do hello portal do Azure, conforme descrito em [como toomanage uma conta de banco de dados do Azure Cosmos](manage-account.md), no entanto, Olá o nome do banco de dados de saudação deve toohello toobe anexado cadeia de caracteres de conexão no hello formato a seguir:

    Database=<CosmosDB Database>;

> [!NOTE]
> Use Olá Verifique se o comando tooensure que Olá instância de banco de dados do Azure Cosmos especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.
> 
> 

tooimport tooa única coleção, digite nome Olá Olá coleção toowhich dados serão importados e clique no botão Adicionar de saudação. tooimport toomultiple coleções, insira cada nome de coleção individualmente ou usar várias coleções de Olá toospecify de sintaxe a seguir: *collection_prefix*[index - índice do fim de iniciar]. Ao especificar várias coleções por meio da sintaxe de saudação mencionados acima, tenha em mente Olá seguinte:

1. Somente padrões de nome de intervalo inteiro têm suporte. Por exemplo, a especificação de coleção [0-3] produzirá Olá coleções a seguir: collection0, collection1, collection2, collection3.
2. Você pode usar uma sintaxe abreviada: collection[3] emitirá o mesmo conjunto de coleções mencionado na etapa 1.
3. Mais de uma substituição pode ser fornecida. Por exemplo, a coleção [0-1] [0-9] gerará 20 nomes de coleção com zeros à esquerda (collection01... 02,... 03).

Depois de hello nomes de coleção forem especificados, escolha desejado taxa de transferência de saudação do hello collection(s) (400 RUs too10, 000 RUs). Para uma importação com melhor desempenho, escolha uma taxa de transferência maior. Para obter mais informações sobre níveis de desempenho, consulte [Níveis de desempenho no Azure Cosmos DB](performance-levels.md).

> [!NOTE]
> configuração de taxa de transferência de desempenho de saudação só se aplica a criação de toocollection. Se Olá especificado coleção já existe, sua taxa de transferência não será modificada.
> 
> 

Ao importar coleções toomultiple, ferramenta de importação de saudação dá suporte a fragmentação de hash com base. Neste cenário, especifique a propriedade de documento de saudação desejar toouse como Olá chave de partição (se a chave de partição é deixada em branco, documentos serão fragmentados aleatoriamente em conjuntos de destino Olá).

Opcionalmente, você pode especificar qual campo na fonte de importação Olá deve ser usado como Olá propriedade de id do banco de dados do Azure Cosmos documento durante a importação da saudação (Observe que se documentos não contenham essa propriedade, em seguida, ferramenta de importação de saudação irá gerar um GUID como o valor da propriedade id Olá).

Há uma série de opções avançadas disponíveis durante a importação. Primeiro, enquanto a ferramenta de saudação inclui uma massa padrão importar (BulkInsert.js) de procedimento armazenado, você pode escolher toospecify seu próprio procedimento armazenado de importação:

 ![Captura de tela da opção de sproc de inserção em massa do Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

Adicionalmente, ao importar tipos de dados (por exemplo, do SQL Server ou do MongoDB), você pode escolher entre três opções de importação:

 ![Captura de tela das opções de importação de data e hora do Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* Cadeia de caracteres: Persistir como um valor de cadeia de caracteres
* Época: Persistir como um valor de número de época
* Ambos: Persistir com os valores de número de cadeia de caracteres e de época. Essa opção criará um sub-documento, por exemplo: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245}

Importador do Hello em massa de banco de dados do Azure Cosmos tem opções avançadas adicionais do hello seguintes:

1. Tamanho do lote: Olá ferramenta padrões tooa tamanho de lote de 50.  Se Olá documentos toobe importado grande, considere reduzir o tamanho do lote hello. Por outro lado, se Olá documentos toobe importado sejam pequeno, considere aumentar o tamanho do lote hello.
2. Tamanho máximo de Script (bytes): ferramenta de saudação padrões tooa tamanho de máximo de script de 512KB
3. Desabilitar a geração automática do Id: Se cada toobe documento importado contém um campo de id, em seguida, selecionar esta opção pode aumentar o desempenho. Documentos com um campo de ID exclusiva ausente não serão importados.
4. Os documentos atualização existente: Olá ferramenta padrões toonot substituindo os documentos existentes com conflitos de id. Esta opção permitirá a substituir documentos existentes por ids correspondentes. Esse recurso é útil para migrações de dados agendadas que atualizam documentos existentes.
5. Número de novas tentativas em caso de falha: especifica Olá número de vezes tooretry Olá conexão tooAzure Cosmos banco de dados no caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).
6. Intervalo de repetição: Especifica quanto tempo toowait entre repetindo Olá conexão tooAzure Cosmos banco de dados no caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).
7. Modo de Conexão: Especifica Olá toouse de modo de conexão com o banco de dados do Azure Cosmos. opções disponíveis de saudação são DirectTcp, DirectHttps e Gateway. modos de conexão direta de saudação são mais rapidamente, enquanto o modo de gateway Olá é firewall mais amigável pois ele usa apenas a porta 443.

![Captura de tela das opções avançadas de importação em massa do Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> Olá importar do modo DirectTcp tooconnection ferramenta padrões. Se você enfrentar problemas de firewall, alterne o modo de tooconnection Gateway, pois exige apenas a porta 443.
> 
> 

## <a id="DocumentDBSeqTarget"></a>tooimport toohello API DocumentDB (sequencial importação de registro)
Importador do Hello Azure Cosmos DB sequencial registro permite que você tooimport de qualquer uma das opções de origem disponível Olá em uma base de registro por registro. Você pode escolher essa opção se você estiver importando tooan coleção existente que já atingiu a cota de procedimentos armazenados. Olá ferramenta oferece suporte à importação tooa única coleção de banco de dados do Azure Cosmos (partição única e várias partições), bem como importação fragmentada no qual os dados são particionados em vários conjuntos de banco de dados do Azure Cosmos de partição única e/ou em várias partições. Para obter mais informações sobre o particionamento de dados, consulte [Particionamento e escala no Azure Cosmos DB](partition-data.md).

![Captura de tela das opções de importação de registro sequencial do Azure Cosmos DB](./media/import-data/documentdbsequential.png)

formato Olá Olá cadeia de caracteres de conexão de banco de dados do Azure Cosmos é:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

saudação de cadeia de caracteres de conexão do banco de dados do Azure Cosmos conta pode ser recuperada da folha de chaves de saudação do hello portal do Azure, conforme descrito em [como toomanage uma conta de banco de dados do Azure Cosmos](manage-account.md), no entanto, Olá o nome do banco de dados de saudação deve toohello toobe anexado cadeia de caracteres de conexão no hello formato a seguir:

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> Use Olá Verifique se o comando tooensure que Olá instância de banco de dados do Azure Cosmos especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.
> 
> 

tooimport tooa única coleção, digite nome Olá Olá coleção toowhich dados serão importados e clique no botão Adicionar de saudação. tooimport toomultiple coleções, insira cada nome de coleção individualmente ou usar várias coleções de Olá toospecify de sintaxe a seguir: *collection_prefix*[index - índice do fim de iniciar]. Ao especificar várias coleções por meio da sintaxe de saudação mencionados acima, tenha em mente Olá seguinte:

1. Somente padrões de nome de intervalo inteiro têm suporte. Por exemplo, a especificação de coleção [0-3] produzirá Olá coleções a seguir: collection0, collection1, collection2, collection3.
2. Você pode usar uma sintaxe abreviada: collection[3] emitirá o mesmo conjunto de coleções mencionado na etapa 1.
3. Mais de uma substituição pode ser fornecida. Por exemplo, a coleção [0-1] [0-9] gerará 20 nomes de coleção com zeros à esquerda (collection01... 02,... 03).

Depois de hello nomes de coleção forem especificados, escolha desejado taxa de transferência de saudação do hello collection(s) (400 RUs too250, 000 RUs). Para uma importação com melhor desempenho, escolha uma taxa de transferência maior. Para obter mais informações sobre níveis de desempenho, consulte [Níveis de desempenho no Azure Cosmos DB](performance-levels.md). Qualquer importar toocollections com taxa de transferência > 10.000 RUs exigirá uma chave de partição. Se você escolher toohave mais de 250.000 RUs, você precisará toofile uma solicitação em toohave portal Olá aumentado de sua conta.

> [!NOTE]
> configuração de taxa de transferência de saudação só se aplica a criação de toocollection. Se Olá especificado coleção já existe, sua taxa de transferência não será modificada.
> 
> 

Ao importar coleções toomultiple, ferramenta de importação de saudação dá suporte a fragmentação de hash com base. Neste cenário, especifique a propriedade de documento de saudação desejar toouse como Olá chave de partição (se a chave de partição é deixada em branco, documentos serão fragmentados aleatoriamente em conjuntos de destino Olá).

Opcionalmente, você pode especificar qual campo na fonte de importação Olá deve ser usado como Olá propriedade de id do banco de dados do Azure Cosmos documento durante a importação da saudação (Observe que se documentos não contenham essa propriedade, em seguida, ferramenta de importação de saudação irá gerar um GUID como o valor da propriedade id Olá).

Há uma série de opções avançadas disponíveis durante a importação. Primeiro, ao importar tipos de dados (por exemplo, do SQL Server ou do MongoDB), você pode escolher entre três opções de importação:

 ![Captura de tela das opções de importação de data e hora do Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* Cadeia de caracteres: Persistir como um valor de cadeia de caracteres
* Época: Persistir como um valor de número de época
* Ambos: Persistir com os valores de número de cadeia de caracteres e de época. Essa opção criará um sub-documento, por exemplo: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245}

Hello Azure Cosmos DB - importador de registro sequencial tem opções avançadas adicionais do hello seguintes:

1. Número de solicitações em paralelo: ferramenta de saudação padrões solicitações paralelas too2. Se Olá documentos toobe importado sejam pequeno, considere aumentar o número de saudação de solicitações em paralelo. Observe que, se esse número é gerado muito, Olá importação pode resultar de limitação.
2. Desabilitar a geração automática do Id: Se cada toobe documento importado contém um campo de id, em seguida, selecionar esta opção pode aumentar o desempenho. Documentos com um campo de ID exclusiva ausente não serão importados.
3. Os documentos atualização existente: Olá ferramenta padrões toonot substituindo os documentos existentes com conflitos de id. Esta opção permitirá a substituir documentos existentes por ids correspondentes. Esse recurso é útil para migrações de dados agendadas que atualizam documentos existentes.
4. Número de novas tentativas em caso de falha: especifica Olá número de vezes tooretry Olá conexão tooAzure Cosmos banco de dados no caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).
5. Intervalo de repetição: Especifica quanto tempo toowait entre repetindo Olá conexão tooAzure Cosmos banco de dados no caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).
6. Modo de Conexão: Especifica Olá toouse de modo de conexão com o banco de dados do Azure Cosmos. opções disponíveis de saudação são DirectTcp, DirectHttps e Gateway. modos de conexão direta de saudação são mais rapidamente, enquanto o modo de gateway Olá é firewall mais amigável pois ele usa apenas a porta 443.

![Captura de tela das opções avançadas de importação de registro sequencial do Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> Olá importar do modo DirectTcp tooconnection ferramenta padrões. Se você enfrentar problemas de firewall, alterne o modo de tooconnection Gateway, pois exige apenas a porta 443.
> 
> 

## <a id="IndexingPolicy"></a>Especificar uma política de indexação ao criar coleções do Azure Cosmos DB
Quando você permite a migração de saudação coleções de toocreate ferramenta durante a importação, você pode especificar a política de indexação de saudação de coleções de saudação. No hello avançado seção Opções de importação em massa de banco de dados do Azure Cosmos de hello e sequenciais do banco de dados do Azure Cosmos opções de registro, navegue toohello seção de política de indexação.

![Captura de tela das opções avançadas de Política de indexação do Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

Usando Olá opção de política de indexação avançada, você pode selecionar um arquivo de política de indexação, insira manualmente uma política de indexação ou selecionar de um conjunto de modelos padrão (clique direito na indexação de política de caixa de texto de saudação).

modelos de política de Olá Olá ferramenta fornece são:

* Padrão. Essa política é mais útil quando você está executando consultas de igualdade em cadeias de caracteres e usando as consultas ORDER BY, intervalo e igualdade para números. Essa política tem uma sobrecarga de armazenamento de índice menor que Intervalo.
* Intervalo. Essa política é mais útil quando você está usando consultas ORDER BY, intervalo e igualdade em números e cadeias de caracteres. Essa política tem uma sobrecarga de armazenamento de índice maior do que Padrão ou Hash.

![Captura de tela das opções avançadas de Política de indexação do Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> Se você não especificar uma política de indexação, a política padrão de saudação será aplicada. Para obter mais informações sobre políticas de indexação, consulte [Políticas de indexação do Azure Cosmos DB](indexing-policies.md).
> 
> 

## <a name="export-toojson-file"></a>Exportar arquivo tooJSON
exportação de JSON de banco de dados do Azure Cosmos Olá permite tooexport qualquer Olá disponíveis opções tooa JSON do arquivo de origem que contém uma matriz de documentos JSON. ferramenta Olá tratará exportação Olá para você, ou você pode escolher o comando de migração tooview Olá resultante e execute o comando de saudação por conta própria. arquivo JSON resultante de saudação pode ser armazenado localmente ou no armazenamento de BLOBs do Azure.

![Captura de tela da opção de exportação de arquivo local JSON do Azure Cosmos DB](./media/import-data/jsontarget.png)

![Captura de tela da opção de exportação de JSON do Armazenamento de blobs do Azure no Azure Cosmos DB](./media/import-data/jsontarget2.png)

Opcionalmente, você pode escolher Olá tooprettify resultante JSON, que aumentará o tamanho de saudação do documento resultante Olá enquanto tornar Olá conteúdo mais legível.

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a>Configuração avançada
Na tela de configuração avançada de hello, especifique o local de saudação do hello toowhich de arquivo de log você deseja que os erros gravados. Olá regras a seguir se aplicam a página toothis:

1. Se um nome de arquivo não for fornecido, serão retornados todos os erros na página de resultados de saudação.
2. Se for fornecido um nome de arquivo sem um diretório, em seguida, arquivo hello será criado (ou substituído) no diretório atual do ambiente hello.
3. Se você selecionar um existente será substituído arquivo e, em seguida, arquivo hello, não há nenhuma opção de anexar.

Em seguida, escolha se toolog todas as críticas, ou se nenhuma mensagem de erro. Finalmente, decida frequência Olá na mensagem de transferência da tela será atualizado com seu progresso.

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a>Confirme as configurações de importação e de linha de comando de exibição
1. Depois de especificar as informações de origem, informações de destino e configuração avançada, examine o resumo de migração hello e, opcionalmente, Olá resultantes do comando de migração (o comando de cópia Olá é útil tooautomate operações de importação) de exibição/copiar:
   
    ![Captura de tela da tela de resumo](./media/import-data/summary.png)
   
    ![Captura de tela da tela de resumo](./media/import-data/summarycommand.png)
2. Quando estiver satisfeito com suas opções de origem e de destino, clique em **Importar**. tempo decorrido de saudação, contagem transferida e informações de falha (se você não fornecer um nome de arquivo de configuração avançada de saudação) serão atualizadas à medida que importar hello está em processo. Uma vez concluído, você pode exportar resultados da saudação (por exemplo, toodeal com quaisquer falhas de importação).
   
    ![Captura de tela da opção de exportação de JSON do Azure Cosmos DB](./media/import-data/viewresults.png)
3. Você também pode iniciar uma nova importação, ao manter as configurações existentes do hello (por exemplo, escolha de informações, origem e destino de cadeia de caracteres de conexão, etc.) ou redefinir todos os valores.
   
    ![Captura de tela da opção de exportação de JSON do Azure Cosmos DB](./media/import-data/newimport.png)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez a seguir hello:

> [!div class="checklist"]
> * Ferramenta de migração de dados Olá instalada
> * Importou dados de diferentes fontes de dados
> * Exportados do banco de dados do Azure Cosmos tooJSON

Agora você pode continuar tutorial próxima toohello e aprender como tooquery dados usando o banco de dados do Azure Cosmos. 

> [!div class="nextstepaction"]
>[Como os dados tooquery?](../cosmos-db/tutorial-query-documentdb.md)
