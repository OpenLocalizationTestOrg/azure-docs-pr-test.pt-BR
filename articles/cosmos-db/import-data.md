---
title: "Ferramenta de migração de banco de dados do Azure Cosmos DB | Microsoft Docs"
description: "Saiba como usar as ferramentas de migração de dados de software livre do Azure Cosmos DB para importar dados para o Azure Cosmos DB de várias fontes, incluindo MongoDB, SQL Server, Armazenamento de tabelas, Amazon DynamoDB, CSV e arquivos JSON. Conversão de CSV para JSON."
keywords: "csv em json, ferramentas de migração de banco de dados, converter csv em json"
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
ms.openlocfilehash: 23a4a82dbdb611f4da90562af936fca28da9b24d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-data-into-azure-cosmos-db-for-the-documentdb-api"></a><span data-ttu-id="18e97-105">Como importar dados para o Azure Cosmos DB da API do DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="18e97-105">How to import data into Azure Cosmos DB for the DocumentDB API?</span></span>

<span data-ttu-id="18e97-106">Este tutorial fornece instruções sobre como usar a ferramenta BD Cosmos do Azure: Migração de Dados da API DocumentDB, que pode importar dados de várias fontes, incluindo arquivos JSON, arquivos CSV, SQL, MongoDB, Armazenamento de tabelas do Azure, Amazon DynamoDB e coleções da API DocumentDB do BD Cosmos do Azure para usar com o BD Cosmos do Azure e a API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="18e97-106">This tutorial provides instructions on using the Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and the DocumentDB API.</span></span> <span data-ttu-id="18e97-107">A ferramenta de Migração de Dados também pode ser usada ao migrar de uma coleção de partição única para uma coleção de várias partições na API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="18e97-107">The Data Migration tool can also be used when migrating from a single partition collection to a multi-partition collection for the DocumentDB API.</span></span>

