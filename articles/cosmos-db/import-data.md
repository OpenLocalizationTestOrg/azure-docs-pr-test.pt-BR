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
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a><span data-ttu-id="f65d9-105">Como tooimport dados no banco de dados do Azure Cosmos para Olá API DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="f65d9-105">How tooimport data into Azure Cosmos DB for hello DocumentDB API?</span></span>

<span data-ttu-id="f65d9-106">Este tutorial fornece instruções sobre como usar o hello Azure Cosmos DB: ferramenta de migração de dados de API de documentos, que pode importar dados de várias fontes, incluindo arquivos JSON, arquivos CSV, SQL, MongoDB, armazenamento de tabela do Azure, DynamoDB Amazon e documentos de banco de dados do Azure Cosmos Conjuntos de API em conjuntos para usam com o banco de dados do Azure Cosmos e hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f65d9-106">This tutorial provides instructions on using hello Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and hello DocumentDB API.</span></span> <span data-ttu-id="f65d9-107">ferramenta de migração de dados de saudação também pode ser usada ao migrar de uma única partição tooa várias partições coleção para Olá API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f65d9-107">hello Data Migration tool can also be used when migrating from a single partition collection tooa multi-partition collection for hello DocumentDB API.</span></span>

<span data-ttu-id="f65d9-108">ferramenta de migração de dados Olá só funciona quando a importação de dados no banco de dados do Azure Cosmos para usa com hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f65d9-108">hello Data Migration tool only works when importing data into Azure Cosmos DB for use with hello DocumentDB API.</span></span> <span data-ttu-id="f65d9-109">Não há suporte para a importação de dados para uso com hello API de tabela ou a API do Graph neste momento.</span><span class="sxs-lookup"><span data-stu-id="f65d9-109">Importing data for use with hello Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="f65d9-110">dados tooimport para uso com hello MongoDB API, consulte [o banco de dados do Azure Cosmos: como dados toomigrate Olá MongoDB API?](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="f65d9-110">tooimport data for use with hello MongoDB API, see [Azure Cosmos DB: How toomigrate data for hello MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="f65d9-111">Este tutorial aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f65d9-111">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f65d9-112">Instalação da ferramenta de migração de dados Olá</span><span class="sxs-lookup"><span data-stu-id="f65d9-112">Installing hello Data Migration tool</span></span>
> * <span data-ttu-id="f65d9-113">Importação de dados de diferentes fontes de dados</span><span class="sxs-lookup"><span data-stu-id="f65d9-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="f65d9-114">Exportação do banco de dados do Azure Cosmos tooJSON</span><span class="sxs-lookup"><span data-stu-id="f65d9-114">Exporting from Azure Cosmos DB tooJSON</span></span>

