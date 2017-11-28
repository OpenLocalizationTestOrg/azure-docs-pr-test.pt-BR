---
title: "tutorial de distribuição global aaaAzure Cosmos DB para a API DocumentDB | Microsoft Docs"
description: "Saiba como distribuição global usando o banco de dados do Azure Cosmos toosetup Olá API DocumentDB."
services: cosmos-db
keywords: "distribuição global, documentDB"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a><span data-ttu-id="7f3dd-104">Como a distribuição global usando o banco de dados do Azure Cosmos toosetup Olá API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="7f3dd-104">How toosetup Azure Cosmos DB global distribution using hello DocumentDB API</span></span>

<span data-ttu-id="7f3dd-105">Neste artigo, mostramos como toouse Olá toosetup portal do Azure distribuição global do banco de dados do Azure Cosmos e, em seguida, conecte-se usando Olá API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello DocumentDB API.</span></span>

<span data-ttu-id="7f3dd-106">Este artigo aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f3dd-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="7f3dd-107">Configurar a distribuição global usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7f3dd-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="7f3dd-108">Configurar a distribuição global usando Olá [APIs do DocumentDB](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="7f3dd-108">Configure global distribution using hello [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a><span data-ttu-id="7f3dd-109">Conectar-se a região preferida tooa usando Olá API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="7f3dd-109">Connecting tooa preferred region using hello DocumentDB API</span></span>

<span data-ttu-id="7f3dd-110">Em ordem tootake aproveitar [distribuição global](distribute-data-globally.md), aplicativos cliente podem especificar Olá ordenados lista de preferência de regiões toobe usada tooperform operações de documento.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="7f3dd-111">Isso pode ser feito definindo a diretiva de conexão hello.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-111">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="7f3dd-112">Com base na configuração de conta do banco de dados do Azure Cosmos hello, disponibilidade regional atual e a lista de preferência de saudação especificado, Olá ponto de extremidade mais ideal será escolhido por Olá SDK do DocumentDB tooperform gravar e operações de leitura.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello DocumentDB SDK tooperform write and read operations.</span></span>

<span data-ttu-id="7f3dd-113">Esta lista de preferência é especificada durante a inicialização de uma conexão usando Olá SDKs do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-113">This preference list is specified when initializing a connection using hello DocumentDB SDKs.</span></span> <span data-ttu-id="7f3dd-114">Olá SDKs aceitar um parâmetro opcional "PreferredLocations" que é uma lista ordenada de regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-114">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="7f3dd-115">Olá SDK enviará automaticamente todas as gravações toohello gravação região atual.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-115">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="7f3dd-116">Todas as leituras serão enviadas toohello primeira região disponível na lista de PreferredLocations hello.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-116">All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="7f3dd-117">Se Olá solicitação falhar, o cliente Olá falhar para baixo próxima região do hello lista toohello e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="7f3dd-118">Olá SDKs somente tentará tooread de regiões de saudação especificado em PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-118">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="7f3dd-119">Assim, por exemplo, se Olá conta de banco de dados está disponível em três regiões, mas somente cliente Olá especifica duas regiões de gravação não Olá para PreferredLocations, em seguida, nenhuma leitura será servida fora da região de gravação hello, mesmo no caso de saudação de failover.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="7f3dd-120">aplicativo Hello pode verificar o ponto de extremidade de gravação atual Olá e ler escolhido pelo Olá SDK pela verificação duas propriedades, WriteEndpoint e ReadEndpoint, disponível no SDK versão 1.8 e acima do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-120">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="7f3dd-121">Se Olá PreferredLocations propriedade não for definida, todas as solicitações serão atendidas a partir de região de gravação atual hello.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-121">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="7f3dd-122">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="7f3dd-122">.NET SDK</span></span>
<span data-ttu-id="7f3dd-123">Olá SDK pode ser usado sem quaisquer alterações de código.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-123">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="7f3dd-124">Nesse caso, hello SDK automaticamente ambas as leituras e gravações toohello região de gravação atual.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-124">In this case, hello SDK automatically directs both reads and writes toohello current write region.</span></span>

<span data-ttu-id="7f3dd-125">Na versão 1.8 e mais recente do SDK .NET de hello, o parâmetro de ConnectionPolicy Olá para construtor de DocumentClient Olá tem uma propriedade chamada Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-125">In version 1.8 and later of hello .NET SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="7f3dd-126">Essa propriedade é do tipo `<string>` de Coleção e deve conter uma lista de nomes de região.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="7f3dd-127">valores de cadeia de caracteres de saudação são formatados por coluna de nome de região Olá Olá [regiões do Azure] [ regions] página, sem espaços antes ou depois de saudação primeiro e último caractere respectivamente.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-127">hello string values are formatted per hello Region Name column on hello [Azure Regions][regions] page, with no spaces before or after hello first and last character respectively.</span></span>

<span data-ttu-id="7f3dd-128">pontos de extremidade de leitura e gravação atual Olá estão disponíveis em DocumentClient.WriteEndpoint e DocumentClient.ReadEndpoint respectivamente.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-128">hello current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="7f3dd-129">Olá URLs para pontos de extremidade de saudação não devem ser consideradas como constantes e longa duração.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-129">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="7f3dd-130">serviço de saudação pode atualizar essas a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-130">hello service may update these at any point.</span></span> <span data-ttu-id="7f3dd-131">Olá SDK manipula essa alteração automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-131">hello SDK handles this change automatically.</span></span>
>
>

```csharp
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
  
ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="7f3dd-132">SDKs para NodeJS, JavaScript e Python</span><span class="sxs-lookup"><span data-stu-id="7f3dd-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="7f3dd-133">Olá SDK pode ser usado sem quaisquer alterações de código.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-133">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="7f3dd-134">Nesse caso, Olá que SDK direcionará automaticamente os lê e grava toohello região de gravação atual.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-134">In this case, hello SDK will automatically direct both reads and writes toohello current write region.</span></span>

<span data-ttu-id="7f3dd-135">Na versão 1.8 e mais tarde de cada SDK, Olá ConnectionPolicy parâmetro para o construtor de DocumentClient Olá uma nova propriedade chamada DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-135">In version 1.8 and later of each SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="7f3dd-136">Esse parâmetro é uma matriz de cadeias de caracteres que usa uma lista de nomes de região.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="7f3dd-137">nomes de saudação são formatados por coluna de nome de região de Olá Olá [regiões do Azure] [ regions] página.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-137">hello names are formatted per hello Region Name column in hello [Azure Regions][regions] page.</span></span> <span data-ttu-id="7f3dd-138">Você também pode usar constantes Olá predefinido no objeto de conveniência Olá AzureDocuments.Regions</span><span class="sxs-lookup"><span data-stu-id="7f3dd-138">You can also use hello predefined constants in hello convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="7f3dd-139">pontos de extremidade de leitura e gravação atual Olá estão disponíveis em DocumentClient.getWriteEndpoint e DocumentClient.getReadEndpoint respectivamente.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-139">hello current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="7f3dd-140">Olá URLs para pontos de extremidade de saudação não devem ser consideradas como constantes e longa duração.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-140">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="7f3dd-141">serviço de saudação pode atualizar essas a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-141">hello service may update these at any point.</span></span> <span data-ttu-id="7f3dd-142">Olá SDK tratará essa alteração automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-142">hello SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="7f3dd-143">Veja abaixo um exemplo de código para NodeJS/Javascript.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="7f3dd-144">Python e Java seguirá Olá mesmo padrão.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-144">Python and Java will follow hello same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="7f3dd-145">REST</span><span class="sxs-lookup"><span data-stu-id="7f3dd-145">REST</span></span>
<span data-ttu-id="7f3dd-146">Depois que uma conta de banco de dados tenha sido disponibilizada em várias regiões, os clientes podem consultar sua disponibilidade ao executar uma solicitação GET em Olá URI a seguir.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on hello following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="7f3dd-147">serviço de saudação retornará uma lista de regiões e seu banco de dados do Azure Cosmos ponto de extremidade correspondente URIs para réplicas de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-147">hello service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for hello replicas.</span></span> <span data-ttu-id="7f3dd-148">região de gravação atual Olá será indicado na resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-148">hello current write region will be indicated in hello response.</span></span> <span data-ttu-id="7f3dd-149">cliente Olá pode selecionar ponto de extremidade apropriado para todas as solicitações da API REST Olá da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-149">hello client can then select hello appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="7f3dd-150">Exemplo de resposta</span><span class="sxs-lookup"><span data-stu-id="7f3dd-150">Example response</span></span>

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* <span data-ttu-id="7f3dd-151">PUT, POST e DELETE todas as solicitações devem ir toohello indicado gravar URI</span><span class="sxs-lookup"><span data-stu-id="7f3dd-151">All PUT, POST and DELETE requests must go toohello indicated write URI</span></span>
* <span data-ttu-id="7f3dd-152">Obtém todas as e outras solicitações somente leitura (por exemplo, consultas) podem ir tooany de ponto de extremidade de escolha do cliente Olá</span><span class="sxs-lookup"><span data-stu-id="7f3dd-152">All GETs and other read-only requests (for example queries) may go tooany endpoint of hello client’s choice</span></span>

<span data-ttu-id="7f3dd-153">Grave solicitações regiões de somente tooread falhará com o código de erro HTTP 403 ("proibido").</span><span class="sxs-lookup"><span data-stu-id="7f3dd-153">Write requests tooread-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="7f3dd-154">Se a região de gravação da saudação alterações após a fase de descoberta inicial do cliente hello, subsequente grava toohello anterior região de gravação falhará com o código de erro HTTP 403 ("proibido").</span><span class="sxs-lookup"><span data-stu-id="7f3dd-154">If hello write region changes after hello client’s initial discovery phase, subsequent writes toohello previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="7f3dd-155">cliente Olá deve, em seguida, obter Olá lista de regiões novamente região do tooget Olá gravação atualizado.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-155">hello client should then GET hello list of regions again tooget hello updated write region.</span></span>

<span data-ttu-id="7f3dd-156">Assim, concluímos este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="7f3dd-157">Você pode aprender como toomanage Olá consistência da sua conta global replicada lendo [níveis de consistência no banco de dados do Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="7f3dd-157">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="7f3dd-158">E para saber mais sobre como a replicação de banco de dados global funciona no Azure Cosmos DB, veja [Distribuir dados globalmente com o Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="7f3dd-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f3dd-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7f3dd-159">Next steps</span></span>

<span data-ttu-id="7f3dd-160">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="7f3dd-160">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7f3dd-161">Configurar a distribuição global usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7f3dd-161">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="7f3dd-162">Configurar a distribuição global usando Olá APIs do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="7f3dd-162">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="7f3dd-163">Você pode continuar toolearn tutorial do próximo toohello como toodevelop localmente usando Olá emulador local do banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-163">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f3dd-164">Desenvolva localmente com o emulador de saudação</span><span class="sxs-lookup"><span data-stu-id="7f3dd-164">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