<span data-ttu-id="18e97-108">A ferramenta de Migração de Dados só funciona durante a importação de dados para o Azure Cosmos DB para uso com a API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="18e97-108">The Data Migration tool only works when importing data into Azure Cosmos DB for use with the DocumentDB API.</span></span> <span data-ttu-id="18e97-109">No momento, não há suporte para a importação de dados para uso com a API de Tabela ou a API do Graph.</span><span class="sxs-lookup"><span data-stu-id="18e97-109">Importing data for use with the Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="18e97-110">Para importar dados para uso com a API do MongoDB, consulte [Azure Cosmos DB: Como migrar dados para a API do MongoDB?](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="18e97-110">To import data for use with the MongoDB API, see [Azure Cosmos DB: How to migrate data for the MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="18e97-111">Este tutorial cobre as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="18e97-111">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18e97-112">Instalação da ferramenta de Migração de Dados</span><span class="sxs-lookup"><span data-stu-id="18e97-112">Installing the Data Migration tool</span></span>
> * <span data-ttu-id="18e97-113">Importação de dados de diferentes fontes de dados</span><span class="sxs-lookup"><span data-stu-id="18e97-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="18e97-114">Exportação do Azure Cosmos DB para o JSON</span><span class="sxs-lookup"><span data-stu-id="18e97-114">Exporting from Azure Cosmos DB to JSON</span></span>

## <span data-ttu-id="18e97-115"><a id="Prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="18e97-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="18e97-116">Antes de seguir as instruções deste artigo, verifique se você tem os seguintes itens instalados:</span><span class="sxs-lookup"><span data-stu-id="18e97-116">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="18e97-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) ou superior.</span><span class="sxs-lookup"><span data-stu-id="18e97-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="18e97-118"><a id="Overviewl"></a>Visão geral da ferramenta de Migração de Dados</span><span class="sxs-lookup"><span data-stu-id="18e97-118"><a id="Overviewl"></a>Overview of the Data Migration tool</span></span>
<span data-ttu-id="18e97-119">A ferramenta de Migração de Dados é uma solução de software livre que importa dados para o Azure Cosmos DB de uma variedade de fontes, incluindo:</span><span class="sxs-lookup"><span data-stu-id="18e97-119">The Data Migration tool is an open source solution that imports data to Azure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="18e97-120">Arquivos JSON</span><span class="sxs-lookup"><span data-stu-id="18e97-120">JSON files</span></span>
* <span data-ttu-id="18e97-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="18e97-121">MongoDB</span></span>
* <span data-ttu-id="18e97-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="18e97-122">SQL Server</span></span>
* <span data-ttu-id="18e97-123">Arquivos CSV</span><span class="sxs-lookup"><span data-stu-id="18e97-123">CSV files</span></span>
* <span data-ttu-id="18e97-124">Armazenamento da tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="18e97-124">Azure Table storage</span></span>
* <span data-ttu-id="18e97-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="18e97-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="18e97-126">HBase</span><span class="sxs-lookup"><span data-stu-id="18e97-126">HBase</span></span>
* <span data-ttu-id="18e97-127">Coleções do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="18e97-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="18e97-128">Embora a ferramenta de importação inclua uma interface gráfica do usuário (dtui.exe), ela também pode ser controlada pela linha de comando (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="18e97-128">While the import tool includes a graphical user interface (dtui.exe), it can also be driven from the command line (dt.exe).</span></span> <span data-ttu-id="18e97-129">Na verdade, há uma opção de extrair o comando associado depois de configurar uma importação por meio da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="18e97-129">In fact, there is an option to output the associated command after setting up an import through the UI.</span></span> <span data-ttu-id="18e97-130">Dados de origem em tabela (por exemplo, arquivos do SQL Server ou CSV) podem ser transformados, de forma que relações hierárquicas (subdocumentos) podem ser criadas durante a importação.</span><span class="sxs-lookup"><span data-stu-id="18e97-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="18e97-131">Continue lendo para saber mais sobre as opções de origem, linhas de comando de exemplo para importar de cada origem, opções de destino e resultados de importação de visualização.</span><span class="sxs-lookup"><span data-stu-id="18e97-131">Keep reading to learn more about source options, sample command lines to import from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="18e97-132"><a id="Install"></a>Instalar a ferramenta de Migração de Dados</span><span class="sxs-lookup"><span data-stu-id="18e97-132"><a id="Install"></a>Install the Data Migration tool</span></span>
<span data-ttu-id="18e97-133">O código-fonte da ferramenta de migração está disponível no GitHub [nesse repositório](https://github.com/azure/azure-documentdb-datamigrationtool) e há uma versão compilada no [Centro de Download da Microsoft](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="18e97-133">The migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="18e97-134">Você pode compilar a solução ou simplesmente baixar e extrair a versão compilada em um diretório de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="18e97-134">You may either compile the solution or simply download and extract the compiled version to a directory of your choice.</span></span> <span data-ttu-id="18e97-135">Em seguida, execute um:</span><span class="sxs-lookup"><span data-stu-id="18e97-135">Then run either:</span></span>

* <span data-ttu-id="18e97-136">**Dtui.exe**: Versão da interface gráfica da ferramenta</span><span class="sxs-lookup"><span data-stu-id="18e97-136">**Dtui.exe**: Graphical interface version of the tool</span></span>
* <span data-ttu-id="18e97-137">**Dt.exe**: Versão de linha de comando da ferramenta</span><span class="sxs-lookup"><span data-stu-id="18e97-137">**Dt.exe**: Command-line version of the tool</span></span>

## <a name="import-data"></a><span data-ttu-id="18e97-138">Importar dados</span><span class="sxs-lookup"><span data-stu-id="18e97-138">Import data</span></span>

<span data-ttu-id="18e97-139">Depois de instalar a ferramenta, é hora de importar os dados.</span><span class="sxs-lookup"><span data-stu-id="18e97-139">Once you've installed the tool, it's time to import your data.</span></span> <span data-ttu-id="18e97-140">Que tipo de dados você deseja importar?</span><span class="sxs-lookup"><span data-stu-id="18e97-140">What kind of data do you want to import?</span></span>

* [<span data-ttu-id="18e97-141">Arquivos JSON</span><span class="sxs-lookup"><span data-stu-id="18e97-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="18e97-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="18e97-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="18e97-143">Arquivos de exportação do MongoDB</span><span class="sxs-lookup"><span data-stu-id="18e97-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="18e97-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="18e97-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="18e97-145">Arquivos CSV</span><span class="sxs-lookup"><span data-stu-id="18e97-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="18e97-146">Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="18e97-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="18e97-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="18e97-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="18e97-148">Blob</span><span class="sxs-lookup"><span data-stu-id="18e97-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="18e97-149">Coleções do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="18e97-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="18e97-150">HBase</span><span class="sxs-lookup"><span data-stu-id="18e97-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="18e97-151">Importação em massa do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="18e97-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="18e97-152">Importação de registro sequencial do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="18e97-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="18e97-153"><a id="JSON"></a>Para importar arquivos JSON</span><span class="sxs-lookup"><span data-stu-id="18e97-153"><a id="JSON"></a>To import JSON files</span></span>
<span data-ttu-id="18e97-154">A opção de importador de origem de arquivo JSON permite importar um ou mais arquivos JSON de documento único ou arquivos JSON que contêm uma matriz de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="18e97-154">The JSON file source importer option allows you to import one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="18e97-155">Ao adicionar pastas que contêm arquivos JSON para importar, você tem a opção de pesquisar recursivamente arquivos em subpastas.</span><span class="sxs-lookup"><span data-stu-id="18e97-155">When adding folders that contain JSON files to import, you have the option of recursively searching for files in subfolders.</span></span>

![Captura de tela das opções de origem do arquivo JSON — ferramentas de migração de banco de dados](./media/import-data/jsonsource.png)

<span data-ttu-id="18e97-157">Aqui estão alguns exemplos de linha de comando para importar os arquivos JSON:</span><span class="sxs-lookup"><span data-stu-id="18e97-157">Here are some command line samples to import JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition the data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="18e97-158"><a id="MongoDB"></a>Para importar do MongoDB</span><span class="sxs-lookup"><span data-stu-id="18e97-158"><a id="MongoDB"></a>To import from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18e97-159">Se você estiver importando para uma conta do Azure Cosmos DB com suporte para o MongoDB, siga estas [instruções](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="18e97-159">If you are importing to an Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="18e97-160">A opção de importador de origem do MongoDB permite importar de uma coleção do MongoDB individual e opcionalmente filtrar documentos usando uma consulta e/ou modificar a estrutura do documento usando uma projeção.</span><span class="sxs-lookup"><span data-stu-id="18e97-160">The MongoDB source importer option allows you to import from an individual MongoDB collection and optionally filter documents using a query and/or modify the document structure by using a projection.</span></span>  

![Captura de tela das opções de fonte do MongoDB](./media/import-data/mongodbsource.png)

<span data-ttu-id="18e97-162">A cadeia de conexão está no formato padrão do MongoDB:</span><span class="sxs-lookup"><span data-stu-id="18e97-162">The connection string is in the standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="18e97-163">Use o comando Verify para garantir que a instância do MongoDB especificada no campo de cadeia de conexão pode ser acessada.</span><span class="sxs-lookup"><span data-stu-id="18e97-163">Use the Verify command to ensure that the MongoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="18e97-164">Digite o nome da coleção por meio da qual os dados serão importados.</span><span class="sxs-lookup"><span data-stu-id="18e97-164">Enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="18e97-165">Você pode opcionalmente especificar ou fornecer um arquivo para uma consulta (por exemplo, {pop: {$gt: 5000}}) e/ou uma projeção (por exemplo, {loc:0}) para filtrar e moldar os dados a serem importados.</span><span class="sxs-lookup"><span data-stu-id="18e97-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) to both filter and shape the data to be imported.</span></span>

<span data-ttu-id="18e97-166">Aqui estão alguns exemplos de linha de comando para importar por meio do MongoDB:</span><span class="sxs-lookup"><span data-stu-id="18e97-166">Here are some command line samples to import from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match the query and exclude the loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="18e97-167"><a id="MongoDBExport"></a>Para importar arquivos de exportação do MongoDB</span><span class="sxs-lookup"><span data-stu-id="18e97-167"><a id="MongoDBExport"></a>To import MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18e97-168">Se você estiver importando para uma conta do Azure Cosmos DB com suporte para o MongoDB, siga estas [instruções](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="18e97-168">If you are importing to an Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="18e97-169">A opção do importador de origem de arquivo JSON de exportação do MongoDB permite que você importe um ou mais arquivos JSON produzidos por meio do utilitário mongoexport.</span><span class="sxs-lookup"><span data-stu-id="18e97-169">The MongoDB export JSON file source importer option allows you to import one or more JSON files produced from the mongoexport utility.</span></span>  

![Captura de tela das opções de fonte de exportação do MongoDB](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="18e97-171">Ao adicionar pastas que contêm arquivos JSON de exportação do MongoDB, você tem a opção de pesquisar recursivamente arquivos em subpastas.</span><span class="sxs-lookup"><span data-stu-id="18e97-171">When adding folders that contain MongoDB export JSON files for import, you have the option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="18e97-172">Aqui está um exemplo de linha de comando para importar de arquivos de JSON de exportação do MongoDB:</span><span class="sxs-lookup"><span data-stu-id="18e97-172">Here is a command line sample to import from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="18e97-173"><a id="SQL"></a>Para importar do SQL Server</span><span class="sxs-lookup"><span data-stu-id="18e97-173"><a id="SQL"></a>To import from SQL Server</span></span>
<span data-ttu-id="18e97-174">A opção do importador de origem do SQL permite importar de um banco de dados do SQL Server individual e, opcionalmente, filtrar os registros a serem importados usando uma consulta.</span><span class="sxs-lookup"><span data-stu-id="18e97-174">The SQL source importer option allows you to import from an individual SQL Server database and optionally filter the records to be imported using a query.</span></span> <span data-ttu-id="18e97-175">Além disso, você pode modificar a estrutura do documento, especificando um separador de aninhamento (falaremos mais sobre isso em instantes).</span><span class="sxs-lookup"><span data-stu-id="18e97-175">In addition, you can modify the document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Captura de tela das opções de origem do SQL — ferramentas de migração de banco de dados](./media/import-data/sqlexportsource.png)

<span data-ttu-id="18e97-177">O formato da cadeia de conexão é o formato da cadeia de conexão SQL padrão.</span><span class="sxs-lookup"><span data-stu-id="18e97-177">The format of the connection string is the standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="18e97-178">Use o comando Verify para garantir que a instância do SQL Server especificada no campo Cadeia de conexão pode ser acessada.</span><span class="sxs-lookup"><span data-stu-id="18e97-178">Use the Verify command to ensure that the SQL Server instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="18e97-179">A propriedade de separador de aninhamento é usada para criar relacionamentos hierárquicos (sub-documentos) durante a importação.</span><span class="sxs-lookup"><span data-stu-id="18e97-179">The nesting separator property is used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="18e97-180">Considere a seguinte consulta SQL:</span><span class="sxs-lookup"><span data-stu-id="18e97-180">Consider the following SQL query:</span></span>

<span data-ttu-id="18e97-181">*Selecione CAST (BusinessEntityID como varchar) como ID, Nome, AddressType como [Address.AddressType], AddressLine1 como [Address.AddressLine1], City como [Address.Location.City], StateProvinceName como [Address.Location.StateProvinceName], PostalCode como [Address.PostalCode], CountryRegionName como [Address.CountryRegionName] de Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span><span class="sxs-lookup"><span data-stu-id="18e97-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="18e97-182">Que retorna os seguintes resultados (parciais):</span><span class="sxs-lookup"><span data-stu-id="18e97-182">Which returns the following (partial) results:</span></span>

![Captura de tela dos resultados de consulta do SQL](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="18e97-184">Observe os aliases como Address.AddressType e Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="18e97-184">Note the aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="18e97-185">Especificando um separador de aninhamento de “.”, a ferramenta de importação cria os sub-documentos Address e Address.Location durante a importação.</span><span class="sxs-lookup"><span data-stu-id="18e97-185">By specifying a nesting separator of ‘.’, the import tool creates Address and Address.Location subdocuments during the import.</span></span> <span data-ttu-id="18e97-186">Este é um exemplo de um documento resultante no Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="18e97-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="18e97-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span><span class="sxs-lookup"><span data-stu-id="18e97-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="18e97-188">Aqui estão alguns exemplos de linha de comando para importar do SQL Server:</span><span class="sxs-lookup"><span data-stu-id="18e97-188">Here are some command line samples to import from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="18e97-189"><a id="CSV"></a>Para importar arquivos CSV e converter CSV em JSON</span><span class="sxs-lookup"><span data-stu-id="18e97-189"><a id="CSV"></a>To import CSV files and convert CSV to JSON</span></span>
<span data-ttu-id="18e97-190">A opção de importador de origem de arquivo CSV permite que você importe um ou mais arquivos CSV.</span><span class="sxs-lookup"><span data-stu-id="18e97-190">The CSV file source importer option enables you to import one or more CSV files.</span></span> <span data-ttu-id="18e97-191">Ao adicionar pastas que contêm arquivos CSV para importar, você tem a opção de pesquisar recursivamente arquivos em subpastas.</span><span class="sxs-lookup"><span data-stu-id="18e97-191">When adding folders that contain CSV files for import, you have the option of recursively searching for files in subfolders.</span></span>

![Captura de tela das opções de origem do CSV — CVS em JSON](media/import-data/csvsource.png)

<span data-ttu-id="18e97-193">De forma semelhante à origem de SQL, a propriedade de separador de aninhamento pode ser usada para criar relacionamentos hierárquicos (sub-documentos) durante a importação.</span><span class="sxs-lookup"><span data-stu-id="18e97-193">Similar to the SQL source, the nesting separator property may be used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="18e97-194">Considere a seguinte linha de cabeçalho CSV e linhas de dados:</span><span class="sxs-lookup"><span data-stu-id="18e97-194">Consider the following CSV header row and data rows:</span></span>

![Captura de tela dos registros de exemplo do CSV — CVS em JSON](./media/import-data/csvsample.png)

<span data-ttu-id="18e97-196">Observe os aliases como DomainInfo.Domain_Name e RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="18e97-196">Note the aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="18e97-197">Especificando um separador de aninhamento de “.”, a ferramenta de importação cria os sub-documentos DomainInfo e RedirectInfo durante a importação.</span><span class="sxs-lookup"><span data-stu-id="18e97-197">By specifying a nesting separator of ‘.’, the import tool will create DomainInfo and RedirectInfo subdocuments during the import.</span></span> <span data-ttu-id="18e97-198">Este é um exemplo de um documento resultante no Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="18e97-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="18e97-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span><span class="sxs-lookup"><span data-stu-id="18e97-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="18e97-200">A ferramenta de importação tentará deduzir informações de tipo para valores sem aspas em arquivos CSV (valores entre aspas são tratados sempre como cadeias de caracteres).</span><span class="sxs-lookup"><span data-stu-id="18e97-200">The import tool will attempt to infer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="18e97-201">Os tipos são identificados na seguinte ordem: número, datetime, booliano.</span><span class="sxs-lookup"><span data-stu-id="18e97-201">Types are identified in the following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="18e97-202">Há duas outras coisas a observar sobre a importação de CSV:</span><span class="sxs-lookup"><span data-stu-id="18e97-202">There are two other things to note about CSV import:</span></span>

1. <span data-ttu-id="18e97-203">Por padrão, os valores sem aspas sempre são cortados para tabulações e espaços, enquanto os valores entre aspas são preservados como estão.</span><span class="sxs-lookup"><span data-stu-id="18e97-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="18e97-204">Esse comportamento pode ser substituído por a caixa de seleção com valores entre aspas de corte ou pela opção de linha de comando /s.TrimQuoted.</span><span class="sxs-lookup"><span data-stu-id="18e97-204">This behavior can be overridden with the Trim quoted values checkbox or the /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="18e97-205">Por padrão, um nulo sem aspas é tratado como um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="18e97-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="18e97-206">Esse comportamento pode ser substituído (isto é, trate um nulo sem aspas como uma cadeia de caracteres "null") com o NULL de tratamento sem aspas como caixa de seleção da cadeia de caracteres ou a opção de linha de comando /s.NoUnquotedNulls.</span><span class="sxs-lookup"><span data-stu-id="18e97-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with the Treat unquoted NULL as string checkbox or the /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="18e97-207">Aqui está um exemplo de linha de comando para importação de CSV:</span><span class="sxs-lookup"><span data-stu-id="18e97-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="18e97-208"><a id="AzureTableSource"></a>Para importar do Armazenamento de tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="18e97-208"><a id="AzureTableSource"></a>To import from Azure Table storage</span></span>
<span data-ttu-id="18e97-209">A opção de importador de origem de armazenamento de tabela do Azure permite importar de uma tabela de armazenamento de uma tabela individual do Azure e filtrar opcionalmente as entidades da tabela a serem importadas.</span><span class="sxs-lookup"><span data-stu-id="18e97-209">The Azure Table storage source importer option allows you to import from an individual Azure Table storage table and optionally filter the table entities to be imported.</span></span> <span data-ttu-id="18e97-210">Observe que não é possível usar a ferramenta de Migração de Dados para importar dados do Armazenamento de tabelas do Azure para o Azure Cosmos DB para uso com a API de Tabela.</span><span class="sxs-lookup"><span data-stu-id="18e97-210">Note that you cannot use the Data Migration tool to import Azure Table storage data into Azure Cosmos DB for use with the Table API.</span></span> <span data-ttu-id="18e97-211">No momento, há suporte apenas para a importação do Azure Cosmos DB para uso com a API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="18e97-211">Only importing to Azure Cosmos DB for use with the DocumentDB API is supported at this time.</span></span>

![Captura de tela das opções de origem de armazenamento da tabela do Azure](./media/import-data/azuretablesource.png)

<span data-ttu-id="18e97-213">O formato da cadeia de conexão de armazenamento de tabela do Azure é:</span><span class="sxs-lookup"><span data-stu-id="18e97-213">The format of the Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="18e97-214">Use o comando Verify para garantir que a instância de armazenamento da tabela do Azure especificada no campo de cadeia de conexão pode ser acessada.</span><span class="sxs-lookup"><span data-stu-id="18e97-214">Use the Verify command to ensure that the Azure Table storage instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="18e97-215">Digite o nome da tabela do Azure por meio da qual os dados serão importados.</span><span class="sxs-lookup"><span data-stu-id="18e97-215">Enter the name of the Azure table from which data will be imported.</span></span> <span data-ttu-id="18e97-216">Opcionalmente, você pode especificar um [filtro](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="18e97-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="18e97-217">A opção de importador de origem de armazenamento de tabela do Azure tem as seguintes opções adicionais:</span><span class="sxs-lookup"><span data-stu-id="18e97-217">The Azure Table storage source importer option has the following additional options:</span></span>

1. <span data-ttu-id="18e97-218">Incluir campos internos</span><span class="sxs-lookup"><span data-stu-id="18e97-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="18e97-219">Todos - incluir todos os campos internos (PartitionKey, RowKey e Timestamp)</span><span class="sxs-lookup"><span data-stu-id="18e97-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="18e97-220">Nenhum - excluir todos os campos internos</span><span class="sxs-lookup"><span data-stu-id="18e97-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="18e97-221">RowKey - incluir somente o campo RowKey</span><span class="sxs-lookup"><span data-stu-id="18e97-221">RowKey - Only include the RowKey field</span></span>
2. <span data-ttu-id="18e97-222">Selecionar colunas</span><span class="sxs-lookup"><span data-stu-id="18e97-222">Select Columns</span></span>
   1. <span data-ttu-id="18e97-223">Filtros de armazenamento de tabela do Azure não dão suporte a projeções.</span><span class="sxs-lookup"><span data-stu-id="18e97-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="18e97-224">Se você quiser importar somente propriedades específicas de entidade da tabela do Azure, adicione-as à lista Selecionar colunas.</span><span class="sxs-lookup"><span data-stu-id="18e97-224">If you want to only import specific Azure Table entity properties, add them to the Select Columns list.</span></span> <span data-ttu-id="18e97-225">Todas as outras propriedades da entidade serão ignoradas.</span><span class="sxs-lookup"><span data-stu-id="18e97-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="18e97-226">Aqui está um exemplo de linha de comando para importar por meio do armazenamento de tabela do Azure:</span><span class="sxs-lookup"><span data-stu-id="18e97-226">Here is a command line sample to import from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="18e97-227"><a id="DynamoDBSource"></a>Para importar do Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="18e97-227"><a id="DynamoDBSource"></a>To import from Amazon DynamoDB</span></span>
<span data-ttu-id="18e97-228">A opção de importação de fonte do Amazon DynamoDB permite importar de uma tabela individual do Amazon DynamoDB e, opcionalmente, filtrar as entidades a serem importadas.</span><span class="sxs-lookup"><span data-stu-id="18e97-228">The Amazon DynamoDB source importer option allows you to import from an individual Amazon DynamoDB table and optionally filter the entities to be imported.</span></span> <span data-ttu-id="18e97-229">Vários modelos são fornecidos para que a configuração de uma importação seja tão fácil quanto possível.</span><span class="sxs-lookup"><span data-stu-id="18e97-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Captura de tela das opções de origem do Amazon DynamoDB — ferramentas de migração de banco de dados](./media/import-data/dynamodbsource1.png)

![Captura de tela das opções de origem do Amazon DynamoDB — ferramentas de migração de banco de dados](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="18e97-232">O formato da cadeia de conexão do Amazon DynamoDB é:</span><span class="sxs-lookup"><span data-stu-id="18e97-232">The format of the Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="18e97-233">Use o comando Verify para garantir que a instância do Amazon DynamoDB especificada no campo de cadeia de conexão possa ser acessada.</span><span class="sxs-lookup"><span data-stu-id="18e97-233">Use the Verify command to ensure that the Amazon DynamoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="18e97-234">Aqui está um exemplo de linha de comando para importar do Amazon DynamoDB:</span><span class="sxs-lookup"><span data-stu-id="18e97-234">Here is a command line sample to import from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="18e97-235"><a id="BlobImport"></a>Para importar arquivos do Armazenamento de blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="18e97-235"><a id="BlobImport"></a>To import files from Azure Blob storage</span></span>
<span data-ttu-id="18e97-236">O arquivo JSON, arquivo de exportação do MongoDB e opções de importador de origem do arquivo CSV permitem que você importe um ou mais arquivos de Armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="18e97-236">The JSON file, MongoDB export file, and CSV file source importer options allow you to import one or more files from Azure Blob storage.</span></span> <span data-ttu-id="18e97-237">Depois de especificar uma URL do contêiner de Blob e a chave de conta, basta fornece uma expressão regular para selecionar os arquivos a serem importados.</span><span class="sxs-lookup"><span data-stu-id="18e97-237">After specifying a Blob container URL and Account Key, simply provide a regular expression to select the file(s) to import.</span></span>

![Captura de tela das opções de origem de arquivo de blob](./media/import-data/blobsource.png)

<span data-ttu-id="18e97-239">Eis um exemplo de linha de comando para importar arquivos JSON do Armazenamento de Blob do Azure:</span><span class="sxs-lookup"><span data-stu-id="18e97-239">Here is command line sample to import JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="18e97-240"><a id="DocumentDBSource"></a>Para importar de uma coleção da API DocumentDB do BC Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="18e97-240"><a id="DocumentDBSource"></a>To import from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="18e97-241">A opção de importador de origem do Azure Cosmos DB permite importar dados de uma ou mais coleções do Azure Cosmos DB e, opcionalmente, filtrar documentos usando uma consulta.</span><span class="sxs-lookup"><span data-stu-id="18e97-241">The Azure Cosmos DB source importer option allows you to import data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Captura de tela das opções de fonte do Azure Cosmos DB](./media/import-data/documentdbsource.png)

<span data-ttu-id="18e97-243">O formato da cadeia de conexão do Azure Cosmos DB é:</span><span class="sxs-lookup"><span data-stu-id="18e97-243">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="18e97-244">A cadeia de conexão da conta do Azure Cosmos DB pode ser recuperada na folha Chaves do portal do Azure, conforme descrito em [Como gerenciar uma conta do Azure Cosmos DB](manage-account.md); no entanto, o nome do banco de dados deve ser acrescentado à cadeia de conexão no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="18e97-244">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="18e97-245">Use o comando Verify para garantir que a instância do Azure Cosmos DB especificada no campo de cadeia de conexão pode ser acessada.</span><span class="sxs-lookup"><span data-stu-id="18e97-245">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="18e97-246">Para importar de uma única coleção do Azure Cosmos DB, insira o nome da coleção da qual os dados serão importados.</span><span class="sxs-lookup"><span data-stu-id="18e97-246">To import from a single Azure Cosmos DB collection, enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="18e97-247">Para importar de várias coleções do Azure Cosmos DB, forneça uma expressão regular para corresponder um ou mais nomes de coleção (por exemplo, collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="18e97-247">To import from multiple Azure Cosmos DB collections, provide a regular expression to match one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="18e97-248">Você pode opcionalmente especificar ou fornecer um arquivo para uma consulta para filtrar e moldar os dados a serem importados.</span><span class="sxs-lookup"><span data-stu-id="18e97-248">You may optionally specify, or provide a file for, a query to both filter and shape the data to be imported.</span></span>

> [!NOTE]
> <span data-ttu-id="18e97-249">Uma vez que o campo de coleção aceita expressões regulares, se você estiver importando de uma única coleção cujo nome contém caracteres de expressão regular, esses caracteres devem ser substituídos adequadamente.</span><span class="sxs-lookup"><span data-stu-id="18e97-249">Since the collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="18e97-250">A opção de importador de origem do Azure Cosmos DB tem as seguintes opções avançadas:</span><span class="sxs-lookup"><span data-stu-id="18e97-250">The Azure Cosmos DB source importer option has the following advanced options:</span></span>

1. <span data-ttu-id="18e97-251">Incluir Campos Internos: especifica se as propriedades do sistema de documentos do Azure Cosmos DB devem ser incluídas na exportação (por exemplo, _rid, _ts).</span><span class="sxs-lookup"><span data-stu-id="18e97-251">Include Internal Fields: Specifies whether or not to include Azure Cosmos DB document system properties in the export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="18e97-252">Número de Repetições em Caso de Falha: especifica o número de vezes para tentar a conexão novamente com o Azure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="18e97-252">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="18e97-253">Intervalo de Repetição: especifica o tempo de espera para tentar a conexão novamente com o Azure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="18e97-253">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="18e97-254">Modo de Conexão: especifica o modo de conexão a ser usado com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="18e97-254">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="18e97-255">As opções disponíveis são DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="18e97-255">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="18e97-256">Os modos de conexão direta são mais rápidos, enquanto que o modo de gateway é mais amigável ao firewall, uma vez que só usa a porta 443.</span><span class="sxs-lookup"><span data-stu-id="18e97-256">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Captura de tela das opções avançadas de fonte do Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="18e97-258">A ferramenta de importação usa como padrão o modo de conexão DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="18e97-258">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="18e97-259">Se você enfrentar problemas de firewall, alterne para o modo de conexão Gateway, uma vez que ele só requer a porta 443.</span><span class="sxs-lookup"><span data-stu-id="18e97-259">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="18e97-260">Estas são algumas amostras de linha de comando para importar do Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="18e97-260">Here are some command line samples to import from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection to another Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections to a single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection to a JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="18e97-261">A ferramenta de Importação de Dados do Azure Cosmos DB também dá suporte à importação de dados do [Emulador do Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="18e97-261">The Azure Cosmos DB Data Import Tool also supports import of data from the [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="18e97-262">Ao importar dados de um emulador local, defina o ponto de extremidade como `https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="18e97-262">When importing data from a local emulator, set the endpoint to `https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="18e97-263"><a id="HBaseSource"></a>Para importar do HBase</span><span class="sxs-lookup"><span data-stu-id="18e97-263"><a id="HBaseSource"></a>To import from HBase</span></span>
<span data-ttu-id="18e97-264">A opção de importador de origem do HBase permite importar dados de uma tabela do HBase e, opcionalmente, filtrar os dados.</span><span class="sxs-lookup"><span data-stu-id="18e97-264">The HBase source importer option allows you to import data from an HBase table and optionally filter the data.</span></span> <span data-ttu-id="18e97-265">Vários modelos são fornecidos para que a configuração de uma importação seja tão fácil quanto possível.</span><span class="sxs-lookup"><span data-stu-id="18e97-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Captura de tela das opções de origem do HBase](./media/import-data/hbasesource1.png)

![Captura de tela das opções de origem do HBase](./media/import-data/hbasesource2.png)

<span data-ttu-id="18e97-268">O formato da cadeia de conexão HBase Stargate é:</span><span class="sxs-lookup"><span data-stu-id="18e97-268">The format of the HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="18e97-269">Use o comando Verify para garantir que a instância do HBase especificada no campo de cadeia de conexão possa ser acessada.</span><span class="sxs-lookup"><span data-stu-id="18e97-269">Use the Verify command to ensure that the HBase instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="18e97-270">Aqui está um exemplo de linha de comando para importar do HBase:</span><span class="sxs-lookup"><span data-stu-id="18e97-270">Here is a command line sample to import from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="18e97-271"><a id="DocumentDBBulkTarget"></a>Para importar para a API DocumentDB (importação em massa)</span><span class="sxs-lookup"><span data-stu-id="18e97-271"><a id="DocumentDBBulkTarget"></a>To import to the DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="18e97-272">O importador em Massa do Azure Cosmos DB permite importar de qualquer uma das opções de origem disponíveis, usando um procedimento armazenado do Azure Cosmos DB para maior eficiência.</span><span class="sxs-lookup"><span data-stu-id="18e97-272">The Azure Cosmos DB Bulk importer allows you to import from any of the available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="18e97-273">A ferramenta dá suporte à importação para uma coleção de partição única do Azure Cosmos DB, bem como à importação fragmentada, por meio da qual os dados são particionados em várias coleções de partição única do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="18e97-273">The tool supports import to one single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="18e97-274">Para obter mais informações sobre o particionamento de dados, consulte [Particionamento e escala no Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="18e97-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="18e97-275">A ferramenta vai criar, executar e, em seguida, excluir o procedimento armazenado da(s) coleção(ões) de destino.</span><span class="sxs-lookup"><span data-stu-id="18e97-275">The tool will create, execute, and then delete the stored procedure from the target collection(s).</span></span>  

![Captura de tela das opções em massa do Azure Cosmos DB](./media/import-data/documentdbbulk.png)

<span data-ttu-id="18e97-277">O formato da cadeia de conexão do Azure Cosmos DB é:</span><span class="sxs-lookup"><span data-stu-id="18e97-277">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="18e97-278">A cadeia de conexão da conta do Azure Cosmos DB pode ser recuperada na folha Chaves do portal do Azure, conforme descrito em [Como gerenciar uma conta do Azure Cosmos DB](manage-account.md); no entanto, o nome do banco de dados deve ser acrescentado à cadeia de conexão no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="18e97-278">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="18e97-279">Use o comando Verify para garantir que a instância do Azure Cosmos DB especificada no campo de cadeia de conexão pode ser acessada.</span><span class="sxs-lookup"><span data-stu-id="18e97-279">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="18e97-280">Para importar para uma única coleção, digite o nome da coleção à qual os dados serão importados e clique no botão Adicionar.</span><span class="sxs-lookup"><span data-stu-id="18e97-280">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="18e97-281">Para importar para várias coleções, insira o nome de cada coleção individualmente ou use a seguinte sintaxe para especificar várias coleções: *collection_prefix*[start index - end index].</span><span class="sxs-lookup"><span data-stu-id="18e97-281">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="18e97-282">Ao especificar várias coleções por meio da sintaxe mencionada anteriormente, lembre-se do seguinte:</span><span class="sxs-lookup"><span data-stu-id="18e97-282">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="18e97-283">Somente padrões de nome de intervalo inteiro têm suporte.</span><span class="sxs-lookup"><span data-stu-id="18e97-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="18e97-284">Por exemplo, a especificação de coleção [0-3] produzirá as seguintes coleções: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="18e97-284">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="18e97-285">Você pode usar uma sintaxe abreviada: collection[3] emitirá o mesmo conjunto de coleções mencionado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="18e97-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="18e97-286">Mais de uma substituição pode ser fornecida.</span><span class="sxs-lookup"><span data-stu-id="18e97-286">More than one substitution can be provided.</span></span> <span data-ttu-id="18e97-287">Por exemplo, a coleção [0-1] [0-9] gerará 20 nomes de coleção com zeros à esquerda (collection01... 02,... 03).</span><span class="sxs-lookup"><span data-stu-id="18e97-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="18e97-288">Depois de especificar o(s) nome(s) de coleção, escolha a taxa de transferência desejada da(s) coleção(ões) (de 400 a 10.000 RUs).</span><span class="sxs-lookup"><span data-stu-id="18e97-288">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 10,000 RUs).</span></span> <span data-ttu-id="18e97-289">Para uma importação com melhor desempenho, escolha uma taxa de transferência maior.</span><span class="sxs-lookup"><span data-stu-id="18e97-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="18e97-290">Para obter mais informações sobre níveis de desempenho, consulte [Níveis de desempenho no Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="18e97-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="18e97-291">A configuração de taxa de transferência de desempenho só se aplica à criação da coleção.</span><span class="sxs-lookup"><span data-stu-id="18e97-291">The performance throughput setting only applies to collection creation.</span></span> <span data-ttu-id="18e97-292">Se a coleção especificada já existir, sua taxa de transferência não será modificada.</span><span class="sxs-lookup"><span data-stu-id="18e97-292">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="18e97-293">Ao importar para várias coleções, a ferramenta de importação dá suporte a hash baseado em fragmentação.</span><span class="sxs-lookup"><span data-stu-id="18e97-293">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="18e97-294">Neste cenário, especifique a propriedade do documento que deseja usar como a Chave de partição (se a Chave de partição for deixada em branco, os documentos serão fragmentados aleatoriamente em coleções de destino).</span><span class="sxs-lookup"><span data-stu-id="18e97-294">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="18e97-295">Opcionalmente, você pode especificar qual campo na origem de importação deve ser usado como a propriedade de ID do documento do Azure Cosmos DB durante a importação (observe que se os documentos não contiverem essa propriedade, a ferramenta de importação gerará um GUID como o valor da propriedade de ID).</span><span class="sxs-lookup"><span data-stu-id="18e97-295">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="18e97-296">Há uma série de opções avançadas disponíveis durante a importação.</span><span class="sxs-lookup"><span data-stu-id="18e97-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="18e97-297">Em primeiro lugar, embora a ferramenta inclua um procedimento armazenado de importação em massa padrão (BulkInsert.js), você pode optar por especificar seu próprio procedimento armazenado de importação:</span><span class="sxs-lookup"><span data-stu-id="18e97-297">First, while the tool includes a default bulk import stored procedure (BulkInsert.js), you may choose to specify your own import stored procedure:</span></span>

 ![Captura de tela da opção de sproc de inserção em massa do Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="18e97-299">Adicionalmente, ao importar tipos de dados (por exemplo, do SQL Server ou do MongoDB), você pode escolher entre três opções de importação:</span><span class="sxs-lookup"><span data-stu-id="18e97-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Captura de tela das opções de importação de data e hora do Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="18e97-301">Cadeia de caracteres: Persistir como um valor de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="18e97-301">String: Persist as a string value</span></span>
* <span data-ttu-id="18e97-302">Época: Persistir como um valor de número de época</span><span class="sxs-lookup"><span data-stu-id="18e97-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="18e97-303">Ambos: Persistir com os valores de número de cadeia de caracteres e de época.</span><span class="sxs-lookup"><span data-stu-id="18e97-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="18e97-304">Essa opção criará um sub-documento, por exemplo: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245}</span><span class="sxs-lookup"><span data-stu-id="18e97-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="18e97-305">O importador em Massa do Azure Cosmos DB tem as seguintes opções avançadas adicionais:</span><span class="sxs-lookup"><span data-stu-id="18e97-305">The Azure Cosmos DB Bulk importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="18e97-306">Tamanho do lote: A ferramenta usa como padrão um tamanho de lote de 50.</span><span class="sxs-lookup"><span data-stu-id="18e97-306">Batch Size: The tool defaults to a batch size of 50.</span></span>  <span data-ttu-id="18e97-307">Se os documentos a serem importados forem grandes, considere reduzir o tamanho do lote.</span><span class="sxs-lookup"><span data-stu-id="18e97-307">If the documents to be imported are large, consider lowering the batch size.</span></span> <span data-ttu-id="18e97-308">Da mesma forma, se os documentos a serem importados forem pequenos, considere aumentar o tamanho do lote.</span><span class="sxs-lookup"><span data-stu-id="18e97-308">Conversely, if the documents to be imported are small, consider raising the batch size.</span></span>
2. <span data-ttu-id="18e97-309">Tamanho máximo de script (bytes): a ferramenta usa como padrão um tamanho máximo de script de 512KB</span><span class="sxs-lookup"><span data-stu-id="18e97-309">Max Script Size (bytes): The tool defaults to a max script size of 512KB</span></span>
3. <span data-ttu-id="18e97-310">Desabilitar a geração automática de ID: Se todos os documentos a serem importados contiverem um campo de identificação, selecionar essa opção pode aumentar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="18e97-310">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="18e97-311">Documentos com um campo de ID exclusiva ausente não serão importados.</span><span class="sxs-lookup"><span data-stu-id="18e97-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="18e97-312">Atualizar documentos existentes: a ferramenta por padrão não substitui os documentos existentes com conflitos de ID.</span><span class="sxs-lookup"><span data-stu-id="18e97-312">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="18e97-313">Esta opção permitirá a substituir documentos existentes por ids correspondentes.</span><span class="sxs-lookup"><span data-stu-id="18e97-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="18e97-314">Esse recurso é útil para migrações de dados agendadas que atualizam documentos existentes.</span><span class="sxs-lookup"><span data-stu-id="18e97-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="18e97-315">Número de Repetições em Caso de Falha: especifica o número de vezes para tentar a conexão novamente com o Azure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="18e97-315">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="18e97-316">Intervalo de Repetição: especifica o tempo de espera para tentar a conexão novamente com o Azure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="18e97-316">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="18e97-317">Modo de Conexão: especifica o modo de conexão a ser usado com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="18e97-317">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="18e97-318">As opções disponíveis são DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="18e97-318">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="18e97-319">Os modos de conexão direta são mais rápidos, enquanto que o modo de gateway é mais amigável ao firewall, uma vez que só usa a porta 443.</span><span class="sxs-lookup"><span data-stu-id="18e97-319">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Captura de tela das opções avançadas de importação em massa do Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="18e97-321">A ferramenta de importação usa como padrão o modo de conexão DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="18e97-321">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="18e97-322">Se você enfrentar problemas de firewall, alterne para o modo de conexão Gateway, uma vez que ele só requer a porta 443.</span><span class="sxs-lookup"><span data-stu-id="18e97-322">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="18e97-323"><a id="DocumentDBSeqTarget"></a>Para importar para a API DocumentDB (Importação de Registro Sequencial)</span><span class="sxs-lookup"><span data-stu-id="18e97-323"><a id="DocumentDBSeqTarget"></a>To import to the DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="18e97-324">O importador de registro sequencial do Azure Cosmos DB permite que você importe de qualquer uma das opções de origem disponíveis com base em cada registro.</span><span class="sxs-lookup"><span data-stu-id="18e97-324">The Azure Cosmos DB sequential record importer allows you to import from any of the available source options on a record by record basis.</span></span> <span data-ttu-id="18e97-325">Você pode escolher esta opção se estiver importando para uma coleção existente que já atingiu a cota de procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="18e97-325">You might choose this option if you’re importing to an existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="18e97-326">A ferramenta dá suporte à importação para uma coleção (com partição única e com várias partições) do Azure Cosmos DB, bem como à importação fragmentada, por meio da qual os dados são particionados em várias coleções de partição única e/ou com várias partições do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="18e97-326">The tool supports import to a single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="18e97-327">Para obter mais informações sobre o particionamento de dados, consulte [Particionamento e escala no Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="18e97-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Captura de tela das opções de importação de registro sequencial do Azure Cosmos DB](./media/import-data/documentdbsequential.png)

<span data-ttu-id="18e97-329">O formato da cadeia de conexão do Azure Cosmos DB é:</span><span class="sxs-lookup"><span data-stu-id="18e97-329">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="18e97-330">A cadeia de conexão da conta do Azure Cosmos DB pode ser recuperada na folha Chaves do portal do Azure, conforme descrito em [Como gerenciar uma conta do Azure Cosmos DB](manage-account.md); no entanto, o nome do banco de dados deve ser acrescentado à cadeia de conexão no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="18e97-330">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="18e97-331">Use o comando Verify para garantir que a instância do Azure Cosmos DB especificada no campo de cadeia de conexão pode ser acessada.</span><span class="sxs-lookup"><span data-stu-id="18e97-331">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="18e97-332">Para importar para uma única coleção, digite o nome da coleção à qual os dados serão importados e clique no botão Adicionar.</span><span class="sxs-lookup"><span data-stu-id="18e97-332">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="18e97-333">Para importar para várias coleções, insira o nome de cada coleção individualmente ou use a seguinte sintaxe para especificar várias coleções: *collection_prefix*[start index - end index].</span><span class="sxs-lookup"><span data-stu-id="18e97-333">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="18e97-334">Ao especificar várias coleções por meio da sintaxe mencionada anteriormente, lembre-se do seguinte:</span><span class="sxs-lookup"><span data-stu-id="18e97-334">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="18e97-335">Somente padrões de nome de intervalo inteiro têm suporte.</span><span class="sxs-lookup"><span data-stu-id="18e97-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="18e97-336">Por exemplo, a especificação de coleção [0-3] produzirá as seguintes coleções: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="18e97-336">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="18e97-337">Você pode usar uma sintaxe abreviada: collection[3] emitirá o mesmo conjunto de coleções mencionado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="18e97-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="18e97-338">Mais de uma substituição pode ser fornecida.</span><span class="sxs-lookup"><span data-stu-id="18e97-338">More than one substitution can be provided.</span></span> <span data-ttu-id="18e97-339">Por exemplo, a coleção [0-1] [0-9] gerará 20 nomes de coleção com zeros à esquerda (collection01... 02,... 03).</span><span class="sxs-lookup"><span data-stu-id="18e97-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="18e97-340">Depois de especificar o(s) nome(s) de coleção, escolha a taxa de transferência desejada da(s) coleção(ões) (de 400 a 250.000 RUs).</span><span class="sxs-lookup"><span data-stu-id="18e97-340">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 250,000 RUs).</span></span> <span data-ttu-id="18e97-341">Para uma importação com melhor desempenho, escolha uma taxa de transferência maior.</span><span class="sxs-lookup"><span data-stu-id="18e97-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="18e97-342">Para obter mais informações sobre níveis de desempenho, consulte [Níveis de desempenho no Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="18e97-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="18e97-343">Qualquer importação para coleções com taxa de transferência acima de 10.000 RUs exigirá uma chave de partição.</span><span class="sxs-lookup"><span data-stu-id="18e97-343">Any import to collections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="18e97-344">Se optar por ter mais de 250.000 RUs, você precisará fazer uma solicitação no portal para aumento da conta.</span><span class="sxs-lookup"><span data-stu-id="18e97-344">If you choose to have more than 250,000 RUs, you will need to file a request in the portal to have your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="18e97-345">A configuração de taxa de transferência só se aplica à criação da coleção.</span><span class="sxs-lookup"><span data-stu-id="18e97-345">The throughput setting only applies to collection creation.</span></span> <span data-ttu-id="18e97-346">Se a coleção especificada já existir, sua taxa de transferência não será modificada.</span><span class="sxs-lookup"><span data-stu-id="18e97-346">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="18e97-347">Ao importar para várias coleções, a ferramenta de importação dá suporte a hash baseado em fragmentação.</span><span class="sxs-lookup"><span data-stu-id="18e97-347">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="18e97-348">Neste cenário, especifique a propriedade do documento que deseja usar como a Chave de partição (se a Chave de partição for deixada em branco, os documentos serão fragmentados aleatoriamente em coleções de destino).</span><span class="sxs-lookup"><span data-stu-id="18e97-348">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="18e97-349">Opcionalmente, você pode especificar qual campo na origem de importação deve ser usado como a propriedade de ID do documento do Azure Cosmos DB durante a importação (observe que se os documentos não contiverem essa propriedade, a ferramenta de importação gerará um GUID como o valor da propriedade de ID).</span><span class="sxs-lookup"><span data-stu-id="18e97-349">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="18e97-350">Há uma série de opções avançadas disponíveis durante a importação.</span><span class="sxs-lookup"><span data-stu-id="18e97-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="18e97-351">Primeiro, ao importar tipos de dados (por exemplo, do SQL Server ou do MongoDB), você pode escolher entre três opções de importação:</span><span class="sxs-lookup"><span data-stu-id="18e97-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Captura de tela das opções de importação de data e hora do Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="18e97-353">Cadeia de caracteres: Persistir como um valor de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="18e97-353">String: Persist as a string value</span></span>
* <span data-ttu-id="18e97-354">Época: Persistir como um valor de número de época</span><span class="sxs-lookup"><span data-stu-id="18e97-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="18e97-355">Ambos: Persistir com os valores de número de cadeia de caracteres e de época.</span><span class="sxs-lookup"><span data-stu-id="18e97-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="18e97-356">Essa opção criará um sub-documento, por exemplo: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245}</span><span class="sxs-lookup"><span data-stu-id="18e97-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="18e97-357">O importador de Registro sequencial do Azure Cosmos DB tem as seguintes opções avançadas adicionais:</span><span class="sxs-lookup"><span data-stu-id="18e97-357">The Azure Cosmos DB - Sequential record importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="18e97-358">Número de solicitações paralelas: A ferramenta usa como padrão 2 solicitações paralelas.</span><span class="sxs-lookup"><span data-stu-id="18e97-358">Number of Parallel Requests: The tool defaults to 2 parallel requests.</span></span> <span data-ttu-id="18e97-359">Se os documentos a serem importados forem pequenos, considere aumentar o número de solicitações paralelas.</span><span class="sxs-lookup"><span data-stu-id="18e97-359">If the documents to be imported are small, consider raising the number of parallel requests.</span></span> <span data-ttu-id="18e97-360">Observe que se esse número for muito elevado, a importação poderá sofrer limitação.</span><span class="sxs-lookup"><span data-stu-id="18e97-360">Note that if this number is raised too much, the import may experience throttling.</span></span>
2. <span data-ttu-id="18e97-361">Desabilitar a geração automática de ID: Se todos os documentos a serem importados contiverem um campo de identificação, selecionar essa opção pode aumentar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="18e97-361">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="18e97-362">Documentos com um campo de ID exclusiva ausente não serão importados.</span><span class="sxs-lookup"><span data-stu-id="18e97-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="18e97-363">Atualizar documentos existentes: a ferramenta por padrão não substitui os documentos existentes com conflitos de ID.</span><span class="sxs-lookup"><span data-stu-id="18e97-363">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="18e97-364">Esta opção permitirá a substituir documentos existentes por ids correspondentes.</span><span class="sxs-lookup"><span data-stu-id="18e97-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="18e97-365">Esse recurso é útil para migrações de dados agendadas que atualizam documentos existentes.</span><span class="sxs-lookup"><span data-stu-id="18e97-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="18e97-366">Número de Repetições em Caso de Falha: especifica o número de vezes para tentar a conexão novamente com o Azure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="18e97-366">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="18e97-367">Intervalo de Repetição: especifica o tempo de espera para tentar a conexão novamente com o Azure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="18e97-367">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="18e97-368">Modo de Conexão: especifica o modo de conexão a ser usado com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="18e97-368">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="18e97-369">As opções disponíveis são DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="18e97-369">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="18e97-370">Os modos de conexão direta são mais rápidos, enquanto que o modo de gateway é mais amigável ao firewall, uma vez que só usa a porta 443.</span><span class="sxs-lookup"><span data-stu-id="18e97-370">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Captura de tela das opções avançadas de importação de registro sequencial do Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="18e97-372">A ferramenta de importação usa como padrão o modo de conexão DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="18e97-372">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="18e97-373">Se você enfrentar problemas de firewall, alterne para o modo de conexão Gateway, uma vez que ele só requer a porta 443.</span><span class="sxs-lookup"><span data-stu-id="18e97-373">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="18e97-374"><a id="IndexingPolicy"></a>Especificar uma política de indexação ao criar coleções do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="18e97-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="18e97-375">Quando você permite que a ferramenta de migração crie coleções durante a importação, pode especificar a política de indexação das coleções.</span><span class="sxs-lookup"><span data-stu-id="18e97-375">When you allow the migration tool to create collections during import, you can specify the indexing policy of the collections.</span></span> <span data-ttu-id="18e97-376">Na seção de opções avançadas das opções de Importação em massa e Registro sequencial do Azure Cosmos DB, navegue para a seção Política de indexação.</span><span class="sxs-lookup"><span data-stu-id="18e97-376">In the advanced options section of the Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate to the Indexing Policy section.</span></span>

![Captura de tela das opções avançadas de Política de indexação do Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="18e97-378">Usando a opção avançada de política de indexação, você pode selecionar um arquivo de política de indexação, inserir manualmente uma política de indexação ou selecionar a partir um conjunto de modelos padrão (clicando com o botão direito na caixa de texto da política indexação).</span><span class="sxs-lookup"><span data-stu-id="18e97-378">Using the Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in the indexing policy textbox).</span></span>

<span data-ttu-id="18e97-379">Os modelos de política que a ferramenta fornece são:</span><span class="sxs-lookup"><span data-stu-id="18e97-379">The policy templates the tool provides are:</span></span>

* <span data-ttu-id="18e97-380">Padrão.</span><span class="sxs-lookup"><span data-stu-id="18e97-380">Default.</span></span> <span data-ttu-id="18e97-381">Essa política é mais útil quando você está executando consultas de igualdade em cadeias de caracteres e usando as consultas ORDER BY, intervalo e igualdade para números.</span><span class="sxs-lookup"><span data-stu-id="18e97-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="18e97-382">Essa política tem uma sobrecarga de armazenamento de índice menor que Intervalo.</span><span class="sxs-lookup"><span data-stu-id="18e97-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="18e97-383">Intervalo.</span><span class="sxs-lookup"><span data-stu-id="18e97-383">Range.</span></span> <span data-ttu-id="18e97-384">Essa política é mais útil quando você está usando consultas ORDER BY, intervalo e igualdade em números e cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="18e97-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="18e97-385">Essa política tem uma sobrecarga de armazenamento de índice maior do que Padrão ou Hash.</span><span class="sxs-lookup"><span data-stu-id="18e97-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Captura de tela das opções avançadas de Política de indexação do Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="18e97-387">Se você não especificar uma política de indexação, a política padrão será aplicada.</span><span class="sxs-lookup"><span data-stu-id="18e97-387">If you do not specify an indexing policy, then the default policy will be applied.</span></span> <span data-ttu-id="18e97-388">Para obter mais informações sobre políticas de indexação, consulte [Políticas de indexação do Azure Cosmos DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="18e97-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-to-json-file"></a><span data-ttu-id="18e97-389">Exportar para arquivo JSON</span><span class="sxs-lookup"><span data-stu-id="18e97-389">Export to JSON file</span></span>
<span data-ttu-id="18e97-390">O exportador de JSON do Azure Cosmos DB permite exportar uma das opções de origem disponíveis para um arquivo JSON que contém uma matriz de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="18e97-390">The Azure Cosmos DB JSON exporter allows you to export any of the available source options to a JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="18e97-391">A ferramenta manipulará a exportação por você, ou você pode optar por exibir o comando de migração resultante e executar o comando por conta própria.</span><span class="sxs-lookup"><span data-stu-id="18e97-391">The tool will handle the export for you, or you can choose to view the resulting migration command and run the command yourself.</span></span> <span data-ttu-id="18e97-392">O arquivo JSON resultante pode ser armazenado localmente ou no Armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="18e97-392">The resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Captura de tela da opção de exportação de arquivo local JSON do Azure Cosmos DB](./media/import-data/jsontarget.png)

![Captura de tela da opção de exportação de JSON do Armazenamento de blobs do Azure no Azure Cosmos DB](./media/import-data/jsontarget2.png)

<span data-ttu-id="18e97-395">Você pode optar por melhorar a aparência do JSON resultante, o que aumentará o tamanho do documento resultante, tornando o conteúdo mais legível.</span><span class="sxs-lookup"><span data-stu-id="18e97-395">You may optionally choose to prettify the resulting JSON, which will increase the size of the resulting document while making the contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places to see in Paris"}]}]

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
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places to see in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="18e97-396">Configuração avançada</span><span class="sxs-lookup"><span data-stu-id="18e97-396">Advanced configuration</span></span>
<span data-ttu-id="18e97-397">Na tela de Configuração avançada, especifique a localização do arquivo de log do qual você gostaria que os erros fossem gravados.</span><span class="sxs-lookup"><span data-stu-id="18e97-397">In the Advanced configuration screen, specify the location of the log file to which you would like any errors written.</span></span> <span data-ttu-id="18e97-398">As seguintes regras se aplicam a esta página:</span><span class="sxs-lookup"><span data-stu-id="18e97-398">The following rules apply to this page:</span></span>

1. <span data-ttu-id="18e97-399">Se não for fornecido um nome de arquivo, todos os erros serão retornados na página Resultados.</span><span class="sxs-lookup"><span data-stu-id="18e97-399">If a file name is not provided, then all errors will be returned on the Results page.</span></span>
2. <span data-ttu-id="18e97-400">Se for fornecido um nome de arquivo sem um diretório, o arquivo será ser criado (ou substituído) no diretório atual do ambiente.</span><span class="sxs-lookup"><span data-stu-id="18e97-400">If a file name is provided without a directory, then the file will be created (or overwritten) in the current environment directory.</span></span>
3. <span data-ttu-id="18e97-401">Se você selecionar um arquivo existente, o arquivo será substituído, não há nenhuma opção de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="18e97-401">If you select an existing file, then the file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="18e97-402">Em seguida, escolha se deseja registrar, todas as mensagens de erro, nenhuma mensagem ou as mensagens críticas.</span><span class="sxs-lookup"><span data-stu-id="18e97-402">Then, choose whether to log all, critical, or no error messages.</span></span> <span data-ttu-id="18e97-403">Finalmente, decida com que frequência a mensagem de transferência na tela será atualizada com seu progresso.</span><span class="sxs-lookup"><span data-stu-id="18e97-403">Finally, decide how frequently the on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="18e97-404">Confirme as configurações de importação e de linha de comando de exibição</span><span class="sxs-lookup"><span data-stu-id="18e97-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="18e97-405">Depois de especificar as informações de origem, as informações de destino e a configuração avançada, examine a resumo de migração e, opcionalmente, examine/copie o comando resultante da migração (copiar o comando é útil para automatizar as operações de importação):</span><span class="sxs-lookup"><span data-stu-id="18e97-405">After specifying source information, target information, and advanced configuration, review the migration summary and, optionally, view/copy the resulting migration command (copying the command is useful to automate import operations):</span></span>
   
    ![Captura de tela da tela de resumo](./media/import-data/summary.png)
   
    ![Captura de tela da tela de resumo](./media/import-data/summarycommand.png)
2. <span data-ttu-id="18e97-408">Quando estiver satisfeito com suas opções de origem e de destino, clique em **Importar**.</span><span class="sxs-lookup"><span data-stu-id="18e97-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="18e97-409">O tempo decorrido, a contagem transferida e as informações de falha (se você não fornecer um nome de arquivo na Configuração avançada) serão atualizados à medida que a importação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="18e97-409">The elapsed time, transferred count, and failure information (if you didn't provide a file name in the Advanced configuration) will update as the import is in process.</span></span> <span data-ttu-id="18e97-410">Uma vez concluído, você pode exportar os resultados (por exemplo, para lidar com as falhas de importação).</span><span class="sxs-lookup"><span data-stu-id="18e97-410">Once complete, you can export the results (e.g. to deal with any import failures).</span></span>
   
    ![Captura de tela da opção de exportação de JSON do Azure Cosmos DB](./media/import-data/viewresults.png)
3. <span data-ttu-id="18e97-412">Você também pode iniciar uma nova importação, mantendo as configurações existentes (por exemplo, informações da cadeia de conexão, escolha de origem e destino, etc.) ou redefinindo todos os valores.</span><span class="sxs-lookup"><span data-stu-id="18e97-412">You may also start a new import, either keeping the existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Captura de tela da opção de exportação de JSON do Azure Cosmos DB](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="18e97-414">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="18e97-414">Next steps</span></span>

<span data-ttu-id="18e97-415">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="18e97-415">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18e97-416">Instalou a ferramenta de Migração de Dados</span><span class="sxs-lookup"><span data-stu-id="18e97-416">Installed the Data Migration tool</span></span>
> * <span data-ttu-id="18e97-417">Importou dados de diferentes fontes de dados</span><span class="sxs-lookup"><span data-stu-id="18e97-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="18e97-418">Exportou do Azure Cosmos DB para o JSON</span><span class="sxs-lookup"><span data-stu-id="18e97-418">Exported from Azure Cosmos DB to JSON</span></span>

<span data-ttu-id="18e97-419">Agora, você pode seguir para o próximo tutorial e saber como consultar dados usando o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="18e97-419">You can now proceed to the next tutorial and learn how to query data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="18e97-420">Como consultar os dados?</span><span class="sxs-lookup"><span data-stu-id="18e97-420">How to query data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