## <span data-ttu-id="f65d9-115"><a id="Prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f65d9-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="f65d9-116">Antes de seguir as instruções neste artigo hello, certifique-se de que você tenha a seguinte Olá instalado:</span><span class="sxs-lookup"><span data-stu-id="f65d9-116">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="f65d9-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) ou superior.</span><span class="sxs-lookup"><span data-stu-id="f65d9-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="f65d9-118"><a id="Overviewl"></a>Visão geral da ferramenta de migração de dados Olá</span><span class="sxs-lookup"><span data-stu-id="f65d9-118"><a id="Overviewl"></a>Overview of hello Data Migration tool</span></span>
<span data-ttu-id="f65d9-119">ferramenta de migração de dados de saudação é uma solução de software livre que importa dados tooAzure Cosmos banco de dados de uma variedade de fontes, incluindo:</span><span class="sxs-lookup"><span data-stu-id="f65d9-119">hello Data Migration tool is an open source solution that imports data tooAzure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="f65d9-120">Arquivos JSON</span><span class="sxs-lookup"><span data-stu-id="f65d9-120">JSON files</span></span>
* <span data-ttu-id="f65d9-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="f65d9-121">MongoDB</span></span>
* <span data-ttu-id="f65d9-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="f65d9-122">SQL Server</span></span>
* <span data-ttu-id="f65d9-123">Arquivos CSV</span><span class="sxs-lookup"><span data-stu-id="f65d9-123">CSV files</span></span>
* <span data-ttu-id="f65d9-124">Armazenamento da tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="f65d9-124">Azure Table storage</span></span>
* <span data-ttu-id="f65d9-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="f65d9-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="f65d9-126">HBase</span><span class="sxs-lookup"><span data-stu-id="f65d9-126">HBase</span></span>
* <span data-ttu-id="f65d9-127">Coleções do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f65d9-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="f65d9-128">Enquanto a ferramenta de importação de saudação inclui uma interface gráfica do usuário (dtui.exe), ele também pode ser controlado pela linha de comando da saudação (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="f65d9-128">While hello import tool includes a graphical user interface (dtui.exe), it can also be driven from hello command line (dt.exe).</span></span> <span data-ttu-id="f65d9-129">Na verdade, há um comando de saudação associado toooutput opção depois de configurar uma importação por meio de saudação da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="f65d9-129">In fact, there is an option toooutput hello associated command after setting up an import through hello UI.</span></span> <span data-ttu-id="f65d9-130">Dados de origem em tabela (por exemplo, arquivos do SQL Server ou CSV) podem ser transformados, de forma que relações hierárquicas (subdocumentos) podem ser criadas durante a importação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="f65d9-131">Manter toolearn de ler mais sobre as opções de fonte, tooimport de linhas de comando de exemplo de cada fonte, opções de destino e a exibição de resultados de importação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-131">Keep reading toolearn more about source options, sample command lines tooimport from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="f65d9-132"><a id="Install"></a>Instalar a ferramenta de migração de dados Olá</span><span class="sxs-lookup"><span data-stu-id="f65d9-132"><a id="Install"></a>Install hello Data Migration tool</span></span>
<span data-ttu-id="f65d9-133">código-fonte Olá migração ferramenta está disponível no GitHub no [este repositório](https://github.com/azure/azure-documentdb-datamigrationtool) e uma versão compilada está disponível em [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="f65d9-133">hello migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="f65d9-134">Você pode compilar solução hello ou simplesmente baixar e extrair o diretório de tooa Olá versão compilada de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="f65d9-134">You may either compile hello solution or simply download and extract hello compiled version tooa directory of your choice.</span></span> <span data-ttu-id="f65d9-135">Em seguida, execute um:</span><span class="sxs-lookup"><span data-stu-id="f65d9-135">Then run either:</span></span>

* <span data-ttu-id="f65d9-136">**Dtui.exe**: versão de interface gráfica da ferramenta de saudação</span><span class="sxs-lookup"><span data-stu-id="f65d9-136">**Dtui.exe**: Graphical interface version of hello tool</span></span>
* <span data-ttu-id="f65d9-137">**DT.exe**: versão de linha de comando da ferramenta de saudação</span><span class="sxs-lookup"><span data-stu-id="f65d9-137">**Dt.exe**: Command-line version of hello tool</span></span>

## <a name="import-data"></a><span data-ttu-id="f65d9-138">Importar dados</span><span class="sxs-lookup"><span data-stu-id="f65d9-138">Import data</span></span>

<span data-ttu-id="f65d9-139">Depois de instalar a ferramenta Olá, é hora tooimport seus dados.</span><span class="sxs-lookup"><span data-stu-id="f65d9-139">Once you've installed hello tool, it's time tooimport your data.</span></span> <span data-ttu-id="f65d9-140">O tipo de dados você deseja tooimport?</span><span class="sxs-lookup"><span data-stu-id="f65d9-140">What kind of data do you want tooimport?</span></span>

* [<span data-ttu-id="f65d9-141">Arquivos JSON</span><span class="sxs-lookup"><span data-stu-id="f65d9-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="f65d9-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="f65d9-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="f65d9-143">Arquivos de exportação do MongoDB</span><span class="sxs-lookup"><span data-stu-id="f65d9-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="f65d9-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="f65d9-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="f65d9-145">Arquivos CSV</span><span class="sxs-lookup"><span data-stu-id="f65d9-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="f65d9-146">Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="f65d9-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="f65d9-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="f65d9-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="f65d9-148">Blob</span><span class="sxs-lookup"><span data-stu-id="f65d9-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="f65d9-149">Coleções do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f65d9-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="f65d9-150">HBase</span><span class="sxs-lookup"><span data-stu-id="f65d9-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="f65d9-151">Importação em massa do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f65d9-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="f65d9-152">Importação de registro sequencial do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f65d9-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="f65d9-153"><a id="JSON"></a>arquivos JSON tooimport</span><span class="sxs-lookup"><span data-stu-id="f65d9-153"><a id="JSON"></a>tooimport JSON files</span></span>
<span data-ttu-id="f65d9-154">opção de Importador de fonte de arquivo JSON de saudação permite que você tooimport um ou mais arquivos JSON único documento ou arquivos JSON que contêm uma matriz de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="f65d9-154">hello JSON file source importer option allows you tooimport one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="f65d9-155">Ao adicionar pastas que contêm tooimport de arquivos JSON, você tem a opção de saudação do recursivamente procurando arquivos em subpastas.</span><span class="sxs-lookup"><span data-stu-id="f65d9-155">When adding folders that contain JSON files tooimport, you have hello option of recursively searching for files in subfolders.</span></span>

![Captura de tela das opções de origem do arquivo JSON — ferramentas de migração de banco de dados](./media/import-data/jsonsource.png)

<span data-ttu-id="f65d9-157">Aqui estão alguns arquivos JSON de tooimport de exemplos de linha de comando:</span><span class="sxs-lookup"><span data-stu-id="f65d9-157">Here are some command line samples tooimport JSON files:</span></span>

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

## <span data-ttu-id="f65d9-158"><a id="MongoDB"></a>tooimport do MongoDB</span><span class="sxs-lookup"><span data-stu-id="f65d9-158"><a id="MongoDB"></a>tooimport from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f65d9-159">Se você estiver importando tooan Azure Cosmos DB conta com suporte para o MongoDB, siga estas [instruções](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="f65d9-159">If you are importing tooan Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="f65d9-160">Olá opção de Importador de origem do MongoDB permite tooimport de uma coleção do MongoDB individual e opcionalmente filtre documentos usando uma consulta e/ou modificar a estrutura do documento hello usando uma projeção.</span><span class="sxs-lookup"><span data-stu-id="f65d9-160">hello MongoDB source importer option allows you tooimport from an individual MongoDB collection and optionally filter documents using a query and/or modify hello document structure by using a projection.</span></span>  

![Captura de tela das opções de fonte do MongoDB](./media/import-data/mongodbsource.png)

<span data-ttu-id="f65d9-162">cadeia de caracteres de conexão Hello está no formato de MongoDB padrão da saudação:</span><span class="sxs-lookup"><span data-stu-id="f65d9-162">hello connection string is in hello standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="f65d9-163">Use Olá Verifique se o comando tooensure que Olá MongoDB instância especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.</span><span class="sxs-lookup"><span data-stu-id="f65d9-163">Use hello Verify command tooensure that hello MongoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="f65d9-164">Digite o nome de saudação de coleção de saudação do qual os dados serão importados.</span><span class="sxs-lookup"><span data-stu-id="f65d9-164">Enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="f65d9-165">Você pode opcionalmente especificar ou fornecer um arquivo para uma consulta (por exemplo, {pop: {$gt: 5000}}) e/ou projeção (por exemplo, {loc:0}) tooboth filtro e forma Olá dados toobe importado.</span><span class="sxs-lookup"><span data-stu-id="f65d9-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) tooboth filter and shape hello data toobe imported.</span></span>

<span data-ttu-id="f65d9-166">Aqui estão alguns tooimport de exemplos de linha de comando do MongoDB:</span><span class="sxs-lookup"><span data-stu-id="f65d9-166">Here are some command line samples tooimport from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="f65d9-167"><a id="MongoDBExport"></a>arquivos de exportação do MongoDB tooimport</span><span class="sxs-lookup"><span data-stu-id="f65d9-167"><a id="MongoDBExport"></a>tooimport MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f65d9-168">Se você estiver importando tooan Azure Cosmos DB conta com suporte para o MongoDB, siga estas [instruções](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="f65d9-168">If you are importing tooan Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="f65d9-169">Olá opção importador fonte de arquivo do MongoDB exportação JSON permite que você tooimport um ou mais arquivos JSON produzida do utilitário de mongoexport hello.</span><span class="sxs-lookup"><span data-stu-id="f65d9-169">hello MongoDB export JSON file source importer option allows you tooimport one or more JSON files produced from hello mongoexport utility.</span></span>  

![Captura de tela das opções de fonte de exportação do MongoDB](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="f65d9-171">Ao adicionar pastas que contêm arquivos de JSON do MongoDB exportação para importação, você tem a opção de saudação do procurando arquivos em subpastas de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="f65d9-171">When adding folders that contain MongoDB export JSON files for import, you have hello option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="f65d9-172">Aqui está um tooimport de exemplo de linha de comando de exportação do MongoDB arquivos JSON:</span><span class="sxs-lookup"><span data-stu-id="f65d9-172">Here is a command line sample tooimport from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="f65d9-173"><a id="SQL"></a>tooimport do SQL Server</span><span class="sxs-lookup"><span data-stu-id="f65d9-173"><a id="SQL"></a>tooimport from SQL Server</span></span>
<span data-ttu-id="f65d9-174">Olá opção de Importador de origem do SQL permite que você tooimport de um banco de dados individual do SQL Server e opcionalmente filtros Olá registros toobe importado usando uma consulta.</span><span class="sxs-lookup"><span data-stu-id="f65d9-174">hello SQL source importer option allows you tooimport from an individual SQL Server database and optionally filter hello records toobe imported using a query.</span></span> <span data-ttu-id="f65d9-175">Além disso, você pode modificar a estrutura do documento hello especificando um separador de aninhamento (mais detalhes em breve).</span><span class="sxs-lookup"><span data-stu-id="f65d9-175">In addition, you can modify hello document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Captura de tela das opções de origem do SQL — ferramentas de migração de banco de dados](./media/import-data/sqlexportsource.png)

<span data-ttu-id="f65d9-177">Olá formato de cadeia de caracteres de conexão de saudação é saudação padrão SQL conexão cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f65d9-177">hello format of hello connection string is hello standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="f65d9-178">Use Olá Verifique se o comando tooensure que Olá a instância do SQL Server especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.</span><span class="sxs-lookup"><span data-stu-id="f65d9-178">Use hello Verify command tooensure that hello SQL Server instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="f65d9-179">Olá aninhamento propriedade separator é usado toocreate as relações hierárquicas (subdocumentos) durante a importação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-179">hello nesting separator property is used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="f65d9-180">Considere Olá consulta SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="f65d9-180">Consider hello following SQL query:</span></span>

<span data-ttu-id="f65d9-181">*Selecione CAST (BusinessEntityID como varchar) como ID, Nome, AddressType como [Address.AddressType], AddressLine1 como [Address.AddressLine1], City como [Address.Location.City], StateProvinceName como [Address.Location.StateProvinceName], PostalCode como [Address.PostalCode], CountryRegionName como [Address.CountryRegionName] de Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span><span class="sxs-lookup"><span data-stu-id="f65d9-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="f65d9-182">Que retorna Olá resultados (parciais) a seguir:</span><span class="sxs-lookup"><span data-stu-id="f65d9-182">Which returns hello following (partial) results:</span></span>

![Captura de tela dos resultados de consulta do SQL](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="f65d9-184">Observe os aliases hello como Address.AddressType e Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="f65d9-184">Note hello aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="f65d9-185">Especificando um separador de aninhamento de '.', ferramenta de importação de saudação cria endereço e importar subdocumentos Address.Location durante a saudação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-185">By specifying a nesting separator of ‘.’, hello import tool creates Address and Address.Location subdocuments during hello import.</span></span> <span data-ttu-id="f65d9-186">Este é um exemplo de um documento resultante no Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="f65d9-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="f65d9-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span><span class="sxs-lookup"><span data-stu-id="f65d9-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="f65d9-188">Aqui estão alguns tooimport de exemplos de linha de comando do SQL Server:</span><span class="sxs-lookup"><span data-stu-id="f65d9-188">Here are some command line samples tooimport from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="f65d9-189"><a id="CSV"></a>os arquivos CSV tooimport e converter CSV tooJSON</span><span class="sxs-lookup"><span data-stu-id="f65d9-189"><a id="CSV"></a>tooimport CSV files and convert CSV tooJSON</span></span>
<span data-ttu-id="f65d9-190">Olá opção de Importador de fonte de arquivo CSV permite que você tooimport um ou mais arquivos CSV.</span><span class="sxs-lookup"><span data-stu-id="f65d9-190">hello CSV file source importer option enables you tooimport one or more CSV files.</span></span> <span data-ttu-id="f65d9-191">Ao adicionar pastas que contêm arquivos CSV para importar, você tem a opção de saudação do procurando arquivos em subpastas de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="f65d9-191">When adding folders that contain CSV files for import, you have hello option of recursively searching for files in subfolders.</span></span>

![Opções de fonte de captura de tela de CSV - tooJSON CSV](media/import-data/csvsource.png)

<span data-ttu-id="f65d9-193">Fonte SQL toohello semelhante, Olá aninhamento propriedade separator pode ser relações hierárquicas de toocreate usado (subdocumentos) durante a importação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-193">Similar toohello SQL source, hello nesting separator property may be used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="f65d9-194">Considere Olá a linha de cabeçalho CSV e linhas de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="f65d9-194">Consider hello following CSV header row and data rows:</span></span>

![Registros de exemplo de captura de tela de CSV - tooJSON CSV](./media/import-data/csvsample.png)

<span data-ttu-id="f65d9-196">Observe os aliases hello como DomainInfo.Domain_Name e RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="f65d9-196">Note hello aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="f65d9-197">Especificando um separador de aninhamento de '.', a ferramenta de importação de saudação criará DomainInfo e importar subdocumentos RedirectInfo durante a saudação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-197">By specifying a nesting separator of ‘.’, hello import tool will create DomainInfo and RedirectInfo subdocuments during hello import.</span></span> <span data-ttu-id="f65d9-198">Este é um exemplo de um documento resultante no Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="f65d9-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="f65d9-199">*{"DomainInfo": {"Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www. ACUS.GOV"},"Órgão Federal":"Administrativa conferência de saudação dos Estados Unidos","RedirectInfo": {"Redirecionar":"0","Redirect_Destination":" "},"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*</span><span class="sxs-lookup"><span data-stu-id="f65d9-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of hello United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="f65d9-200">ferramenta de importação de saudação tentará tooinfer informações de tipo de valores sem aspas em arquivos CSV (valores entre aspas sempre são tratados como cadeias de caracteres).</span><span class="sxs-lookup"><span data-stu-id="f65d9-200">hello import tool will attempt tooinfer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="f65d9-201">Tipos são identificados em ordem de saudação: número, datetime, booleano.</span><span class="sxs-lookup"><span data-stu-id="f65d9-201">Types are identified in hello following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="f65d9-202">Há dois outros toonote coisas sobre importação de CSV:</span><span class="sxs-lookup"><span data-stu-id="f65d9-202">There are two other things toonote about CSV import:</span></span>

1. <span data-ttu-id="f65d9-203">Por padrão, os valores sem aspas sempre são cortados para tabulações e espaços, enquanto os valores entre aspas são preservados como estão.</span><span class="sxs-lookup"><span data-stu-id="f65d9-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="f65d9-204">Esse comportamento pode ser substituído por hello que Trim entre aspas a opção de linha de comando de /s.TrimQuoted de caixa de seleção ou saudação de valores.</span><span class="sxs-lookup"><span data-stu-id="f65d9-204">This behavior can be overridden with hello Trim quoted values checkbox or hello /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="f65d9-205">Por padrão, um nulo sem aspas é tratado como um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="f65d9-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="f65d9-206">Esse comportamento pode ser substituído (isto é, trate um null sem aspas como uma cadeia de caracteres "null") com hello tratar sem aspas NULL como a opção de linha de comando de /s.NoUnquotedNulls de caixa de seleção ou saudação de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f65d9-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with hello Treat unquoted NULL as string checkbox or hello /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="f65d9-207">Aqui está um exemplo de linha de comando para importação de CSV:</span><span class="sxs-lookup"><span data-stu-id="f65d9-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="f65d9-208"><a id="AzureTableSource"></a>tooimport do armazenamento de tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="f65d9-208"><a id="AzureTableSource"></a>tooimport from Azure Table storage</span></span>
<span data-ttu-id="f65d9-209">Olá opção de Importador de origem de armazenamento de tabela do Azure permite que você tooimport de uma tabela de armazenamento de tabela do Azure individual e opcionalmente filtros Olá toobe de entidades de tabela importada.</span><span class="sxs-lookup"><span data-stu-id="f65d9-209">hello Azure Table storage source importer option allows you tooimport from an individual Azure Table storage table and optionally filter hello table entities toobe imported.</span></span> <span data-ttu-id="f65d9-210">Observe que você não pode usar dados de armazenamento de tabela do Azure ferramenta tooimport do hello migração de dados no banco de dados do Azure Cosmos para uso com hello API de tabela.</span><span class="sxs-lookup"><span data-stu-id="f65d9-210">Note that you cannot use hello Data Migration tool tooimport Azure Table storage data into Azure Cosmos DB for use with hello Table API.</span></span> <span data-ttu-id="f65d9-211">Importação só tooAzure Cosmos banco de dados para uso com hello API DocumentDB é suportada no momento.</span><span class="sxs-lookup"><span data-stu-id="f65d9-211">Only importing tooAzure Cosmos DB for use with hello DocumentDB API is supported at this time.</span></span>

![Captura de tela das opções de origem de armazenamento da tabela do Azure](./media/import-data/azuretablesource.png)

<span data-ttu-id="f65d9-213">formato Olá Olá cadeia de conexão de armazenamento de tabela do Azure é:</span><span class="sxs-lookup"><span data-stu-id="f65d9-213">hello format of hello Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="f65d9-214">Use Olá Verifique se o comando tooensure que Olá instância de armazenamento de tabela do Azure especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.</span><span class="sxs-lookup"><span data-stu-id="f65d9-214">Use hello Verify command tooensure that hello Azure Table storage instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="f65d9-215">Insira nome de saudação do hello Azure tabela da qual os dados serão importados.</span><span class="sxs-lookup"><span data-stu-id="f65d9-215">Enter hello name of hello Azure table from which data will be imported.</span></span> <span data-ttu-id="f65d9-216">Opcionalmente, você pode especificar um [filtro](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="f65d9-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="f65d9-217">Olá opção de Importador de origem de armazenamento de tabela do Azure tem Olá opções adicionais a seguir:</span><span class="sxs-lookup"><span data-stu-id="f65d9-217">hello Azure Table storage source importer option has hello following additional options:</span></span>

1. <span data-ttu-id="f65d9-218">Incluir campos internos</span><span class="sxs-lookup"><span data-stu-id="f65d9-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="f65d9-219">Todos - incluir todos os campos internos (PartitionKey, RowKey e Timestamp)</span><span class="sxs-lookup"><span data-stu-id="f65d9-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="f65d9-220">Nenhum - excluir todos os campos internos</span><span class="sxs-lookup"><span data-stu-id="f65d9-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="f65d9-221">RowKey - incluir apenas o campo de RowKey Olá</span><span class="sxs-lookup"><span data-stu-id="f65d9-221">RowKey - Only include hello RowKey field</span></span>
2. <span data-ttu-id="f65d9-222">Selecionar colunas</span><span class="sxs-lookup"><span data-stu-id="f65d9-222">Select Columns</span></span>
   1. <span data-ttu-id="f65d9-223">Filtros de armazenamento de tabela do Azure não dão suporte a projeções.</span><span class="sxs-lookup"><span data-stu-id="f65d9-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="f65d9-224">Se você quiser importar tooonly propriedades da entidade específicas tabela do Azure, adicione lista de colunas selecione toohello.</span><span class="sxs-lookup"><span data-stu-id="f65d9-224">If you want tooonly import specific Azure Table entity properties, add them toohello Select Columns list.</span></span> <span data-ttu-id="f65d9-225">Todas as outras propriedades da entidade serão ignoradas.</span><span class="sxs-lookup"><span data-stu-id="f65d9-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="f65d9-226">Aqui está um tooimport de exemplo de linha de comando do armazenamento de tabela do Azure:</span><span class="sxs-lookup"><span data-stu-id="f65d9-226">Here is a command line sample tooimport from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="f65d9-227"><a id="DynamoDBSource"></a>tooimport do Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="f65d9-227"><a id="DynamoDBSource"></a>tooimport from Amazon DynamoDB</span></span>
<span data-ttu-id="f65d9-228">Olá Amazon DynamoDB opção de Importador de origem permite tooimport de uma tabela individual do Amazon DynamoDB e opcionalmente filtre Olá entidades toobe importado.</span><span class="sxs-lookup"><span data-stu-id="f65d9-228">hello Amazon DynamoDB source importer option allows you tooimport from an individual Amazon DynamoDB table and optionally filter hello entities toobe imported.</span></span> <span data-ttu-id="f65d9-229">Vários modelos são fornecidos para que a configuração de uma importação seja tão fácil quanto possível.</span><span class="sxs-lookup"><span data-stu-id="f65d9-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Captura de tela das opções de origem do Amazon DynamoDB — ferramentas de migração de banco de dados](./media/import-data/dynamodbsource1.png)

![Captura de tela das opções de origem do Amazon DynamoDB — ferramentas de migração de banco de dados](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="f65d9-232">formato Olá Olá Amazon DynamoDB cadeia de caracteres de conexão é:</span><span class="sxs-lookup"><span data-stu-id="f65d9-232">hello format of hello Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="f65d9-233">Use Olá Verifique se o comando tooensure que Olá Amazon DynamoDB instância especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.</span><span class="sxs-lookup"><span data-stu-id="f65d9-233">Use hello Verify command tooensure that hello Amazon DynamoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="f65d9-234">Aqui está um tooimport de exemplo de linha de comando do Amazon DynamoDB:</span><span class="sxs-lookup"><span data-stu-id="f65d9-234">Here is a command line sample tooimport from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="f65d9-235"><a id="BlobImport"></a>arquivos de tooimport do armazenamento de BLOBs do Azure</span><span class="sxs-lookup"><span data-stu-id="f65d9-235"><a id="BlobImport"></a>tooimport files from Azure Blob storage</span></span>
<span data-ttu-id="f65d9-236">Olá arquivo JSON, arquivo de exportação do MongoDB e as opções de Importador de fonte de arquivo CSV permitem que você tooimport um ou mais arquivos de armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f65d9-236">hello JSON file, MongoDB export file, and CSV file source importer options allow you tooimport one or more files from Azure Blob storage.</span></span> <span data-ttu-id="f65d9-237">Depois de especificar uma URL de contêiner de Blob e a chave de conta, basta fornece um tooimport de arquivo (s) expressão regular tooselect hello.</span><span class="sxs-lookup"><span data-stu-id="f65d9-237">After specifying a Blob container URL and Account Key, simply provide a regular expression tooselect hello file(s) tooimport.</span></span>

![Captura de tela das opções de origem de arquivo de blob](./media/import-data/blobsource.png)

<span data-ttu-id="f65d9-239">Aqui está o arquivos de JSON de tooimport de exemplo de linha de comando do armazenamento de BLOBs do Azure:</span><span class="sxs-lookup"><span data-stu-id="f65d9-239">Here is command line sample tooimport JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="f65d9-240"><a id="DocumentDBSource"></a>tooimport de uma coleção de API do Azure Cosmos banco de dados DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f65d9-240"><a id="DocumentDBSource"></a>tooimport from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="f65d9-241">Olá opção do banco de dados do Azure Cosmos fonte importador permite tooimport dados de uma ou mais coleções de banco de dados do Azure Cosmos e opcionalmente filtre documentos usando uma consulta.</span><span class="sxs-lookup"><span data-stu-id="f65d9-241">hello Azure Cosmos DB source importer option allows you tooimport data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Captura de tela das opções de fonte do Azure Cosmos DB](./media/import-data/documentdbsource.png)

<span data-ttu-id="f65d9-243">formato Olá Olá cadeia de caracteres de conexão de banco de dados do Azure Cosmos é:</span><span class="sxs-lookup"><span data-stu-id="f65d9-243">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="f65d9-244">saudação de cadeia de caracteres de conexão do banco de dados do Azure Cosmos conta pode ser recuperada da folha de chaves de saudação do hello portal do Azure, conforme descrito em [como toomanage uma conta de banco de dados do Azure Cosmos](manage-account.md), no entanto, Olá o nome do banco de dados de saudação deve toohello toobe anexado cadeia de caracteres de conexão no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="f65d9-244">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="f65d9-245">Use Olá Verifique se o comando tooensure que Olá instância de banco de dados do Azure Cosmos especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.</span><span class="sxs-lookup"><span data-stu-id="f65d9-245">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="f65d9-246">tooimport de uma coleção de banco de dados do Azure Cosmos único, digite o nome de saudação de coleção de saudação do qual os dados serão importados.</span><span class="sxs-lookup"><span data-stu-id="f65d9-246">tooimport from a single Azure Cosmos DB collection, enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="f65d9-247">tooimport de várias coleções de banco de dados do Azure Cosmos, forneça uma expressão regular toomatch um ou mais nomes de coleção (por exemplo, collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="f65d9-247">tooimport from multiple Azure Cosmos DB collections, provide a regular expression toomatch one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="f65d9-248">Você pode opcionalmente especificar, ou fornecer um arquivo para um filtro de consulta tooboth e Olá toobe de dados importado de forma.</span><span class="sxs-lookup"><span data-stu-id="f65d9-248">You may optionally specify, or provide a file for, a query tooboth filter and shape hello data toobe imported.</span></span>

> [!NOTE]
> <span data-ttu-id="f65d9-249">Desde que o campo de coleção Olá aceita expressões regulares, se você estiver importando de uma única coleção cujo nome contém caracteres de expressão regular, em seguida, esses caracteres devem ser substituídas adequadamente.</span><span class="sxs-lookup"><span data-stu-id="f65d9-249">Since hello collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="f65d9-250">Olá opção do banco de dados do Azure Cosmos fonte importador tem seguintes Olá opções avançadas:</span><span class="sxs-lookup"><span data-stu-id="f65d9-250">hello Azure Cosmos DB source importer option has hello following advanced options:</span></span>

1. <span data-ttu-id="f65d9-251">Incluir campos internos: Especifica se ou não tooinclude Azure Cosmos DB documento propriedades do sistema Olá exportar (por exemplo, RID, TS).</span><span class="sxs-lookup"><span data-stu-id="f65d9-251">Include Internal Fields: Specifies whether or not tooinclude Azure Cosmos DB document system properties in hello export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="f65d9-252">Número de novas tentativas em caso de falha: especifica Olá número de vezes tooretry Olá conexão tooAzure Cosmos banco de dados no caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="f65d9-252">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="f65d9-253">Intervalo de repetição: Especifica quanto tempo toowait entre repetindo Olá conexão tooAzure Cosmos banco de dados no caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="f65d9-253">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="f65d9-254">Modo de Conexão: Especifica Olá toouse de modo de conexão com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f65d9-254">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="f65d9-255">opções disponíveis de saudação são DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="f65d9-255">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="f65d9-256">modos de conexão direta de saudação são mais rapidamente, enquanto o modo de gateway Olá é firewall mais amigável pois ele usa apenas a porta 443.</span><span class="sxs-lookup"><span data-stu-id="f65d9-256">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Captura de tela das opções avançadas de fonte do Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="f65d9-258">Olá importar do modo DirectTcp tooconnection ferramenta padrões.</span><span class="sxs-lookup"><span data-stu-id="f65d9-258">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="f65d9-259">Se você enfrentar problemas de firewall, alterne o modo de tooconnection Gateway, pois exige apenas a porta 443.</span><span class="sxs-lookup"><span data-stu-id="f65d9-259">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="f65d9-260">Aqui estão alguns tooimport de exemplos de linha de comando do banco de dados do Azure Cosmos:</span><span class="sxs-lookup"><span data-stu-id="f65d9-260">Here are some command line samples tooimport from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="f65d9-261">Olá, ferramenta de importação de dados do Azure Cosmos DB também oferece suporte à importação de dados de saudação [emulador de banco de dados do Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="f65d9-261">hello Azure Cosmos DB Data Import Tool also supports import of data from hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="f65d9-262">Ao importar dados de um emulador local, defina o ponto de extremidade de saudação muito`https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="f65d9-262">When importing data from a local emulator, set hello endpoint too`https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="f65d9-263"><a id="HBaseSource"></a>tooimport do HBase</span><span class="sxs-lookup"><span data-stu-id="f65d9-263"><a id="HBaseSource"></a>tooimport from HBase</span></span>
<span data-ttu-id="f65d9-264">Olá HBase opção de Importador de origem permite tooimport dados de uma tabela do HBase e opcionalmente filtre dados saudação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-264">hello HBase source importer option allows you tooimport data from an HBase table and optionally filter hello data.</span></span> <span data-ttu-id="f65d9-265">Vários modelos são fornecidos para que a configuração de uma importação seja tão fácil quanto possível.</span><span class="sxs-lookup"><span data-stu-id="f65d9-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Captura de tela das opções de origem do HBase](./media/import-data/hbasesource1.png)

![Captura de tela das opções de origem do HBase](./media/import-data/hbasesource2.png)

<span data-ttu-id="f65d9-268">formato Olá Olá HBase Stargate cadeia de caracteres de conexão é:</span><span class="sxs-lookup"><span data-stu-id="f65d9-268">hello format of hello HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="f65d9-269">Use Olá Verifique se o comando tooensure que Olá HBase instância especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.</span><span class="sxs-lookup"><span data-stu-id="f65d9-269">Use hello Verify command tooensure that hello HBase instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="f65d9-270">Aqui está um tooimport de exemplo de linha de comando do HBase:</span><span class="sxs-lookup"><span data-stu-id="f65d9-270">Here is a command line sample tooimport from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="f65d9-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello API DocumentDB (importação em massa)</span><span class="sxs-lookup"><span data-stu-id="f65d9-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="f65d9-272">Importador do Hello Azure Cosmos DB Bulk permite tooimport de qualquer uma das opções de origem disponível hello, usando um procedimento armazenado do Azure Cosmos DB para a eficiência.</span><span class="sxs-lookup"><span data-stu-id="f65d9-272">hello Azure Cosmos DB Bulk importer allows you tooimport from any of hello available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="f65d9-273">ferramenta de saudação oferece suporte a importação tooone particionada único banco de dados do Azure Cosmos coleção, bem como importação fragmentada no qual os dados são particionados em vários conjuntos de banco de dados do Azure Cosmos particionada único.</span><span class="sxs-lookup"><span data-stu-id="f65d9-273">hello tool supports import tooone single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="f65d9-274">Para obter mais informações sobre o particionamento de dados, consulte [Particionamento e escala no Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="f65d9-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="f65d9-275">ferramenta de saudação criar, executar e, em seguida, excluir procedimento armazenado de saudação do hello collection(s) de destino.</span><span class="sxs-lookup"><span data-stu-id="f65d9-275">hello tool will create, execute, and then delete hello stored procedure from hello target collection(s).</span></span>  

![Captura de tela das opções em massa do Azure Cosmos DB](./media/import-data/documentdbbulk.png)

<span data-ttu-id="f65d9-277">formato Olá Olá cadeia de caracteres de conexão de banco de dados do Azure Cosmos é:</span><span class="sxs-lookup"><span data-stu-id="f65d9-277">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="f65d9-278">saudação de cadeia de caracteres de conexão do banco de dados do Azure Cosmos conta pode ser recuperada da folha de chaves de saudação do hello portal do Azure, conforme descrito em [como toomanage uma conta de banco de dados do Azure Cosmos](manage-account.md), no entanto, Olá o nome do banco de dados de saudação deve toohello toobe anexado cadeia de caracteres de conexão no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="f65d9-278">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="f65d9-279">Use Olá Verifique se o comando tooensure que Olá instância de banco de dados do Azure Cosmos especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.</span><span class="sxs-lookup"><span data-stu-id="f65d9-279">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="f65d9-280">tooimport tooa única coleção, digite nome Olá Olá coleção toowhich dados serão importados e clique no botão Adicionar de saudação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-280">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="f65d9-281">tooimport toomultiple coleções, insira cada nome de coleção individualmente ou usar várias coleções de Olá toospecify de sintaxe a seguir: *collection_prefix*[index - índice do fim de iniciar].</span><span class="sxs-lookup"><span data-stu-id="f65d9-281">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="f65d9-282">Ao especificar várias coleções por meio da sintaxe de saudação mencionados acima, tenha em mente Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="f65d9-282">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="f65d9-283">Somente padrões de nome de intervalo inteiro têm suporte.</span><span class="sxs-lookup"><span data-stu-id="f65d9-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="f65d9-284">Por exemplo, a especificação de coleção [0-3] produzirá Olá coleções a seguir: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="f65d9-284">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="f65d9-285">Você pode usar uma sintaxe abreviada: collection[3] emitirá o mesmo conjunto de coleções mencionado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="f65d9-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="f65d9-286">Mais de uma substituição pode ser fornecida.</span><span class="sxs-lookup"><span data-stu-id="f65d9-286">More than one substitution can be provided.</span></span> <span data-ttu-id="f65d9-287">Por exemplo, a coleção [0-1] [0-9] gerará 20 nomes de coleção com zeros à esquerda (collection01... 02,... 03).</span><span class="sxs-lookup"><span data-stu-id="f65d9-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="f65d9-288">Depois de hello nomes de coleção forem especificados, escolha desejado taxa de transferência de saudação do hello collection(s) (400 RUs too10, 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="f65d9-288">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too10,000 RUs).</span></span> <span data-ttu-id="f65d9-289">Para uma importação com melhor desempenho, escolha uma taxa de transferência maior.</span><span class="sxs-lookup"><span data-stu-id="f65d9-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="f65d9-290">Para obter mais informações sobre níveis de desempenho, consulte [Níveis de desempenho no Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="f65d9-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f65d9-291">configuração de taxa de transferência de desempenho de saudação só se aplica a criação de toocollection.</span><span class="sxs-lookup"><span data-stu-id="f65d9-291">hello performance throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="f65d9-292">Se Olá especificado coleção já existe, sua taxa de transferência não será modificada.</span><span class="sxs-lookup"><span data-stu-id="f65d9-292">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="f65d9-293">Ao importar coleções toomultiple, ferramenta de importação de saudação dá suporte a fragmentação de hash com base.</span><span class="sxs-lookup"><span data-stu-id="f65d9-293">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="f65d9-294">Neste cenário, especifique a propriedade de documento de saudação desejar toouse como Olá chave de partição (se a chave de partição é deixada em branco, documentos serão fragmentados aleatoriamente em conjuntos de destino Olá).</span><span class="sxs-lookup"><span data-stu-id="f65d9-294">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="f65d9-295">Opcionalmente, você pode especificar qual campo na fonte de importação Olá deve ser usado como Olá propriedade de id do banco de dados do Azure Cosmos documento durante a importação da saudação (Observe que se documentos não contenham essa propriedade, em seguida, ferramenta de importação de saudação irá gerar um GUID como o valor da propriedade id Olá).</span><span class="sxs-lookup"><span data-stu-id="f65d9-295">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="f65d9-296">Há uma série de opções avançadas disponíveis durante a importação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="f65d9-297">Primeiro, enquanto a ferramenta de saudação inclui uma massa padrão importar (BulkInsert.js) de procedimento armazenado, você pode escolher toospecify seu próprio procedimento armazenado de importação:</span><span class="sxs-lookup"><span data-stu-id="f65d9-297">First, while hello tool includes a default bulk import stored procedure (BulkInsert.js), you may choose toospecify your own import stored procedure:</span></span>

 ![Captura de tela da opção de sproc de inserção em massa do Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="f65d9-299">Adicionalmente, ao importar tipos de dados (por exemplo, do SQL Server ou do MongoDB), você pode escolher entre três opções de importação:</span><span class="sxs-lookup"><span data-stu-id="f65d9-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Captura de tela das opções de importação de data e hora do Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="f65d9-301">Cadeia de caracteres: Persistir como um valor de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f65d9-301">String: Persist as a string value</span></span>
* <span data-ttu-id="f65d9-302">Época: Persistir como um valor de número de época</span><span class="sxs-lookup"><span data-stu-id="f65d9-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="f65d9-303">Ambos: Persistir com os valores de número de cadeia de caracteres e de época.</span><span class="sxs-lookup"><span data-stu-id="f65d9-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="f65d9-304">Essa opção criará um sub-documento, por exemplo: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245}</span><span class="sxs-lookup"><span data-stu-id="f65d9-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="f65d9-305">Importador do Hello em massa de banco de dados do Azure Cosmos tem opções avançadas adicionais do hello seguintes:</span><span class="sxs-lookup"><span data-stu-id="f65d9-305">hello Azure Cosmos DB Bulk importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="f65d9-306">Tamanho do lote: Olá ferramenta padrões tooa tamanho de lote de 50.</span><span class="sxs-lookup"><span data-stu-id="f65d9-306">Batch Size: hello tool defaults tooa batch size of 50.</span></span>  <span data-ttu-id="f65d9-307">Se Olá documentos toobe importado grande, considere reduzir o tamanho do lote hello.</span><span class="sxs-lookup"><span data-stu-id="f65d9-307">If hello documents toobe imported are large, consider lowering hello batch size.</span></span> <span data-ttu-id="f65d9-308">Por outro lado, se Olá documentos toobe importado sejam pequeno, considere aumentar o tamanho do lote hello.</span><span class="sxs-lookup"><span data-stu-id="f65d9-308">Conversely, if hello documents toobe imported are small, consider raising hello batch size.</span></span>
2. <span data-ttu-id="f65d9-309">Tamanho máximo de Script (bytes): ferramenta de saudação padrões tooa tamanho de máximo de script de 512KB</span><span class="sxs-lookup"><span data-stu-id="f65d9-309">Max Script Size (bytes): hello tool defaults tooa max script size of 512KB</span></span>
3. <span data-ttu-id="f65d9-310">Desabilitar a geração automática do Id: Se cada toobe documento importado contém um campo de id, em seguida, selecionar esta opção pode aumentar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="f65d9-310">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="f65d9-311">Documentos com um campo de ID exclusiva ausente não serão importados.</span><span class="sxs-lookup"><span data-stu-id="f65d9-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="f65d9-312">Os documentos atualização existente: Olá ferramenta padrões toonot substituindo os documentos existentes com conflitos de id.</span><span class="sxs-lookup"><span data-stu-id="f65d9-312">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="f65d9-313">Esta opção permitirá a substituir documentos existentes por ids correspondentes.</span><span class="sxs-lookup"><span data-stu-id="f65d9-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="f65d9-314">Esse recurso é útil para migrações de dados agendadas que atualizam documentos existentes.</span><span class="sxs-lookup"><span data-stu-id="f65d9-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="f65d9-315">Número de novas tentativas em caso de falha: especifica Olá número de vezes tooretry Olá conexão tooAzure Cosmos banco de dados no caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="f65d9-315">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="f65d9-316">Intervalo de repetição: Especifica quanto tempo toowait entre repetindo Olá conexão tooAzure Cosmos banco de dados no caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="f65d9-316">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="f65d9-317">Modo de Conexão: Especifica Olá toouse de modo de conexão com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f65d9-317">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="f65d9-318">opções disponíveis de saudação são DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="f65d9-318">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="f65d9-319">modos de conexão direta de saudação são mais rapidamente, enquanto o modo de gateway Olá é firewall mais amigável pois ele usa apenas a porta 443.</span><span class="sxs-lookup"><span data-stu-id="f65d9-319">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Captura de tela das opções avançadas de importação em massa do Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="f65d9-321">Olá importar do modo DirectTcp tooconnection ferramenta padrões.</span><span class="sxs-lookup"><span data-stu-id="f65d9-321">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="f65d9-322">Se você enfrentar problemas de firewall, alterne o modo de tooconnection Gateway, pois exige apenas a porta 443.</span><span class="sxs-lookup"><span data-stu-id="f65d9-322">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="f65d9-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello API DocumentDB (sequencial importação de registro)</span><span class="sxs-lookup"><span data-stu-id="f65d9-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="f65d9-324">Importador do Hello Azure Cosmos DB sequencial registro permite que você tooimport de qualquer uma das opções de origem disponível Olá em uma base de registro por registro.</span><span class="sxs-lookup"><span data-stu-id="f65d9-324">hello Azure Cosmos DB sequential record importer allows you tooimport from any of hello available source options on a record by record basis.</span></span> <span data-ttu-id="f65d9-325">Você pode escolher essa opção se você estiver importando tooan coleção existente que já atingiu a cota de procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="f65d9-325">You might choose this option if you’re importing tooan existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="f65d9-326">Olá ferramenta oferece suporte à importação tooa única coleção de banco de dados do Azure Cosmos (partição única e várias partições), bem como importação fragmentada no qual os dados são particionados em vários conjuntos de banco de dados do Azure Cosmos de partição única e/ou em várias partições.</span><span class="sxs-lookup"><span data-stu-id="f65d9-326">hello tool supports import tooa single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="f65d9-327">Para obter mais informações sobre o particionamento de dados, consulte [Particionamento e escala no Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="f65d9-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Captura de tela das opções de importação de registro sequencial do Azure Cosmos DB](./media/import-data/documentdbsequential.png)

<span data-ttu-id="f65d9-329">formato Olá Olá cadeia de caracteres de conexão de banco de dados do Azure Cosmos é:</span><span class="sxs-lookup"><span data-stu-id="f65d9-329">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="f65d9-330">saudação de cadeia de caracteres de conexão do banco de dados do Azure Cosmos conta pode ser recuperada da folha de chaves de saudação do hello portal do Azure, conforme descrito em [como toomanage uma conta de banco de dados do Azure Cosmos](manage-account.md), no entanto, Olá o nome do banco de dados de saudação deve toohello toobe anexado cadeia de caracteres de conexão no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="f65d9-330">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="f65d9-331">Use Olá Verifique se o comando tooensure que Olá instância de banco de dados do Azure Cosmos especificada no campo de cadeia de caracteres de conexão Olá pode ser acessado.</span><span class="sxs-lookup"><span data-stu-id="f65d9-331">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="f65d9-332">tooimport tooa única coleção, digite nome Olá Olá coleção toowhich dados serão importados e clique no botão Adicionar de saudação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-332">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="f65d9-333">tooimport toomultiple coleções, insira cada nome de coleção individualmente ou usar várias coleções de Olá toospecify de sintaxe a seguir: *collection_prefix*[index - índice do fim de iniciar].</span><span class="sxs-lookup"><span data-stu-id="f65d9-333">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="f65d9-334">Ao especificar várias coleções por meio da sintaxe de saudação mencionados acima, tenha em mente Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="f65d9-334">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="f65d9-335">Somente padrões de nome de intervalo inteiro têm suporte.</span><span class="sxs-lookup"><span data-stu-id="f65d9-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="f65d9-336">Por exemplo, a especificação de coleção [0-3] produzirá Olá coleções a seguir: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="f65d9-336">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="f65d9-337">Você pode usar uma sintaxe abreviada: collection[3] emitirá o mesmo conjunto de coleções mencionado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="f65d9-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="f65d9-338">Mais de uma substituição pode ser fornecida.</span><span class="sxs-lookup"><span data-stu-id="f65d9-338">More than one substitution can be provided.</span></span> <span data-ttu-id="f65d9-339">Por exemplo, a coleção [0-1] [0-9] gerará 20 nomes de coleção com zeros à esquerda (collection01... 02,... 03).</span><span class="sxs-lookup"><span data-stu-id="f65d9-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="f65d9-340">Depois de hello nomes de coleção forem especificados, escolha desejado taxa de transferência de saudação do hello collection(s) (400 RUs too250, 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="f65d9-340">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too250,000 RUs).</span></span> <span data-ttu-id="f65d9-341">Para uma importação com melhor desempenho, escolha uma taxa de transferência maior.</span><span class="sxs-lookup"><span data-stu-id="f65d9-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="f65d9-342">Para obter mais informações sobre níveis de desempenho, consulte [Níveis de desempenho no Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="f65d9-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="f65d9-343">Qualquer importar toocollections com taxa de transferência > 10.000 RUs exigirá uma chave de partição.</span><span class="sxs-lookup"><span data-stu-id="f65d9-343">Any import toocollections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="f65d9-344">Se você escolher toohave mais de 250.000 RUs, você precisará toofile uma solicitação em toohave portal Olá aumentado de sua conta.</span><span class="sxs-lookup"><span data-stu-id="f65d9-344">If you choose toohave more than 250,000 RUs, you will need toofile a request in hello portal toohave your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="f65d9-345">configuração de taxa de transferência de saudação só se aplica a criação de toocollection.</span><span class="sxs-lookup"><span data-stu-id="f65d9-345">hello throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="f65d9-346">Se Olá especificado coleção já existe, sua taxa de transferência não será modificada.</span><span class="sxs-lookup"><span data-stu-id="f65d9-346">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="f65d9-347">Ao importar coleções toomultiple, ferramenta de importação de saudação dá suporte a fragmentação de hash com base.</span><span class="sxs-lookup"><span data-stu-id="f65d9-347">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="f65d9-348">Neste cenário, especifique a propriedade de documento de saudação desejar toouse como Olá chave de partição (se a chave de partição é deixada em branco, documentos serão fragmentados aleatoriamente em conjuntos de destino Olá).</span><span class="sxs-lookup"><span data-stu-id="f65d9-348">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="f65d9-349">Opcionalmente, você pode especificar qual campo na fonte de importação Olá deve ser usado como Olá propriedade de id do banco de dados do Azure Cosmos documento durante a importação da saudação (Observe que se documentos não contenham essa propriedade, em seguida, ferramenta de importação de saudação irá gerar um GUID como o valor da propriedade id Olá).</span><span class="sxs-lookup"><span data-stu-id="f65d9-349">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="f65d9-350">Há uma série de opções avançadas disponíveis durante a importação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="f65d9-351">Primeiro, ao importar tipos de dados (por exemplo, do SQL Server ou do MongoDB), você pode escolher entre três opções de importação:</span><span class="sxs-lookup"><span data-stu-id="f65d9-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Captura de tela das opções de importação de data e hora do Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="f65d9-353">Cadeia de caracteres: Persistir como um valor de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f65d9-353">String: Persist as a string value</span></span>
* <span data-ttu-id="f65d9-354">Época: Persistir como um valor de número de época</span><span class="sxs-lookup"><span data-stu-id="f65d9-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="f65d9-355">Ambos: Persistir com os valores de número de cadeia de caracteres e de época.</span><span class="sxs-lookup"><span data-stu-id="f65d9-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="f65d9-356">Essa opção criará um sub-documento, por exemplo: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245}</span><span class="sxs-lookup"><span data-stu-id="f65d9-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="f65d9-357">Hello Azure Cosmos DB - importador de registro sequencial tem opções avançadas adicionais do hello seguintes:</span><span class="sxs-lookup"><span data-stu-id="f65d9-357">hello Azure Cosmos DB - Sequential record importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="f65d9-358">Número de solicitações em paralelo: ferramenta de saudação padrões solicitações paralelas too2.</span><span class="sxs-lookup"><span data-stu-id="f65d9-358">Number of Parallel Requests: hello tool defaults too2 parallel requests.</span></span> <span data-ttu-id="f65d9-359">Se Olá documentos toobe importado sejam pequeno, considere aumentar o número de saudação de solicitações em paralelo.</span><span class="sxs-lookup"><span data-stu-id="f65d9-359">If hello documents toobe imported are small, consider raising hello number of parallel requests.</span></span> <span data-ttu-id="f65d9-360">Observe que, se esse número é gerado muito, Olá importação pode resultar de limitação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-360">Note that if this number is raised too much, hello import may experience throttling.</span></span>
2. <span data-ttu-id="f65d9-361">Desabilitar a geração automática do Id: Se cada toobe documento importado contém um campo de id, em seguida, selecionar esta opção pode aumentar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="f65d9-361">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="f65d9-362">Documentos com um campo de ID exclusiva ausente não serão importados.</span><span class="sxs-lookup"><span data-stu-id="f65d9-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="f65d9-363">Os documentos atualização existente: Olá ferramenta padrões toonot substituindo os documentos existentes com conflitos de id.</span><span class="sxs-lookup"><span data-stu-id="f65d9-363">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="f65d9-364">Esta opção permitirá a substituir documentos existentes por ids correspondentes.</span><span class="sxs-lookup"><span data-stu-id="f65d9-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="f65d9-365">Esse recurso é útil para migrações de dados agendadas que atualizam documentos existentes.</span><span class="sxs-lookup"><span data-stu-id="f65d9-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="f65d9-366">Número de novas tentativas em caso de falha: especifica Olá número de vezes tooretry Olá conexão tooAzure Cosmos banco de dados no caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="f65d9-366">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="f65d9-367">Intervalo de repetição: Especifica quanto tempo toowait entre repetindo Olá conexão tooAzure Cosmos banco de dados no caso de falhas transitórias (por exemplo, interrupção da conectividade de rede).</span><span class="sxs-lookup"><span data-stu-id="f65d9-367">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="f65d9-368">Modo de Conexão: Especifica Olá toouse de modo de conexão com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f65d9-368">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="f65d9-369">opções disponíveis de saudação são DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="f65d9-369">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="f65d9-370">modos de conexão direta de saudação são mais rapidamente, enquanto o modo de gateway Olá é firewall mais amigável pois ele usa apenas a porta 443.</span><span class="sxs-lookup"><span data-stu-id="f65d9-370">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Captura de tela das opções avançadas de importação de registro sequencial do Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="f65d9-372">Olá importar do modo DirectTcp tooconnection ferramenta padrões.</span><span class="sxs-lookup"><span data-stu-id="f65d9-372">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="f65d9-373">Se você enfrentar problemas de firewall, alterne o modo de tooconnection Gateway, pois exige apenas a porta 443.</span><span class="sxs-lookup"><span data-stu-id="f65d9-373">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="f65d9-374"><a id="IndexingPolicy"></a>Especificar uma política de indexação ao criar coleções do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f65d9-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="f65d9-375">Quando você permite a migração de saudação coleções de toocreate ferramenta durante a importação, você pode especificar a política de indexação de saudação de coleções de saudação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-375">When you allow hello migration tool toocreate collections during import, you can specify hello indexing policy of hello collections.</span></span> <span data-ttu-id="f65d9-376">No hello avançado seção Opções de importação em massa de banco de dados do Azure Cosmos de hello e sequenciais do banco de dados do Azure Cosmos opções de registro, navegue toohello seção de política de indexação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-376">In hello advanced options section of hello Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate toohello Indexing Policy section.</span></span>

![Captura de tela das opções avançadas de Política de indexação do Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="f65d9-378">Usando Olá opção de política de indexação avançada, você pode selecionar um arquivo de política de indexação, insira manualmente uma política de indexação ou selecionar de um conjunto de modelos padrão (clique direito na indexação de política de caixa de texto de saudação).</span><span class="sxs-lookup"><span data-stu-id="f65d9-378">Using hello Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in hello indexing policy textbox).</span></span>

<span data-ttu-id="f65d9-379">modelos de política de Olá Olá ferramenta fornece são:</span><span class="sxs-lookup"><span data-stu-id="f65d9-379">hello policy templates hello tool provides are:</span></span>

* <span data-ttu-id="f65d9-380">Padrão.</span><span class="sxs-lookup"><span data-stu-id="f65d9-380">Default.</span></span> <span data-ttu-id="f65d9-381">Essa política é mais útil quando você está executando consultas de igualdade em cadeias de caracteres e usando as consultas ORDER BY, intervalo e igualdade para números.</span><span class="sxs-lookup"><span data-stu-id="f65d9-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="f65d9-382">Essa política tem uma sobrecarga de armazenamento de índice menor que Intervalo.</span><span class="sxs-lookup"><span data-stu-id="f65d9-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="f65d9-383">Intervalo.</span><span class="sxs-lookup"><span data-stu-id="f65d9-383">Range.</span></span> <span data-ttu-id="f65d9-384">Essa política é mais útil quando você está usando consultas ORDER BY, intervalo e igualdade em números e cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f65d9-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="f65d9-385">Essa política tem uma sobrecarga de armazenamento de índice maior do que Padrão ou Hash.</span><span class="sxs-lookup"><span data-stu-id="f65d9-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Captura de tela das opções avançadas de Política de indexação do Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="f65d9-387">Se você não especificar uma política de indexação, a política padrão de saudação será aplicada.</span><span class="sxs-lookup"><span data-stu-id="f65d9-387">If you do not specify an indexing policy, then hello default policy will be applied.</span></span> <span data-ttu-id="f65d9-388">Para obter mais informações sobre políticas de indexação, consulte [Políticas de indexação do Azure Cosmos DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f65d9-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-toojson-file"></a><span data-ttu-id="f65d9-389">Exportar arquivo tooJSON</span><span class="sxs-lookup"><span data-stu-id="f65d9-389">Export tooJSON file</span></span>
<span data-ttu-id="f65d9-390">exportação de JSON de banco de dados do Azure Cosmos Olá permite tooexport qualquer Olá disponíveis opções tooa JSON do arquivo de origem que contém uma matriz de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="f65d9-390">hello Azure Cosmos DB JSON exporter allows you tooexport any of hello available source options tooa JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="f65d9-391">ferramenta Olá tratará exportação Olá para você, ou você pode escolher o comando de migração tooview Olá resultante e execute o comando de saudação por conta própria.</span><span class="sxs-lookup"><span data-stu-id="f65d9-391">hello tool will handle hello export for you, or you can choose tooview hello resulting migration command and run hello command yourself.</span></span> <span data-ttu-id="f65d9-392">arquivo JSON resultante de saudação pode ser armazenado localmente ou no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f65d9-392">hello resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Captura de tela da opção de exportação de arquivo local JSON do Azure Cosmos DB](./media/import-data/jsontarget.png)

![Captura de tela da opção de exportação de JSON do Armazenamento de blobs do Azure no Azure Cosmos DB](./media/import-data/jsontarget2.png)

<span data-ttu-id="f65d9-395">Opcionalmente, você pode escolher Olá tooprettify resultante JSON, que aumentará o tamanho de saudação do documento resultante Olá enquanto tornar Olá conteúdo mais legível.</span><span class="sxs-lookup"><span data-stu-id="f65d9-395">You may optionally choose tooprettify hello resulting JSON, which will increase hello size of hello resulting document while making hello contents more human readable.</span></span>

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

## <a name="advanced-configuration"></a><span data-ttu-id="f65d9-396">Configuração avançada</span><span class="sxs-lookup"><span data-stu-id="f65d9-396">Advanced configuration</span></span>
<span data-ttu-id="f65d9-397">Na tela de configuração avançada de hello, especifique o local de saudação do hello toowhich de arquivo de log você deseja que os erros gravados.</span><span class="sxs-lookup"><span data-stu-id="f65d9-397">In hello Advanced configuration screen, specify hello location of hello log file toowhich you would like any errors written.</span></span> <span data-ttu-id="f65d9-398">Olá regras a seguir se aplicam a página toothis:</span><span class="sxs-lookup"><span data-stu-id="f65d9-398">hello following rules apply toothis page:</span></span>

1. <span data-ttu-id="f65d9-399">Se um nome de arquivo não for fornecido, serão retornados todos os erros na página de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f65d9-399">If a file name is not provided, then all errors will be returned on hello Results page.</span></span>
2. <span data-ttu-id="f65d9-400">Se for fornecido um nome de arquivo sem um diretório, em seguida, arquivo hello será criado (ou substituído) no diretório atual do ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="f65d9-400">If a file name is provided without a directory, then hello file will be created (or overwritten) in hello current environment directory.</span></span>
3. <span data-ttu-id="f65d9-401">Se você selecionar um existente será substituído arquivo e, em seguida, arquivo hello, não há nenhuma opção de anexar.</span><span class="sxs-lookup"><span data-stu-id="f65d9-401">If you select an existing file, then hello file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="f65d9-402">Em seguida, escolha se toolog todas as críticas, ou se nenhuma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="f65d9-402">Then, choose whether toolog all, critical, or no error messages.</span></span> <span data-ttu-id="f65d9-403">Finalmente, decida frequência Olá na mensagem de transferência da tela será atualizado com seu progresso.</span><span class="sxs-lookup"><span data-stu-id="f65d9-403">Finally, decide how frequently hello on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="f65d9-404">Confirme as configurações de importação e de linha de comando de exibição</span><span class="sxs-lookup"><span data-stu-id="f65d9-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="f65d9-405">Depois de especificar as informações de origem, informações de destino e configuração avançada, examine o resumo de migração hello e, opcionalmente, Olá resultantes do comando de migração (o comando de cópia Olá é útil tooautomate operações de importação) de exibição/copiar:</span><span class="sxs-lookup"><span data-stu-id="f65d9-405">After specifying source information, target information, and advanced configuration, review hello migration summary and, optionally, view/copy hello resulting migration command (copying hello command is useful tooautomate import operations):</span></span>
   
    ![Captura de tela da tela de resumo](./media/import-data/summary.png)
   
    ![Captura de tela da tela de resumo](./media/import-data/summarycommand.png)
2. <span data-ttu-id="f65d9-408">Quando estiver satisfeito com suas opções de origem e de destino, clique em **Importar**.</span><span class="sxs-lookup"><span data-stu-id="f65d9-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="f65d9-409">tempo decorrido de saudação, contagem transferida e informações de falha (se você não fornecer um nome de arquivo de configuração avançada de saudação) serão atualizadas à medida que importar hello está em processo.</span><span class="sxs-lookup"><span data-stu-id="f65d9-409">hello elapsed time, transferred count, and failure information (if you didn't provide a file name in hello Advanced configuration) will update as hello import is in process.</span></span> <span data-ttu-id="f65d9-410">Uma vez concluído, você pode exportar resultados da saudação (por exemplo, toodeal com quaisquer falhas de importação).</span><span class="sxs-lookup"><span data-stu-id="f65d9-410">Once complete, you can export hello results (e.g. toodeal with any import failures).</span></span>
   
    ![Captura de tela da opção de exportação de JSON do Azure Cosmos DB](./media/import-data/viewresults.png)
3. <span data-ttu-id="f65d9-412">Você também pode iniciar uma nova importação, ao manter as configurações existentes do hello (por exemplo, escolha de informações, origem e destino de cadeia de caracteres de conexão, etc.) ou redefinir todos os valores.</span><span class="sxs-lookup"><span data-stu-id="f65d9-412">You may also start a new import, either keeping hello existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Captura de tela da opção de exportação de JSON do Azure Cosmos DB](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="f65d9-414">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f65d9-414">Next steps</span></span>

<span data-ttu-id="f65d9-415">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="f65d9-415">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f65d9-416">Ferramenta de migração de dados Olá instalada</span><span class="sxs-lookup"><span data-stu-id="f65d9-416">Installed hello Data Migration tool</span></span>
> * <span data-ttu-id="f65d9-417">Importou dados de diferentes fontes de dados</span><span class="sxs-lookup"><span data-stu-id="f65d9-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="f65d9-418">Exportados do banco de dados do Azure Cosmos tooJSON</span><span class="sxs-lookup"><span data-stu-id="f65d9-418">Exported from Azure Cosmos DB tooJSON</span></span>

<span data-ttu-id="f65d9-419">Agora você pode continuar tutorial próxima toohello e aprender como tooquery dados usando o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f65d9-419">You can now proceed toohello next tutorial and learn how tooquery data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="f65d9-420">Como os dados tooquery?</span><span class="sxs-lookup"><span data-stu-id="f65d9-420">How tooquery data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
