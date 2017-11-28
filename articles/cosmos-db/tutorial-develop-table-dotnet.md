---
title: 'Azure Cosmos DB: Desenvolver com a API de Tabela no .NET | Microsoft Docs'
description: Aprenda a desenvolver com a API de Tabela do Azure Cosmos DB usando o .NET
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
ms.openlocfilehash: 52cb5f2569b6c3a5301752b1e8bfb6cea13ff7f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-develop-with-the-table-api-in-net"></a><span data-ttu-id="44b89-103">Azure Cosmos DB: Desenvolver com a API de Tabela no .NET</span><span class="sxs-lookup"><span data-stu-id="44b89-103">Azure Cosmos DB: Develop with the Table API in .NET</span></span>

<span data-ttu-id="44b89-104">O Azure Cosmos DB é o serviço de banco de dados multimodelo distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="44b89-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="44b89-105">É possível criar e consultar rapidamente documentos, chave/valor e bancos de dados do gráfico. Todos se beneficiam de recursos de escala horizontal e distribuição global no núcleo do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44b89-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="44b89-106">Este tutorial cobre as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="44b89-106">This tutorial covers the following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="44b89-107">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="44b89-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="44b89-108">Habilitar a funcionalidade no arquivo app. config</span><span class="sxs-lookup"><span data-stu-id="44b89-108">Enable functionality in the app.config file</span></span> 
> * <span data-ttu-id="44b89-109">Criar uma tabela usando o [API de Tabela](table-introduction.md) (visualização)</span><span class="sxs-lookup"><span data-stu-id="44b89-109">Create a table using the [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="44b89-110">Adicionar uma entidade a uma tabela</span><span class="sxs-lookup"><span data-stu-id="44b89-110">Add an entity to a table</span></span> 
> * <span data-ttu-id="44b89-111">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="44b89-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="44b89-112">Recuperar uma única entidade</span><span class="sxs-lookup"><span data-stu-id="44b89-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="44b89-113">Consultar entidades usando índices secundários automáticos</span><span class="sxs-lookup"><span data-stu-id="44b89-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="44b89-114">Substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="44b89-114">Replace an entity</span></span> 
> * <span data-ttu-id="44b89-115">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="44b89-115">Delete an entity</span></span> 
> * <span data-ttu-id="44b89-116">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="44b89-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="44b89-117">Tabelas no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="44b89-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="44b89-118">O Azure Cosmos DB fornece a [API de Tabela](table-introduction.md) (visualização) para aplicativos que precisam de um repositório de chave-valor com um design menos esquemático.</span><span class="sxs-lookup"><span data-stu-id="44b89-118">Azure Cosmos DB provides the [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="44b89-119">Os SDKs e as APIs REST do [Armazenamento de Tabelas do Azure](../storage/common/storage-introduction.md) podem ser usados para trabalhar com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44b89-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used to work with Azure Cosmos DB.</span></span> <span data-ttu-id="44b89-120">Você pode usar o Azure Cosmos DB para criar tabelas com requisitos de alta taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="44b89-120">You can use Azure Cosmos DB to create tables with high throughput requirements.</span></span> <span data-ttu-id="44b89-121">O Azure Cosmos DB dá suporte a tabelas com otimização de taxa de transferência (chamadas informalmente de "tabelas premium"), atualmente em visualização pública.</span><span class="sxs-lookup"><span data-stu-id="44b89-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="44b89-122">Você pode continuar usando o Armazenamento de Tabelas do Azure para tabelas com alto requisitos de armazenamento e menores taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="44b89-122">You can continue to use Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="44b89-123">O Azure Cosmos DB apresentará o suporte para tabelas com otimização de armazenamento em uma atualização futura, e contas de armazenamento de tabelas do Azure novas e existentes serão atualizadas automaticamente para o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44b89-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded to Azure Cosmos DB.</span></span>

<span data-ttu-id="44b89-124">Caso utilize o Armazenamento de Tabelas do Azure neste momento, você recebe os seguintes benefícios com a visualização de "tabela premium":</span><span class="sxs-lookup"><span data-stu-id="44b89-124">If you currently use Azure Table storage, you gain the following benefits with the "premium table" preview:</span></span>

- <span data-ttu-id="44b89-125">[Distribuição global](distribute-data-globally.md) turnkey com hospedagem múltipla e [failovers automáticos e manuais](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="44b89-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="44b89-126">Suporte para indexação agnóstica de esquema automática em relação a todas as propriedades ("índices secundários") e consultas rápidas</span><span class="sxs-lookup"><span data-stu-id="44b89-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="44b89-127">Suporte para [dimensionamento independente de armazenamento e taxa de transferência](partition-data.md), em qualquer número de regiões</span><span class="sxs-lookup"><span data-stu-id="44b89-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="44b89-128">Suporte para [taxa de transferência dedicada por tabela](request-units.md) que podem ser dimensionados para centenas a milhões de solicitações por segundo</span><span class="sxs-lookup"><span data-stu-id="44b89-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds to millions of requests per second</span></span>
- <span data-ttu-id="44b89-129">Suporte para [cinco níveis de consistência bem definidos](consistency-levels.md) para compensar a disponibilidade, latência e consistência com base nas necessidades do seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="44b89-129">Support for [five tunable consistency levels](consistency-levels.md) to trade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="44b89-130">99,99% de disponibilidade dentro de uma única região e a capacidade de adicionar mais regiões para maior disponibilidade, e [SLAs abrangentes líderes do setor](https://azure.microsoft.com/support/legal/sla/cosmos-db/) em disponibilidade geral</span><span class="sxs-lookup"><span data-stu-id="44b89-130">99.99% availability within a single region, and ability to add more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="44b89-131">Trabalhar com o SDK do .NET de armazenamento do Azure existente e nenhuma alteração de código no seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="44b89-131">Work with the existing Azure storage .NET SDK, and no code changes to your application</span></span>

<span data-ttu-id="44b89-132">Durante a visualização, o Azure Cosmos DB oferece suporte a API de Tabela usando o SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="44b89-132">During the preview, Azure Cosmos DB supports the Table API using the .NET SDK.</span></span> <span data-ttu-id="44b89-133">Você pode baixar o [SDK de Visualização do Armazenamento do Azure](https://aka.ms/premiumtablenuget) do NuGet, que tem as mesmas classes e assinaturas de método que o [SDK de Armazenamento do Azure](https://www.nuget.org/packages/WindowsAzure.Storage), mas também pode conectar-se às contas do Azure Cosmos DB usando a API de Tabela.</span><span class="sxs-lookup"><span data-stu-id="44b89-133">You can download the [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has the same classes and method signatures as the [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect to Azure Cosmos DB accounts using the Table API.</span></span>

<span data-ttu-id="44b89-134">Para saber mais sobre tarefas complexas de armazenamento de Tabelas do Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="44b89-134">To learn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="44b89-135">Introdução ao Azure Cosmos DB: API de Tabela</span><span class="sxs-lookup"><span data-stu-id="44b89-135">Introduction to Azure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="44b89-136">Consulte a documentação de referência do serviço Tabela para saber os detalhes completos sobre a referência da [Biblioteca de Clientes do Armazenamento do Azure para .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409) das APIs disponíveis</span><span class="sxs-lookup"><span data-stu-id="44b89-136">The Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="44b89-137">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="44b89-137">About this tutorial</span></span>
<span data-ttu-id="44b89-138">Este tutorial é para desenvolvedores que estão familiarizados com o SDK de armazenamento de Tabelas do Azure e desejam usar os recursos premium disponíveis usando o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44b89-138">This tutorial is for developers who are familiar with the Azure Table storage SDK, and would like to use the premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="44b89-139">Ele se baseia na [Introdução ao armazenamento de Tabelas do Azure usando o .NET](table-storage-how-to-use-dotnet.md) e mostra como aproveitar os recursos adicionais, como índices secundários, taxa de transferência provisionada e hospedagem múltipla.</span><span class="sxs-lookup"><span data-stu-id="44b89-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how to take advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="44b89-140">Abordaremos como usar o portal do Azure para criar uma conta do Azure Cosmos DB e, em seguida, criar e implantar um aplicativo de Tabela.</span><span class="sxs-lookup"><span data-stu-id="44b89-140">We cover how to use the Azure portal to create an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="44b89-141">Também explicaremos detalhadamente os exemplos de .NET para criar e excluir uma tabela e inserir, atualizar, excluir e consultar dados de tabela.</span><span class="sxs-lookup"><span data-stu-id="44b89-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="44b89-142">Se você ainda não tem o Visual 2017 Studio instalado, poderá baixar e usar o **Visual Studio 2017 Community Edition** [gratuito](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="44b89-142">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="44b89-143">Verifique se você habilitou o **desenvolvimento do Azure** durante a instalação do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44b89-143">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="44b89-144">Crie uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="44b89-144">Create a database account</span></span>

<span data-ttu-id="44b89-145">Vamos começar criando uma conta do Azure Cosmos DB no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="44b89-145">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="44b89-146">Já tem uma conta do Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="44b89-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="44b89-147">Nesse caso, pule para [Configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="44b89-147">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="44b89-148">Você tinha uma conta do Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="44b89-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="44b89-149">Se sua conta agora é uma conta do Azure Cosmos DB, você pode pular para [Configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="44b89-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="44b89-150">Se estiver usando o Emulador do Azure Cosmos DB, execute as etapas em [Emulador do Azure Cosmos DB](local-emulator.md) para configurar o emulador e pule para [Configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="44b89-150">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting to any location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-the-sample-application"></a><span data-ttu-id="44b89-151">Clonar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="44b89-151">Clone the sample application</span></span>

<span data-ttu-id="44b89-152">Agora, clonaremos um aplicativo de Tabela do github, definiremos a cadeia de conexão e o executaremos.</span><span class="sxs-lookup"><span data-stu-id="44b89-152">Now let's clone a Table app from github, set the connection string, and run it.</span></span>

1. <span data-ttu-id="44b89-153">Abra uma janela de terminal do Git, tal como git bash, e `cd` para um diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="44b89-153">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="44b89-154">Execute o comando a seguir para clonar o repositório de exemplo.</span><span class="sxs-lookup"><span data-stu-id="44b89-154">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="44b89-155">Em seguida, abra o arquivo da solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44b89-155">Then open the solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="44b89-156">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="44b89-156">Update your connection string</span></span>

<span data-ttu-id="44b89-157">Agora, volte ao portal do Azure para obter informações sobre a cadeia de conexão e copiá-las para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="44b89-157">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="44b89-158">No [portal do Azure](http://portal.azure.com/), na sua conta do Azure Cosmos DB, no painel de navegação esquerdo, clique em **Chaves**e, em seguida, clique em **Chaves de leitura/gravação**.</span><span class="sxs-lookup"><span data-stu-id="44b89-158">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="44b89-159">Você usará os botões de cópia no lado direito da tela para copiar a cadeia de conexão para o arquivo app.config na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="44b89-159">You'll use the copy buttons on the right side of the screen to copy the connection string into the app.config file in the next step.</span></span>

2. <span data-ttu-id="44b89-160">No Visual Studio, abra o arquivo app.config.</span><span class="sxs-lookup"><span data-stu-id="44b89-160">In Visual Studio, open the app.config file.</span></span> 

3. <span data-ttu-id="44b89-161">Copie o valor do URI do portal (usando o botão de cópia) e torne este o valor de account-key no app.config. Use o nome da conta criado anteriormente para o account-name no app. config.</span><span class="sxs-lookup"><span data-stu-id="44b89-161">Copy your URI value from the portal (using the copy button) and make it the value of the account-key in app.config. Use the account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="44b89-162">Para usar este aplicativo com o Armazenamento de Tabela do Azure padrão, você precisa alterar a cadeia de conexão no `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="44b89-162">To use this app with standard Azure Table Storage, you need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="44b89-163">Use o nome da conta como nome da conta de tabela e a chave como chave primária de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="44b89-163">Use the account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-the-app"></a><span data-ttu-id="44b89-164">Compilar e implantar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="44b89-164">Build and deploy the app</span></span>
1. <span data-ttu-id="44b89-165">No Visual Studio, clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="44b89-165">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="44b89-166">Na caixa **procurar** do NuGet, digite ***WindowsAzure.Storage-PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="44b89-166">In the NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="44b89-167">Marque **Incluir versões de pré-lançamento**.</span><span class="sxs-lookup"><span data-stu-id="44b89-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="44b89-168">Nos resultados, instale o **WindowsAzure. Storage-PremiumTable** e escolha a visualização de compilação `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="44b89-168">From the results, install the **WindowsAzure.Storage-PremiumTable** and choose the preview build `0.0.1-preview`.</span></span> <span data-ttu-id="44b89-169">Essa ação instala o pacote de armazenamento de Tabelas do Azure e todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="44b89-169">This action installs the Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="44b89-170">Clique em CTRL + F5 para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="44b89-170">Click CTRL + F5 to run the application.</span></span> 

<span data-ttu-id="44b89-171">Agora, é possível voltar ao Data Explorer e ver, consultar, modificar e trabalhar com esses dados de tabela.</span><span class="sxs-lookup"><span data-stu-id="44b89-171">You can now go back to Data Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="44b89-172">Para usar este aplicativo com um emulador do Azure Cosmos DB, basta alterar a cadeia de conexão no `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="44b89-172">To use this app with an Azure Cosmos DB Emulator, you just need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="44b89-173">Use o valor abaixo para o emulador.</span><span class="sxs-lookup"><span data-stu-id="44b89-173">Use the below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="44b89-174">Recursos Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="44b89-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="44b89-175">O Azure Cosmos DB oferece suporte a uma série de recursos que não estão disponíveis na API de armazenamento de Tabelas do Azure API.</span><span class="sxs-lookup"><span data-stu-id="44b89-175">Azure Cosmos DB supports a number of capabilities that are not available in the Azure Table storage API.</span></span> <span data-ttu-id="44b89-176">A nova funcionalidade pode ser habilitada através dos seguintes valores de configuração `appSettings`.</span><span class="sxs-lookup"><span data-stu-id="44b89-176">The new functionality can be enabled via the following `appSettings` configuration values.</span></span> <span data-ttu-id="44b89-177">Nós não introduzimos nenhuma nova assinatura ou sobrecarga para a visualização do SDK do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="44b89-177">We did not introduce any new signatures or overloads to the preview Azure Storage SDK.</span></span> <span data-ttu-id="44b89-178">Isso permite que você se conecte a tabelas standard e premium e trabalhe com outros serviços de Armazenamento do Azure como Blobs e Filas.</span><span class="sxs-lookup"><span data-stu-id="44b89-178">This allows you to connect to both standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="44b89-179">Chave</span><span class="sxs-lookup"><span data-stu-id="44b89-179">Key</span></span> | <span data-ttu-id="44b89-180">Descrição</span><span class="sxs-lookup"><span data-stu-id="44b89-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44b89-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="44b89-181">TableConnectionMode</span></span>  | <span data-ttu-id="44b89-182">O Azure Cosmos DB oferece suporte a dois modos de conectividade.</span><span class="sxs-lookup"><span data-stu-id="44b89-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="44b89-183">No modo `Gateway`, as solicitações são sempre feitas no gateway do Azure Cosmos DB, que encaminha para as partições de dados correspondentes.</span><span class="sxs-lookup"><span data-stu-id="44b89-183">In `Gateway` mode, requests are always made to the Azure Cosmos DB gateway, which forwards it to the corresponding data partitions.</span></span> <span data-ttu-id="44b89-184">No modo de conectividade `Direct`, o cliente busca o mapeamento de tabelas de partições e as solicitações são feitas diretamente em partições de dados.</span><span class="sxs-lookup"><span data-stu-id="44b89-184">In `Direct` connectivity mode, the client fetches the mapping of tables to partitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="44b89-185">Recomendamos `Direct`, o padrão.</span><span class="sxs-lookup"><span data-stu-id="44b89-185">We recommend `Direct`, the default.</span></span>  |
| <span data-ttu-id="44b89-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="44b89-186">TableConnectionProtocol</span></span> | <span data-ttu-id="44b89-187">O Azure Cosmos DB oferece suporte a dois protocolos de conexão - `Https` e `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="44b89-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="44b89-188">`Tcp` é o padrão e recomendado porque é mais leve.</span><span class="sxs-lookup"><span data-stu-id="44b89-188">`Tcp` is the default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="44b89-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="44b89-189">TablePreferredLocations</span></span> | <span data-ttu-id="44b89-190">A lista separada por vírgulas de locais (hospedagem múltipla) preferenciais para leituras.</span><span class="sxs-lookup"><span data-stu-id="44b89-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="44b89-191">Cada conta do Azure Cosmos DB pode ser associada a 1 ou 30 ou mais regiões.</span><span class="sxs-lookup"><span data-stu-id="44b89-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="44b89-192">Cada instância do cliente pode especificar um subconjunto dessas regiões na ordem preferida para leituras de baixa latência.</span><span class="sxs-lookup"><span data-stu-id="44b89-192">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="44b89-193">As regiões devem ser nomeadas usando seus [nomes de exibição](https://msdn.microsoft.com/library/azure/gg441293.aspx), por exemplo, `West US`.</span><span class="sxs-lookup"><span data-stu-id="44b89-193">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="44b89-194">Consulte também [APIs de hospedagem múltipla](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="44b89-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="44b89-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="44b89-195">TableConsistencyLevel</span></span> | <span data-ttu-id="44b89-196">Você pode alternar entre disponibilidade, consistência e latência escolhendo entre cinco níveis de consistência bem definidos: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` e `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="44b89-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="44b89-197">O padrão é `Session`.</span><span class="sxs-lookup"><span data-stu-id="44b89-197">Default is `Session`.</span></span> <span data-ttu-id="44b89-198">A escolha do nível de consistência faz uma diferença significativa de desempenho em configurações de várias regiões.</span><span class="sxs-lookup"><span data-stu-id="44b89-198">The choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="44b89-199">Consulte [Níveis de consistência](consistency-levels.md) para saber detalhes.</span><span class="sxs-lookup"><span data-stu-id="44b89-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="44b89-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="44b89-200">TableThroughput</span></span> | <span data-ttu-id="44b89-201">Taxa de transferência reservada para a tabela expressada em unidades de solicitação (RU) por segundo.</span><span class="sxs-lookup"><span data-stu-id="44b89-201">Reserved throughput for the table expressed in request units (RU) per second.</span></span> <span data-ttu-id="44b89-202">Tabelas únicas podem suportar centenas de milhões de RU/s.</span><span class="sxs-lookup"><span data-stu-id="44b89-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="44b89-203">Consulte [Unidades de solicitação](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="44b89-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="44b89-204">O padrão é `400`</span><span class="sxs-lookup"><span data-stu-id="44b89-204">Default is `400`</span></span> |
| <span data-ttu-id="44b89-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="44b89-205">TableIndexingPolicy</span></span> | <span data-ttu-id="44b89-206">Indexação secundária consistente e automática de todas as colunas de tabelas</span><span class="sxs-lookup"><span data-stu-id="44b89-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="44b89-207">Cadeia de caracteres de JSON em conformidade com a política de indexação.</span><span class="sxs-lookup"><span data-stu-id="44b89-207">JSON string conforming to the indexing policy specification.</span></span> <span data-ttu-id="44b89-208">Consulte [Política de indexação](indexing-policies.md) para ver como você pode alterar a política de indexação para incluir/excluir colunas específicas.</span><span class="sxs-lookup"><span data-stu-id="44b89-208">See [Indexing Policy](indexing-policies.md) to see how you can change indexing policy to include/exclude specific columns.</span></span> | <span data-ttu-id="44b89-209">Indexação automática de todas as propriedades (hash para cadeias de caracteres e o intervalo de números)</span><span class="sxs-lookup"><span data-stu-id="44b89-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="44b89-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="44b89-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="44b89-211">Configure o número máximo de itens retornados por consultas de tabela em uma única viagem de ida e volta.</span><span class="sxs-lookup"><span data-stu-id="44b89-211">Configure the maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="44b89-212">O padrão é `-1`, que permite ao Azure Cosmos DB determinar dinamicamente o valor em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="44b89-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |
| <span data-ttu-id="44b89-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="44b89-213">TableQueryEnableScan</span></span> | <span data-ttu-id="44b89-214">Se a consulta não pode usar o índice para qualquer filtro, em seguida, execute assim mesmo por meio de uma varredura.</span><span class="sxs-lookup"><span data-stu-id="44b89-214">If the query cannot use the index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="44b89-215">O padrão é `false`.</span><span class="sxs-lookup"><span data-stu-id="44b89-215">Default is `false`.</span></span>|
| <span data-ttu-id="44b89-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="44b89-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="44b89-217">O grau de paralelismo para execução de uma consulta entre partições.</span><span class="sxs-lookup"><span data-stu-id="44b89-217">The degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="44b89-218">`0` é serial sem nenhuma busca prévia, `1` é serial com busca prévia e valores mais altos aumentam a taxa de paralelismo.</span><span class="sxs-lookup"><span data-stu-id="44b89-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase the rate of parallelism.</span></span> <span data-ttu-id="44b89-219">O padrão é `-1`, que permite ao Azure Cosmos DB determinar dinamicamente o valor em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="44b89-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |

<span data-ttu-id="44b89-220">Para alterar o valor padrão, abra o arquivo `app.config` do Gerenciador de Soluções no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44b89-220">To change the default value, open the `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="44b89-221">Adicionar o conteúdo do elemento `<appSettings>` mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="44b89-221">Add the contents of the `<appSettings>` element shown below.</span></span> <span data-ttu-id="44b89-222">Substitua `account-name` pelo nome da sua conta de armazenamento e `account-key` pela chave de acesso da conta.</span><span class="sxs-lookup"><span data-stu-id="44b89-222">Replace `account-name` with the name of your storage account, and `account-key` with your account access key.</span></span> 

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

<span data-ttu-id="44b89-223">Façamos uma rápida revisão do que está acontecendo no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="44b89-223">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="44b89-224">Abra o arquivo `Program.cs` e veja que essas linhas de código criam os recursos da Tabela.</span><span class="sxs-lookup"><span data-stu-id="44b89-224">Open the `Program.cs` file and you find that these lines of code create the Table resources.</span></span> 

## <a name="create-the-table-client"></a><span data-ttu-id="44b89-225">Criar o cliente da tabela</span><span class="sxs-lookup"><span data-stu-id="44b89-225">Create the table client</span></span>
<span data-ttu-id="44b89-226">Você deve inicializar um `CloudTableClient` para conectar-se à conta de tabela.</span><span class="sxs-lookup"><span data-stu-id="44b89-226">You initialize a `CloudTableClient` to connect to the table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="44b89-227">Esse cliente é inicializado usando os valores de configuração `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel` e `TablePreferredLocations` se especificados nas configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="44b89-227">This client is initialized using the `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in the app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="44b89-228">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="44b89-228">Create a table</span></span>
<span data-ttu-id="44b89-229">Em seguida, você cria uma tabela usando `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="44b89-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="44b89-230">As tabelas no Azure Cosmos DB pode ser dimensionada independentemente em termos de armazenamento e taxa de transferência e o particionamento é tratado automaticamente pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="44b89-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by the service.</span></span> <span data-ttu-id="44b89-231">O Azure Cosmos DB oferece suporte a tabelas ilimitadas e tamanho fixo.</span><span class="sxs-lookup"><span data-stu-id="44b89-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="44b89-232">Consulte [Particionamento no Azure Cosmos DB](partition-data.md) para saber detalhes.</span><span class="sxs-lookup"><span data-stu-id="44b89-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="44b89-233">Há uma diferença importante em como as tabelas são criadas.</span><span class="sxs-lookup"><span data-stu-id="44b89-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="44b89-234">O Azure Cosmos DB reserva a taxa de transferência, ao contrário do modelo baseado em consumo do armazenamento do Azure para transações.</span><span class="sxs-lookup"><span data-stu-id="44b89-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="44b89-235">O modelo de reserva tem dois benefícios principais:</span><span class="sxs-lookup"><span data-stu-id="44b89-235">The reservation model has two key benefits:</span></span>

* <span data-ttu-id="44b89-236">A taxa de transferência é dedicada/reservada, para que você nunca sofra restrições se a taxa de solicitação está no limite ou abaixo da sua taxa de transferência provisionada</span><span class="sxs-lookup"><span data-stu-id="44b89-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="44b89-237">O modelo de reserva é mais [econômico para cargas de trabalho pesadas de taxa de transferência](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="44b89-237">The reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="44b89-238">Você pode configurar a taxa de transferência padrão definindo a configuração para `TableThroughput` em termos de RU (unidades de solicitação) por segundo.</span><span class="sxs-lookup"><span data-stu-id="44b89-238">You can configure the default throughput by configuring the setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="44b89-239">Uma leitura de uma entidade de 1 KB é normalizada como 1 RU e outras operações são normalizados para um valor fixo de RU com base em seu consumo de CPU, memória e IOPS.</span><span class="sxs-lookup"><span data-stu-id="44b89-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized to a fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="44b89-240">Saiba mais sobre [Unidades de solicitação no Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="44b89-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="44b89-241">Enquanto atualmente, o SDK de armazenamento de Tabelas não oferece suporte para a modificação de taxa de transferência, você pode alterar a taxa de transferência instantaneamente a qualquer momento usando o portal do Azure ou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="44b89-241">While Table storage SDK does not currently support modifying throughput, you can change the throughput instantaneously at any time using the Azure portal or Azure CLI.</span></span>

<span data-ttu-id="44b89-242">Em seguida, percorremos as operações simples de leitura e gravação (CRUD) usando o SDK de armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="44b89-242">Next, we walk through the simple read and write (CRUD) operations using the Azure Table storage SDK.</span></span> <span data-ttu-id="44b89-243">Este tutorial demonstra latências baixas de milissegundos de dígito único previsíveis e consultas rápidas fornecidas pelo Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44b89-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="44b89-244">Adicionar uma entidade a uma tabela</span><span class="sxs-lookup"><span data-stu-id="44b89-244">Add an entity to a table</span></span>
<span data-ttu-id="44b89-245">As entidades no armazenamento de Tabelas do Azure estendem-se a partir da classe `TableEntity` e deve ter as propriedades `PartitionKey` e `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="44b89-245">Entities in Azure Table storage extend from the `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="44b89-246">Aqui está um exemplo de definição de uma entidade de cliente.</span><span class="sxs-lookup"><span data-stu-id="44b89-246">Here's a sample definition for a customer entity.</span></span>

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

<span data-ttu-id="44b89-247">O trecho a seguir mostra como inserir uma entidade com o SDK do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="44b89-247">The following snippet shows how to insert an entity with the Azure storage SDK.</span></span> <span data-ttu-id="44b89-248">O Azure Cosmos DB destina-se à garantia de baixa latência em qualquer escala, em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="44b89-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across the world.</span></span>

<span data-ttu-id="44b89-249">As gravações são concluídas em menos de 15 ms em p99 e ~6 ms em p50 para aplicativos executados na mesma região que a conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44b89-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in the same region as the Azure Cosmos DB account.</span></span> <span data-ttu-id="44b89-250">E essa duração de considera o fato de que as gravações são confirmadas para o cliente somente depois que eles são replicados de maneira síncrona, com confirmação permanentemente, e com todo o conteúdo indexado.</span><span class="sxs-lookup"><span data-stu-id="44b89-250">And this duration accounts for the fact that writes are acknowledged back to the client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="44b89-251">A API de Tabela do Azure Cosmos DB está em visualização.</span><span class="sxs-lookup"><span data-stu-id="44b89-251">The Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="44b89-252">Para disponibilidade geral, as garantias de latência p99 contam com os SLAs como outras APIs do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44b89-252">At general availability, the p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="44b89-253">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="44b89-253">Insert a batch of entities</span></span>
<span data-ttu-id="44b89-254">O armazenamento de tabela do Azure suporta uma API de operação em lote, que permite que você combine atualizações, exclusões e inserções na mesma operação de único lote.</span><span class="sxs-lookup"><span data-stu-id="44b89-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in the same single batch operation.</span></span> <span data-ttu-id="44b89-255">O Azure Cosmos DB não tem algumas das limitações na API do lote como armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="44b89-255">Azure Cosmos DB does not have some of the limitations on the batch API as Azure Table storage.</span></span> <span data-ttu-id="44b89-256">Por exemplo, você pode executar várias leituras dentro de um lote, você pode executar várias gravações para a mesma entidade dentro de um lote e não há nenhum limite para 100 operações por lote.</span><span class="sxs-lookup"><span data-stu-id="44b89-256">For example, you can perform multiple reads within a batch, you can perform multiple writes to the same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="44b89-257">Recuperar uma única entidade</span><span class="sxs-lookup"><span data-stu-id="44b89-257">Retrieve a single entity</span></span>
<span data-ttu-id="44b89-258">As recuperações (GETs) no Azure Cosmos DB são concluídas em menos de 10 ms em p99 e ~1 ms em p50 na mesma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="44b89-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in the same Azure region.</span></span> <span data-ttu-id="44b89-259">Você pode adicionar a mesma quantidade de regiões à sua conta para leituras de baixa latência e implantar aplicativos para leitura da sua região local (com hospedagem múltipla), definindo `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="44b89-259">You can add as many regions to your account for low latency reads, and deploy applications to read from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="44b89-260">Você pode recuperar uma única entidade usando o trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="44b89-260">You can retrieve a single entity using the following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="44b89-261">Saiba mais sobre as APIs de hospedagem múltipla em [Desenvolvendo com várias regiões](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="44b89-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="44b89-262">Consultar entidades usando índices secundários automáticos</span><span class="sxs-lookup"><span data-stu-id="44b89-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="44b89-263">Tabelas podem ser consultadas usando a classe `TableQuery`.</span><span class="sxs-lookup"><span data-stu-id="44b89-263">Tables can be queried using the `TableQuery` class.</span></span> <span data-ttu-id="44b89-264">O Azure Cosmos DB tem um mecanismo de banco de dados otimizado para gravação que indexa automaticamente todas as colunas em sua tabela.</span><span class="sxs-lookup"><span data-stu-id="44b89-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="44b89-265">A indexação no Azure Cosmos DB é agnóstica em relação ao esquema.</span><span class="sxs-lookup"><span data-stu-id="44b89-265">Indexing in Azure Cosmos DB is agnostic to schema.</span></span> <span data-ttu-id="44b89-266">Portanto, mesmo que seu esquema seja diferente entre as linhas, ou se o esquema evoluir ao longo do tempo, ele será indexado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="44b89-266">Therefore, even if your schema is different between rows, or if the schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="44b89-267">Como o Azure Cosmos DB oferece suporte a índices secundários automáticos, as consultas em relação a qualquer propriedade podem usar o índice e serem apresentadas de forma eficiente.</span><span class="sxs-lookup"><span data-stu-id="44b89-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use the index and be served efficiently.</span></span>

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

<span data-ttu-id="44b89-268">Na visualização, o Azure Cosmos DB oferece suporte à mesma funcionalidade de consulta que o armazenamento de tabela do Azure para a API de Tabela.</span><span class="sxs-lookup"><span data-stu-id="44b89-268">In preview, Azure Cosmos DB supports the same query functionality as Azure Table storage for the Table API.</span></span> <span data-ttu-id="44b89-269">O Azure Cosmos DB também oferece suporte à classificação, agregações, consulta geoespacial, hierarquia e uma ampla variedade de funções internas.</span><span class="sxs-lookup"><span data-stu-id="44b89-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="44b89-270">Os recursos adicionais serão fornecidos na API de Tabela em uma atualização futura do serviço.</span><span class="sxs-lookup"><span data-stu-id="44b89-270">The additional functionality will be provided in the Table API in a future service update.</span></span> <span data-ttu-id="44b89-271">Consulte [Consulta do Azure Cosmos DB](documentdb-sql-query.md) para uma visão geral desses recursos.</span><span class="sxs-lookup"><span data-stu-id="44b89-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="44b89-272">Substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="44b89-272">Replace an entity</span></span>
<span data-ttu-id="44b89-273">Para atualizar uma entidade, recupere-a do serviço Tabela, modifique o objeto de entidade e, em seguida, salve as alterações novamente no serviço Tabela.</span><span class="sxs-lookup"><span data-stu-id="44b89-273">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="44b89-274">O código a seguir altera o número de telefone de um cliente existente.</span><span class="sxs-lookup"><span data-stu-id="44b89-274">The following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="44b89-275">Da mesma forma, você pode executar as operações `InsertOrMerge` ou `Merge`.</span><span class="sxs-lookup"><span data-stu-id="44b89-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="44b89-276">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="44b89-276">Delete an entity</span></span>
<span data-ttu-id="44b89-277">Você pode excluir facilmente uma entidade após a recuperação usando o mesmo padrão mostrado para a atualização de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="44b89-277">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="44b89-278">O código a seguir recupera e exclui uma entidade de cliente.</span><span class="sxs-lookup"><span data-stu-id="44b89-278">The following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="44b89-279">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="44b89-279">Delete a table</span></span>
<span data-ttu-id="44b89-280">Finalmente, o exemplo de código a seguir exclui uma tabela de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="44b89-280">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="44b89-281">Você pode excluir e recriar uma tabela imediatamente com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44b89-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="44b89-282">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="44b89-282">Clean up resources</span></span> 

<span data-ttu-id="44b89-283">Se você não continuar usando este aplicativo, siga as seguintes etapas para excluir todos os recursos criados neste tutorial no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="44b89-283">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>   

1. <span data-ttu-id="44b89-284">No menu à esquerda no portal do Azure, clique em **Grupos de recursos** e depois clique no nome do recurso criado.</span><span class="sxs-lookup"><span data-stu-id="44b89-284">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span>  
2. <span data-ttu-id="44b89-285">Em sua página de grupo de recursos, clique em **Excluir**, digite o nome do recurso para excluir na caixa de texto e depois clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="44b89-285">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="44b89-286">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="44b89-286">Next steps</span></span>

<span data-ttu-id="44b89-287">Neste tutorial, abordamos como começar a usar o Azure Cosmos DB com a API de Tabela e você tiver feito o seguinte:</span><span class="sxs-lookup"><span data-stu-id="44b89-287">In this tutorial, we covered how to get started using Azure Cosmos DB with the Table API, and you've done the following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="44b89-288">Criou uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="44b89-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="44b89-289">Habilitou a funcionalidade no arquivo app. config</span><span class="sxs-lookup"><span data-stu-id="44b89-289">Enabled functionality in the app.config file</span></span> 
> * <span data-ttu-id="44b89-290">Criou uma tabela</span><span class="sxs-lookup"><span data-stu-id="44b89-290">Created a table</span></span> 
> * <span data-ttu-id="44b89-291">Adicionou uma entidade a uma tabela</span><span class="sxs-lookup"><span data-stu-id="44b89-291">Added an entity to a table</span></span> 
> * <span data-ttu-id="44b89-292">Inseriu um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="44b89-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="44b89-293">Recuperou uma única entidade</span><span class="sxs-lookup"><span data-stu-id="44b89-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="44b89-294">Consultou entidades usando índices secundários automáticos</span><span class="sxs-lookup"><span data-stu-id="44b89-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="44b89-295">Substituiu uma entidade</span><span class="sxs-lookup"><span data-stu-id="44b89-295">Replaced an entity</span></span> 
> * <span data-ttu-id="44b89-296">Excluiu uma entidade</span><span class="sxs-lookup"><span data-stu-id="44b89-296">Deleted an entity</span></span> 
> * <span data-ttu-id="44b89-297">Excluiu uma tabela</span><span class="sxs-lookup"><span data-stu-id="44b89-297">Deleted a table</span></span>  

<span data-ttu-id="44b89-298">Agora você pode prosseguir para o próximo tutorial e saber mais sobre como consultar dados da tabela.</span><span class="sxs-lookup"><span data-stu-id="44b89-298">You can now proceed to the next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="44b89-299">Consulta com a API de Tabela</span><span class="sxs-lookup"><span data-stu-id="44b89-299">Query with the Table API</span></span>](tutorial-query-table.md)
