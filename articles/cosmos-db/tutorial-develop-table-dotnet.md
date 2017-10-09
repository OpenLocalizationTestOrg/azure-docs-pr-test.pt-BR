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
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a><span data-ttu-id="0b00c-103">Cosmos do Azure DB: Desenvolver com hello API de tabela no .NET</span><span class="sxs-lookup"><span data-stu-id="0b00c-103">Azure Cosmos DB: Develop with hello Table API in .NET</span></span>

<span data-ttu-id="0b00c-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0b00c-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="0b00c-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="0b00c-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="0b00c-106">Este tutorial aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b00c-106">This tutorial covers hello following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="0b00c-107">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0b00c-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="0b00c-108">Habilitar a funcionalidade no arquivo App. config de saudação</span><span class="sxs-lookup"><span data-stu-id="0b00c-108">Enable functionality in hello app.config file</span></span> 
> * <span data-ttu-id="0b00c-109">Criar uma tabela usando Olá [API tabela](table-introduction.md) (visualização)</span><span class="sxs-lookup"><span data-stu-id="0b00c-109">Create a table using hello [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="0b00c-110">Adicionar uma tabela de entidade tooa</span><span class="sxs-lookup"><span data-stu-id="0b00c-110">Add an entity tooa table</span></span> 
> * <span data-ttu-id="0b00c-111">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="0b00c-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="0b00c-112">Recuperar uma única entidade</span><span class="sxs-lookup"><span data-stu-id="0b00c-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="0b00c-113">Consultar entidades usando índices secundários automáticos</span><span class="sxs-lookup"><span data-stu-id="0b00c-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="0b00c-114">Substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="0b00c-114">Replace an entity</span></span> 
> * <span data-ttu-id="0b00c-115">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="0b00c-115">Delete an entity</span></span> 
> * <span data-ttu-id="0b00c-116">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="0b00c-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="0b00c-117">Tabelas no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0b00c-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="0b00c-118">Banco de dados do Azure Cosmos fornece Olá [API tabela](table-introduction.md) (visualização) para aplicativos que precisam de um repositório de chave-valor com um design sem esquema.</span><span class="sxs-lookup"><span data-stu-id="0b00c-118">Azure Cosmos DB provides hello [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="0b00c-119">[Armazenamento de tabela do Azure](../storage/common/storage-introduction.md) SDKs e APIs REST podem ser toowork usado com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0b00c-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used toowork with Azure Cosmos DB.</span></span> <span data-ttu-id="0b00c-120">Você pode usar as tabelas do banco de dados do Azure Cosmos toocreate com requisitos de alta taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="0b00c-120">You can use Azure Cosmos DB toocreate tables with high throughput requirements.</span></span> <span data-ttu-id="0b00c-121">O Azure Cosmos DB dá suporte a tabelas com otimização de taxa de transferência (chamadas informalmente de "tabelas premium"), atualmente em visualização pública.</span><span class="sxs-lookup"><span data-stu-id="0b00c-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="0b00c-122">Você pode continuar toouse armazenamento de tabela do Azure para tabelas com armazenamento de alta e reduzir os requisitos de taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="0b00c-122">You can continue toouse Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="0b00c-123">Banco de dados do Azure Cosmos apresenta suporte para tabelas com otimização de armazenamento em uma atualização futura e tabela de Azure existentes e novas contas de armazenamento será perfeitamente atualizado tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0b00c-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded tooAzure Cosmos DB.</span></span>

<span data-ttu-id="0b00c-124">Se você usar o armazenamento de tabela do Azure no momento, você ganha Olá benefícios com visualização de "tabela premium" hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b00c-124">If you currently use Azure Table storage, you gain hello following benefits with hello "premium table" preview:</span></span>

- <span data-ttu-id="0b00c-125">[Distribuição global](distribute-data-globally.md) turnkey com hospedagem múltipla e [failovers automáticos e manuais](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="0b00c-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="0b00c-126">Suporte para indexação agnóstica de esquema automática em relação a todas as propriedades ("índices secundários") e consultas rápidas</span><span class="sxs-lookup"><span data-stu-id="0b00c-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="0b00c-127">Suporte para [dimensionamento independente de armazenamento e taxa de transferência](partition-data.md), em qualquer número de regiões</span><span class="sxs-lookup"><span data-stu-id="0b00c-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="0b00c-128">Suporte para [dedicada de taxa de transferência por tabela](request-units.md) que podem ser dimensionados de centenas toomillions de solicitações por segundo</span><span class="sxs-lookup"><span data-stu-id="0b00c-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds toomillions of requests per second</span></span>
- <span data-ttu-id="0b00c-129">Suporte para [cinco níveis de consistência ajustáveis](consistency-levels.md) tootrade disponibilidade, latência e consistência com base em suas necessidades de aplicativo</span><span class="sxs-lookup"><span data-stu-id="0b00c-129">Support for [five tunable consistency levels](consistency-levels.md) tootrade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="0b00c-130">disponibilidade de 99,99% em uma única região e capacidade tooadd mais regiões para alta disponibilidade, e [SLAs abrangentes do setor](https://azure.microsoft.com/support/legal/sla/cosmos-db/) em disponibilidade geral</span><span class="sxs-lookup"><span data-stu-id="0b00c-130">99.99% availability within a single region, and ability tooadd more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="0b00c-131">Trabalhar com o armazenamento do Azure existente Olá .NET SDK e nenhum aplicativo de tooyour de alterações de código</span><span class="sxs-lookup"><span data-stu-id="0b00c-131">Work with hello existing Azure storage .NET SDK, and no code changes tooyour application</span></span>

<span data-ttu-id="0b00c-132">Durante a visualização de Olá, oferece suporte a banco de dados do Azure Cosmos Olá API de tabela usando o SDK .NET de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b00c-132">During hello preview, Azure Cosmos DB supports hello Table API using hello .NET SDK.</span></span> <span data-ttu-id="0b00c-133">Você pode baixar Olá [SDK de visualização do armazenamento do Azure](https://aka.ms/premiumtablenuget) do NuGet, que tem Olá mesmas classes e assinaturas de método como Olá [SDK de armazenamento do Azure](https://www.nuget.org/packages/WindowsAzure.Storage), mas também pode se conectar tooAzure Cosmos DB contas usando Olá Tabela de API.</span><span class="sxs-lookup"><span data-stu-id="0b00c-133">You can download hello [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has hello same classes and method signatures as hello [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect tooAzure Cosmos DB accounts using hello Table API.</span></span>

<span data-ttu-id="0b00c-134">toolearn mais informações sobre tarefas complexas do armazenamento de tabela do Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="0b00c-134">toolearn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="0b00c-135">Introdução tooAzure Cosmos DB: API de tabela</span><span class="sxs-lookup"><span data-stu-id="0b00c-135">Introduction tooAzure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="0b00c-136">Olá documentação de referência de serviço de tabela para obter detalhes completos sobre as APIs disponíveis [biblioteca de cliente de armazenamento para a referência do .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="0b00c-136">hello Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="0b00c-137">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="0b00c-137">About this tutorial</span></span>
<span data-ttu-id="0b00c-138">Este tutorial é para desenvolvedores que estão familiarizados com hello SDK de armazenamento de tabela do Azure e deseja que os recursos do premium Olá toouse disponíveis usando o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0b00c-138">This tutorial is for developers who are familiar with hello Azure Table storage SDK, and would like toouse hello premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="0b00c-139">Ele se baseia [Introdução ao armazenamento de tabela do Azure usando o .NET](table-storage-how-to-use-dotnet.md) e mostra como tootake proveito dos recursos adicionais, como índices secundários, taxa de transferência fornecida e hospedagem múltipla.</span><span class="sxs-lookup"><span data-stu-id="0b00c-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how tootake advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="0b00c-140">Abordaremos como toouse Olá toocreate portal do Azure uma conta de banco de dados do Azure Cosmos e, em seguida, criar e implantar um aplicativo de tabela.</span><span class="sxs-lookup"><span data-stu-id="0b00c-140">We cover how toouse hello Azure portal toocreate an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="0b00c-141">Também explicaremos detalhadamente os exemplos de .NET para criar e excluir uma tabela e inserir, atualizar, excluir e consultar dados de tabela.</span><span class="sxs-lookup"><span data-stu-id="0b00c-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="0b00c-142">Se você ainda não tiver o Visual Studio de 2017 instalado, você pode baixar e usar o hello **livre** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0b00c-142">If you don't already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="0b00c-143">Certifique-se de que você habilite **desenvolvimento do Azure** durante a instalação do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="0b00c-143">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="0b00c-144">Criar uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="0b00c-144">Create a database account</span></span>

<span data-ttu-id="0b00c-145">Vamos começar criando uma conta de banco de dados do Azure Cosmos em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b00c-145">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="0b00c-146">Já tem uma conta do Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="0b00c-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="0b00c-147">Nesse caso, pular muito[configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="0b00c-147">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="0b00c-148">Você tinha uma conta do Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="0b00c-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="0b00c-149">Se assim, sua conta agora é uma conta de banco de dados do Azure Cosmos e poderá pular muito[configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="0b00c-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="0b00c-150">Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) toosetup Olá emulador e pular muito[configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="0b00c-150">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a><span data-ttu-id="0b00c-151">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="0b00c-151">Clone hello sample application</span></span>

<span data-ttu-id="0b00c-152">Agora vamos, clonar um aplicativo de tabela do github, defina a cadeia de caracteres de conexão hello e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="0b00c-152">Now let's clone a Table app from github, set hello connection string, and run it.</span></span>

1. <span data-ttu-id="0b00c-153">Abra uma janela de terminal de git, como git bash, e `cd` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0b00c-153">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="0b00c-154">Execute Olá repositório de exemplo do comando tooclone Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="0b00c-154">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="0b00c-155">Em seguida, abra o arquivo de solução de saudação no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b00c-155">Then open hello solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="0b00c-156">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="0b00c-156">Update your connection string</span></span>

<span data-ttu-id="0b00c-157">Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0b00c-157">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="0b00c-158">Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**.</span><span class="sxs-lookup"><span data-stu-id="0b00c-158">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="0b00c-159">Você usará botões de cópia Olá Olá direita da cadeia de conexão do hello tela toocopy Olá em arquivo App. config de saudação na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="0b00c-159">You'll use hello copy buttons on hello right side of hello screen toocopy hello connection string into hello app.config file in hello next step.</span></span>

2. <span data-ttu-id="0b00c-160">No Visual Studio, abra o arquivo App. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b00c-160">In Visual Studio, open hello app.config file.</span></span> 

3. <span data-ttu-id="0b00c-161">Copie o valor URI do portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá o valor da chave conta Olá no App. config. Use nome de conta Olá criada anteriormente para o nome de conta no App. config.</span><span class="sxs-lookup"><span data-stu-id="0b00c-161">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello account-key in app.config. Use hello account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="0b00c-162">toouse esse aplicativo com o armazenamento de tabela do Azure padrão, você precisa de cadeia de conexão de Olá toochange em `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="0b00c-162">toouse this app with standard Azure Table Storage, you need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="0b00c-163">Use nome de conta do hello como o nome da conta de tabela e a chave como chave primária de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b00c-163">Use hello account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a><span data-ttu-id="0b00c-164">Criar e implantar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="0b00c-164">Build and deploy hello app</span></span>
1. <span data-ttu-id="0b00c-165">No Visual Studio, clique com botão direito no projeto Olá no **Solution Explorer** e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0b00c-165">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="0b00c-166">Em Olá NuGet **procurar** , digite ***windowsazure PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="0b00c-166">In hello NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="0b00c-167">Marque **Incluir versões de pré-lançamento**.</span><span class="sxs-lookup"><span data-stu-id="0b00c-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="0b00c-168">Resultados de hello, instalar Olá **windowsazure PremiumTable** e escolha a compilação de visualização de saudação `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="0b00c-168">From hello results, install hello **WindowsAzure.Storage-PremiumTable** and choose hello preview build `0.0.1-preview`.</span></span> <span data-ttu-id="0b00c-169">Essa ação instala o pacote de armazenamento de tabela do Azure hello e todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="0b00c-169">This action installs hello Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="0b00c-170">Clique em CTRL + F5 aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="0b00c-170">Click CTRL + F5 toorun hello application.</span></span> 

<span data-ttu-id="0b00c-171">Agora você pode voltar tooData Explorer e consulte a consulta, modificar e trabalhar com esses dados de tabela.</span><span class="sxs-lookup"><span data-stu-id="0b00c-171">You can now go back tooData Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="0b00c-172">toouse esse aplicativo com o emulador do Azure Cosmos banco de dados, você apenas precisa de cadeia de conexão Olá toochange no `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="0b00c-172">toouse this app with an Azure Cosmos DB Emulator, you just need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="0b00c-173">Saudação de uso abaixo do valor de emulador.</span><span class="sxs-lookup"><span data-stu-id="0b00c-173">Use hello below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="0b00c-174">Recursos Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0b00c-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="0b00c-175">Banco de dados do Azure Cosmos dá suporte a vários recursos que não estão disponíveis no hello API de armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b00c-175">Azure Cosmos DB supports a number of capabilities that are not available in hello Azure Table storage API.</span></span> <span data-ttu-id="0b00c-176">Olá nova funcionalidade pode ser habilitada por meio do seguinte Olá `appSettings` valores de configuração.</span><span class="sxs-lookup"><span data-stu-id="0b00c-176">hello new functionality can be enabled via hello following `appSettings` configuration values.</span></span> <span data-ttu-id="0b00c-177">Não apresentamos qualquer nova assinaturas ou sobrecargas toohello visualização do SDK do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b00c-177">We did not introduce any new signatures or overloads toohello preview Azure Storage SDK.</span></span> <span data-ttu-id="0b00c-178">Isso permite que você tooconnect tooboth standard e premium tabelas e trabalho com outros serviços de armazenamento do Azure como Blobs e filas.</span><span class="sxs-lookup"><span data-stu-id="0b00c-178">This allows you tooconnect tooboth standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="0b00c-179">Chave</span><span class="sxs-lookup"><span data-stu-id="0b00c-179">Key</span></span> | <span data-ttu-id="0b00c-180">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b00c-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0b00c-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="0b00c-181">TableConnectionMode</span></span>  | <span data-ttu-id="0b00c-182">O Azure Cosmos DB oferece suporte a dois modos de conectividade.</span><span class="sxs-lookup"><span data-stu-id="0b00c-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="0b00c-183">Em `Gateway` modo, as solicitações sempre são feitas gateway de banco de dados do Azure Cosmos toohello, que encaminha toohello partições de dados correspondente.</span><span class="sxs-lookup"><span data-stu-id="0b00c-183">In `Gateway` mode, requests are always made toohello Azure Cosmos DB gateway, which forwards it toohello corresponding data partitions.</span></span> <span data-ttu-id="0b00c-184">Em `Direct` modo de conectividade cliente Olá busca o mapeamento de saudação do toopartitions de tabelas e as solicitações são feitas diretamente em partições de dados.</span><span class="sxs-lookup"><span data-stu-id="0b00c-184">In `Direct` connectivity mode, hello client fetches hello mapping of tables toopartitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="0b00c-185">É recomendável `Direct`, Olá padrão.</span><span class="sxs-lookup"><span data-stu-id="0b00c-185">We recommend `Direct`, hello default.</span></span>  |
| <span data-ttu-id="0b00c-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="0b00c-186">TableConnectionProtocol</span></span> | <span data-ttu-id="0b00c-187">O Azure Cosmos DB oferece suporte a dois protocolos de conexão - `Https` e `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="0b00c-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="0b00c-188">`Tcp`saudação padrão e recomendada, pois é mais simples.</span><span class="sxs-lookup"><span data-stu-id="0b00c-188">`Tcp` is hello default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="0b00c-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="0b00c-189">TablePreferredLocations</span></span> | <span data-ttu-id="0b00c-190">A lista separada por vírgulas de locais (hospedagem múltipla) preferenciais para leituras.</span><span class="sxs-lookup"><span data-stu-id="0b00c-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="0b00c-191">Cada conta do Azure Cosmos DB pode ser associada a 1 ou 30 ou mais regiões.</span><span class="sxs-lookup"><span data-stu-id="0b00c-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="0b00c-192">Cada instância de cliente pode especificar um subconjunto dessas regiões Olá preferido para leituras de baixa latência.</span><span class="sxs-lookup"><span data-stu-id="0b00c-192">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="0b00c-193">regiões de saudação devem ser nomeados usando seus [exibir nomes](https://msdn.microsoft.com/library/azure/gg441293.aspx), por exemplo, `West US`.</span><span class="sxs-lookup"><span data-stu-id="0b00c-193">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="0b00c-194">Consulte também [APIs de hospedagem múltipla](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="0b00c-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="0b00c-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="0b00c-195">TableConsistencyLevel</span></span> | <span data-ttu-id="0b00c-196">Você pode alternar entre disponibilidade, consistência e latência escolhendo entre cinco níveis de consistência bem definidos: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` e `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="0b00c-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="0b00c-197">O padrão é `Session`.</span><span class="sxs-lookup"><span data-stu-id="0b00c-197">Default is `Session`.</span></span> <span data-ttu-id="0b00c-198">Escolha de saudação do nível de consistência faz diferença significativa de desempenho em configurações de várias regiões.</span><span class="sxs-lookup"><span data-stu-id="0b00c-198">hello choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="0b00c-199">Consulte [Níveis de consistência](consistency-levels.md) para saber detalhes.</span><span class="sxs-lookup"><span data-stu-id="0b00c-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="0b00c-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="0b00c-200">TableThroughput</span></span> | <span data-ttu-id="0b00c-201">Taxa de transferência reservada para a tabela de saudação expressada em unidades de solicitação (RU) por segundo.</span><span class="sxs-lookup"><span data-stu-id="0b00c-201">Reserved throughput for hello table expressed in request units (RU) per second.</span></span> <span data-ttu-id="0b00c-202">Tabelas únicas podem suportar centenas de milhões de RU/s.</span><span class="sxs-lookup"><span data-stu-id="0b00c-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="0b00c-203">Consulte [Unidades de solicitação](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="0b00c-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="0b00c-204">O padrão é `400`</span><span class="sxs-lookup"><span data-stu-id="0b00c-204">Default is `400`</span></span> |
| <span data-ttu-id="0b00c-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="0b00c-205">TableIndexingPolicy</span></span> | <span data-ttu-id="0b00c-206">Indexação secundária consistente e automática de todas as colunas de tabelas</span><span class="sxs-lookup"><span data-stu-id="0b00c-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="0b00c-207">Toohello de conformidade de cadeia de caracteres JSON especificação da política de indexação.</span><span class="sxs-lookup"><span data-stu-id="0b00c-207">JSON string conforming toohello indexing policy specification.</span></span> <span data-ttu-id="0b00c-208">Consulte [política de indexação](indexing-policies.md) toosee como você pode alterar a indexação colunas específicas tooinclude/exclusão de política.</span><span class="sxs-lookup"><span data-stu-id="0b00c-208">See [Indexing Policy](indexing-policies.md) toosee how you can change indexing policy tooinclude/exclude specific columns.</span></span> | <span data-ttu-id="0b00c-209">Indexação automática de todas as propriedades (hash para cadeias de caracteres e o intervalo de números)</span><span class="sxs-lookup"><span data-stu-id="0b00c-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="0b00c-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="0b00c-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="0b00c-211">Configure o número máximo de saudação de itens retornados por consultas de tabela em uma única viagem de ida.</span><span class="sxs-lookup"><span data-stu-id="0b00c-211">Configure hello maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="0b00c-212">O padrão é `-1`, que permite que o banco de dados do Azure Cosmos determinar dinamicamente o valor de saudação em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="0b00c-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |
| <span data-ttu-id="0b00c-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="0b00c-213">TableQueryEnableScan</span></span> | <span data-ttu-id="0b00c-214">Se a consulta de saudação não pode usar índice Olá para qualquer filtro, em seguida, executá-lo assim mesmo por meio de uma verificação.</span><span class="sxs-lookup"><span data-stu-id="0b00c-214">If hello query cannot use hello index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="0b00c-215">O padrão é `false`.</span><span class="sxs-lookup"><span data-stu-id="0b00c-215">Default is `false`.</span></span>|
| <span data-ttu-id="0b00c-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="0b00c-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="0b00c-217">grau de saudação de paralelismo de execução de uma consulta entre partições.</span><span class="sxs-lookup"><span data-stu-id="0b00c-217">hello degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="0b00c-218">`0`serial com nenhuma pré-leitura, `1` serial com pré-leitura e valores maior taxa de saudação do aumento de paralelismo.</span><span class="sxs-lookup"><span data-stu-id="0b00c-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase hello rate of parallelism.</span></span> <span data-ttu-id="0b00c-219">O padrão é `-1`, que permite que o banco de dados do Azure Cosmos determinar dinamicamente o valor de saudação em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="0b00c-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |

<span data-ttu-id="0b00c-220">valor padrão do hello toochange, abra Olá `app.config` arquivo no Gerenciador de soluções no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b00c-220">toochange hello default value, open hello `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="0b00c-221">Adicionar conteúdo Olá Olá `<appSettings>` elemento mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="0b00c-221">Add hello contents of hello `<appSettings>` element shown below.</span></span> <span data-ttu-id="0b00c-222">Substituir `account-name` com o nome de saudação da sua conta de armazenamento e `account-key` com sua chave de acesso da conta.</span><span class="sxs-lookup"><span data-stu-id="0b00c-222">Replace `account-name` with hello name of your storage account, and `account-key` with your account access key.</span></span> 

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

<span data-ttu-id="0b00c-223">Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0b00c-223">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="0b00c-224">Olá abrir `Program.cs` arquivo e descobrir que essas linhas de código criam Olá recursos de tabela.</span><span class="sxs-lookup"><span data-stu-id="0b00c-224">Open hello `Program.cs` file and you find that these lines of code create hello Table resources.</span></span> 

## <a name="create-hello-table-client"></a><span data-ttu-id="0b00c-225">Crie saudação do cliente de tabela</span><span class="sxs-lookup"><span data-stu-id="0b00c-225">Create hello table client</span></span>
<span data-ttu-id="0b00c-226">Você inicializar um `CloudTableClient` conta de tabela toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="0b00c-226">You initialize a `CloudTableClient` tooconnect toohello table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="0b00c-227">Esse cliente é inicializado usando Olá `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, e `TablePreferredLocations` valores de configuração, se especificado nas configurações de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0b00c-227">This client is initialized using hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in hello app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="0b00c-228">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="0b00c-228">Create a table</span></span>
<span data-ttu-id="0b00c-229">Em seguida, você cria uma tabela usando `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="0b00c-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="0b00c-230">Tabelas no banco de dados do Azure Cosmos podem dimensionada de forma independente em termos de armazenamento e a taxa de transferência e o particionamento é tratado automaticamente pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b00c-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by hello service.</span></span> <span data-ttu-id="0b00c-231">O Azure Cosmos DB oferece suporte a tabelas ilimitadas e tamanho fixo.</span><span class="sxs-lookup"><span data-stu-id="0b00c-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="0b00c-232">Consulte [Particionamento no Azure Cosmos DB](partition-data.md) para saber detalhes.</span><span class="sxs-lookup"><span data-stu-id="0b00c-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="0b00c-233">Há uma diferença importante em como as tabelas são criadas.</span><span class="sxs-lookup"><span data-stu-id="0b00c-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="0b00c-234">O Azure Cosmos DB reserva a taxa de transferência, ao contrário do modelo baseado em consumo do armazenamento do Azure para transações.</span><span class="sxs-lookup"><span data-stu-id="0b00c-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="0b00c-235">modelo de reserva Olá tem dois benefícios principais:</span><span class="sxs-lookup"><span data-stu-id="0b00c-235">hello reservation model has two key benefits:</span></span>

* <span data-ttu-id="0b00c-236">A taxa de transferência é dedicada/reservada, para que você nunca sofra restrições se a taxa de solicitação está no limite ou abaixo da sua taxa de transferência provisionada</span><span class="sxs-lookup"><span data-stu-id="0b00c-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="0b00c-237">modelo de reserva de saudação é mais [econômico para cargas de trabalho pesadas de taxa de transferência](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="0b00c-237">hello reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="0b00c-238">Você pode configurar a taxa de transferência saudação padrão por configuração hello para `TableThroughput` em termos de RUS (unidades de solicitação) por segundo.</span><span class="sxs-lookup"><span data-stu-id="0b00c-238">You can configure hello default throughput by configuring hello setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="0b00c-239">Uma leitura de uma entidade de 1 KB é normalizada como 1 RU e outras operações são normalizada tooa RU valor com base no seu consumo de CPU, memória e IOPS fixo.</span><span class="sxs-lookup"><span data-stu-id="0b00c-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized tooa fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="0b00c-240">Saiba mais sobre [Unidades de solicitação no Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="0b00c-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0b00c-241">Enquanto o SDK de armazenamento de tabela não oferece suporte a modificação de taxa de transferência, você pode alterar a taxa de transferência Olá instantaneamente a qualquer momento usando o portal do Azure de saudação ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b00c-241">While Table storage SDK does not currently support modifying throughput, you can change hello throughput instantaneously at any time using hello Azure portal or Azure CLI.</span></span>

<span data-ttu-id="0b00c-242">Em seguida, percorremos leitura simples hello e operações de gravação (CRUD) usando armazenamento de tabela do Azure Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="0b00c-242">Next, we walk through hello simple read and write (CRUD) operations using hello Azure Table storage SDK.</span></span> <span data-ttu-id="0b00c-243">Este tutorial demonstra latências baixas de milissegundos de dígito único previsíveis e consultas rápidas fornecidas pelo Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0b00c-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="0b00c-244">Adicionar uma tabela de entidade tooa</span><span class="sxs-lookup"><span data-stu-id="0b00c-244">Add an entity tooa table</span></span>
<span data-ttu-id="0b00c-245">As entidades no armazenamento de tabela do Azure estendem da saudação `TableEntity` classe e deve ter `PartitionKey` e `RowKey` propriedades.</span><span class="sxs-lookup"><span data-stu-id="0b00c-245">Entities in Azure Table storage extend from hello `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="0b00c-246">Aqui está um exemplo de definição de uma entidade de cliente.</span><span class="sxs-lookup"><span data-stu-id="0b00c-246">Here's a sample definition for a customer entity.</span></span>

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

<span data-ttu-id="0b00c-247">saudação de trecho de código a seguir mostra como tooinsert uma entidade com hello SDK de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b00c-247">hello following snippet shows how tooinsert an entity with hello Azure storage SDK.</span></span> <span data-ttu-id="0b00c-248">Banco de dados do Azure Cosmos destina-se a garantia de baixa latência em qualquer escala em Olá, mundo.</span><span class="sxs-lookup"><span data-stu-id="0b00c-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across hello world.</span></span>

<span data-ttu-id="0b00c-249">Conclusão de gravações < 15 ms em p99 e ~ 6 ms em p50 para aplicativos executados em Olá Olá conta de banco de dados do Azure Cosmos mesma região.</span><span class="sxs-lookup"><span data-stu-id="0b00c-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in hello same region as hello Azure Cosmos DB account.</span></span> <span data-ttu-id="0b00c-250">E a duração da contas do fato de saudação que grava reconhecidas toohello back cliente somente depois que eles são replicados de maneira síncrona, forma duradoura confirmada, e todo o conteúdo foi indexado.</span><span class="sxs-lookup"><span data-stu-id="0b00c-250">And this duration accounts for hello fact that writes are acknowledged back toohello client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="0b00c-251">Olá API de tabela para o banco de dados do Azure Cosmos está em visualização.</span><span class="sxs-lookup"><span data-stu-id="0b00c-251">hello Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="0b00c-252">Disponibilidade geral, Olá p99 latência garantias contam com SLAs como outras APIs de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0b00c-252">At general availability, hello p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

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

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="0b00c-253">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="0b00c-253">Insert a batch of entities</span></span>
<span data-ttu-id="0b00c-254">Oferece suporte de armazenamento do Azure tabela uma API de operação em lote, que permite que você combine atualizações, exclusões e inserções em Olá a mesma operação de lote único.</span><span class="sxs-lookup"><span data-stu-id="0b00c-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in hello same single batch operation.</span></span> <span data-ttu-id="0b00c-255">Banco de dados do Azure Cosmos não tem algumas das limitações de saudação na API de lote hello como armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b00c-255">Azure Cosmos DB does not have some of hello limitations on hello batch API as Azure Table storage.</span></span> <span data-ttu-id="0b00c-256">Por exemplo, você pode executar várias leituras dentro de um lote, você pode executar várias toohello de gravações mesma entidade dentro de um lote, e não há nenhum limite no 100 operações por lote.</span><span class="sxs-lookup"><span data-stu-id="0b00c-256">For example, you can perform multiple reads within a batch, you can perform multiple writes toohello same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

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
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="0b00c-257">Recuperar uma única entidade</span><span class="sxs-lookup"><span data-stu-id="0b00c-257">Retrieve a single entity</span></span>
<span data-ttu-id="0b00c-258">Recupera (obtém) no Azure Cosmos DB completa < 10 ms p99 e ~ 1 ms com p50 em Olá mesma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b00c-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in hello same Azure region.</span></span> <span data-ttu-id="0b00c-259">Você pode adicionar quantos conta tooyour de regiões para leituras de baixa latência e implantar aplicativos tooread da sua região local ("multihomed"), definindo `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="0b00c-259">You can add as many regions tooyour account for low latency reads, and deploy applications tooread from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="0b00c-260">Você pode recuperar uma única entidade utilizando Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b00c-260">You can retrieve a single entity using hello following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="0b00c-261">Saiba mais sobre as APIs de hospedagem múltipla em [Desenvolvendo com várias regiões](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="0b00c-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="0b00c-262">Consultar entidades usando índices secundários automáticos</span><span class="sxs-lookup"><span data-stu-id="0b00c-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="0b00c-263">Tabelas podem ser consultadas usando Olá `TableQuery` classe.</span><span class="sxs-lookup"><span data-stu-id="0b00c-263">Tables can be queried using hello `TableQuery` class.</span></span> <span data-ttu-id="0b00c-264">O Azure Cosmos DB tem um mecanismo de banco de dados otimizado para gravação que indexa automaticamente todas as colunas em sua tabela.</span><span class="sxs-lookup"><span data-stu-id="0b00c-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="0b00c-265">A indexação no banco de dados do Azure Cosmos é tooschema desconhecido.</span><span class="sxs-lookup"><span data-stu-id="0b00c-265">Indexing in Azure Cosmos DB is agnostic tooschema.</span></span> <span data-ttu-id="0b00c-266">Portanto, mesmo que seu esquema é diferente entre as linhas, ou se o esquema Olá evolui ao longo do tempo, ele será indexado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0b00c-266">Therefore, even if your schema is different between rows, or if hello schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="0b00c-267">Como o banco de dados do Azure Cosmos dá suporte a índices secundários automática, consultas em relação a qualquer propriedade podem usar índice hello e ser atendidas com eficiência.</span><span class="sxs-lookup"><span data-stu-id="0b00c-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use hello index and be served efficiently.</span></span>

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

<span data-ttu-id="0b00c-268">Na visualização, o banco de dados do Azure Cosmos dá suporte a saudação mesma funcionalidade como armazenamento de tabela do Azure para Olá API da tabela de consulta.</span><span class="sxs-lookup"><span data-stu-id="0b00c-268">In preview, Azure Cosmos DB supports hello same query functionality as Azure Table storage for hello Table API.</span></span> <span data-ttu-id="0b00c-269">O Azure Cosmos DB também oferece suporte à classificação, agregações, consulta geoespacial, hierarquia e uma ampla variedade de funções internas.</span><span class="sxs-lookup"><span data-stu-id="0b00c-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="0b00c-270">funcionalidade adicional Olá será fornecida em Olá API de tabela em uma atualização futura do serviço.</span><span class="sxs-lookup"><span data-stu-id="0b00c-270">hello additional functionality will be provided in hello Table API in a future service update.</span></span> <span data-ttu-id="0b00c-271">Consulte [Consulta do Azure Cosmos DB](documentdb-sql-query.md) para uma visão geral desses recursos.</span><span class="sxs-lookup"><span data-stu-id="0b00c-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="0b00c-272">Substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="0b00c-272">Replace an entity</span></span>
<span data-ttu-id="0b00c-273">tooupdate uma entidade, recuperá-lo do serviço de tabela hello, modificar o objeto de entidade hello e, em seguida, salvar as alterações de saudação fazer toohello serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="0b00c-273">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="0b00c-274">Olá código a seguir altera o número de telefone de um cliente existente.</span><span class="sxs-lookup"><span data-stu-id="0b00c-274">hello following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="0b00c-275">Da mesma forma, você pode executar as operações `InsertOrMerge` ou `Merge`.</span><span class="sxs-lookup"><span data-stu-id="0b00c-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="0b00c-276">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="0b00c-276">Delete an entity</span></span>
<span data-ttu-id="0b00c-277">Você pode facilmente excluir uma entidade após recuperá-lo usando Olá mesmo padrão mostrado para a atualização de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="0b00c-277">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="0b00c-278">saudação de código a seguir recupera e exclui uma entidade customer.</span><span class="sxs-lookup"><span data-stu-id="0b00c-278">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="0b00c-279">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="0b00c-279">Delete a table</span></span>
<span data-ttu-id="0b00c-280">Por fim, Olá exemplo de código a seguir exclui uma tabela de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0b00c-280">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="0b00c-281">Você pode excluir e recriar uma tabela imediatamente com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0b00c-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="0b00c-282">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="0b00c-282">Clean up resources</span></span> 

<span data-ttu-id="0b00c-283">Se você não vai toocontinue toouse esse aplicativo, use Olá seguindo as etapas toodelete todos os recursos criados por esse tutorial Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b00c-283">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>   

1. <span data-ttu-id="0b00c-284">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="0b00c-284">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span>  
2. <span data-ttu-id="0b00c-285">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="0b00c-285">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0b00c-286">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0b00c-286">Next steps</span></span>

<span data-ttu-id="0b00c-287">Neste tutorial, abordamos como tooget iniciado usando o banco de dados do Azure Cosmos com hello API de tabela e que você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="0b00c-287">In this tutorial, we covered how tooget started using Azure Cosmos DB with hello Table API, and you've done hello following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="0b00c-288">Criou uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0b00c-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="0b00c-289">Funcionalidade habilitada no arquivo App. config de saudação</span><span class="sxs-lookup"><span data-stu-id="0b00c-289">Enabled functionality in hello app.config file</span></span> 
> * <span data-ttu-id="0b00c-290">Criou uma tabela</span><span class="sxs-lookup"><span data-stu-id="0b00c-290">Created a table</span></span> 
> * <span data-ttu-id="0b00c-291">Adicionada a uma tabela de entidade tooa</span><span class="sxs-lookup"><span data-stu-id="0b00c-291">Added an entity tooa table</span></span> 
> * <span data-ttu-id="0b00c-292">Inseriu um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="0b00c-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="0b00c-293">Recuperou uma única entidade</span><span class="sxs-lookup"><span data-stu-id="0b00c-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="0b00c-294">Consultou entidades usando índices secundários automáticos</span><span class="sxs-lookup"><span data-stu-id="0b00c-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="0b00c-295">Substituiu uma entidade</span><span class="sxs-lookup"><span data-stu-id="0b00c-295">Replaced an entity</span></span> 
> * <span data-ttu-id="0b00c-296">Excluiu uma entidade</span><span class="sxs-lookup"><span data-stu-id="0b00c-296">Deleted an entity</span></span> 
> * <span data-ttu-id="0b00c-297">Excluiu uma tabela</span><span class="sxs-lookup"><span data-stu-id="0b00c-297">Deleted a table</span></span>  

<span data-ttu-id="0b00c-298">Agora você pode continuar tutorial próxima toohello e saber mais sobre como consultar dados da tabela.</span><span class="sxs-lookup"><span data-stu-id="0b00c-298">You can now proceed toohello next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="0b00c-299">Consultar com hello API de tabela</span><span class="sxs-lookup"><span data-stu-id="0b00c-299">Query with hello Table API</span></span>](tutorial-query-table.md)
