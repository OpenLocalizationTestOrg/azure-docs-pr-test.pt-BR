---
title: "Tutorial de distribuição global do Azure Cosmos DB para a API do DocumentDB | Microsoft Docs"
description: "Saiba como configurar a distribuição global do Azure Cosmos DB usando a API do DocumentDB."
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
ms.openlocfilehash: f4d8efe9814bd28bb902567a23b541bc9b5414a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-documentdb-api"></a><span data-ttu-id="dd924-104">Como configurar a distribuição global do Azure Cosmos DB usando a API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="dd924-104">How to setup Azure Cosmos DB global distribution using the DocumentDB API</span></span>

<span data-ttu-id="dd924-105">Neste artigo, mostraremos como usar o Portal do Azure para configurar a distribuição global do Azure Cosmos DB e, depois, conectar-se usando a API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="dd924-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the DocumentDB API.</span></span>

<span data-ttu-id="dd924-106">Este artigo aborda as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="dd924-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="dd924-107">Configurar a distribuição global usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dd924-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="dd924-108">Configurar a distribuição global usando a [API do DocumentDB](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="dd924-108">Configure global distribution using the [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-documentdb-api"></a><span data-ttu-id="dd924-109">Conectar-se a uma região preferencial usando a API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="dd924-109">Connecting to a preferred region using the DocumentDB API</span></span>

<span data-ttu-id="dd924-110">Para aproveitar a [distribuição global](distribute-data-globally.md), os aplicativos cliente podem especificar a lista de preferências ordenadas de regiões a serem usadas para executar operações de documento.</span><span class="sxs-lookup"><span data-stu-id="dd924-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="dd924-111">Isso pode ser feito definindo a política de conexão.</span><span class="sxs-lookup"><span data-stu-id="dd924-111">This can be done by setting the connection policy.</span></span> <span data-ttu-id="dd924-112">Com base na configuração da conta do Azure Cosmos DB, na disponibilidade regional atual e na lista de preferências especificada, o ponto de extremidade mais adequado será escolhido pelo SDK do DocumentDB para executar operações de gravação e leitura.</span><span class="sxs-lookup"><span data-stu-id="dd924-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the DocumentDB SDK to perform write and read operations.</span></span>

<span data-ttu-id="dd924-113">Essa lista de preferências é especificada ao inicializar uma conexão usando os SDKs do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="dd924-113">This preference list is specified when initializing a connection using the DocumentDB SDKs.</span></span> <span data-ttu-id="dd924-114">Os SDKs aceitam um parâmetro opcional "PreferredLocations", que é uma lista ordenada de regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd924-114">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="dd924-115">O SDK enviará automaticamente todas as gravações para a região de gravação atual.</span><span class="sxs-lookup"><span data-stu-id="dd924-115">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="dd924-116">Todas as leituras serão enviadas para a primeira região disponível na lista PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="dd924-116">All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="dd924-117">Se a solicitação falhar, o cliente não fará o envio para a próxima região da lista, e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="dd924-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="dd924-118">Os SDKs tentarão ler apenas das regiões especificadas em PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="dd924-118">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="dd924-119">Desse modo, se a Conta do Banco de Dados estiver disponível em três regiões, por exemplo, mas o cliente especificar apenas duas das regiões de não gravação para PreferredLocations, nenhuma leitura será atendida fora da região de gravação, mesmo no caso de failover.</span><span class="sxs-lookup"><span data-stu-id="dd924-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="dd924-120">O aplicativo pode verificar o ponto de extremidade de gravação e o ponto de extremidade de leitura atuais escolhidos pelo SDK marcando duas propriedades, WriteEndpoint e ReadEndpoint, disponíveis no SDK versão 1.8 e superiores.</span><span class="sxs-lookup"><span data-stu-id="dd924-120">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="dd924-121">Se a propriedade PreferredLocations não estiver definida, todas as solicitações serão atendidas na região de gravação atual.</span><span class="sxs-lookup"><span data-stu-id="dd924-121">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="dd924-122">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="dd924-122">.NET SDK</span></span>
<span data-ttu-id="dd924-123">O SDK pode ser usado sem qualquer mudança de código.</span><span class="sxs-lookup"><span data-stu-id="dd924-123">The SDK can be used without any code changes.</span></span> <span data-ttu-id="dd924-124">Nesse caso, o SDK direciona automaticamente as leituras e gravações para a região de gravação atual.</span><span class="sxs-lookup"><span data-stu-id="dd924-124">In this case, the SDK automatically directs both reads and writes to the current write region.</span></span>

<span data-ttu-id="dd924-125">Na versão 1.8 e posteriores do SDK para .NET, o parâmetro ConnectionPolicy do construtor DocumentClient tem uma propriedade chamada Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="dd924-125">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="dd924-126">Essa propriedade é do tipo `<string>` de Coleção e deve conter uma lista de nomes de região.</span><span class="sxs-lookup"><span data-stu-id="dd924-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="dd924-127">Os valores de cadeia de caracteres são formatados de acordo com a coluna Nome da Região na página [Regiões do Azure][regions], sem espaços antes ou depois do primeiro e último caracteres, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="dd924-127">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span></span>

<span data-ttu-id="dd924-128">Os pontos de extremidade atuais de gravação e leitura estão disponíveis em DocumentClient.WriteEndpoint e DocumentClient.ReadEndpoint, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="dd924-128">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="dd924-129">As URLs para os pontos de extremidade não devem ser consideradas como constantes de vida longa.</span><span class="sxs-lookup"><span data-stu-id="dd924-129">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="dd924-130">O serviço pode atualizá-las a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="dd924-130">The service may update these at any point.</span></span> <span data-ttu-id="dd924-131">O SDK lida com essa alteração automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dd924-131">The SDK handles this change automatically.</span></span>
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

// connect to DocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="dd924-132">SDKs para NodeJS, JavaScript e Python</span><span class="sxs-lookup"><span data-stu-id="dd924-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="dd924-133">O SDK pode ser usado sem qualquer mudança de código.</span><span class="sxs-lookup"><span data-stu-id="dd924-133">The SDK can be used without any code changes.</span></span> <span data-ttu-id="dd924-134">Nesse caso, o SDK direcionará automaticamente as leituras e gravações para a região de gravação atual.</span><span class="sxs-lookup"><span data-stu-id="dd924-134">In this case, the SDK will automatically direct both reads and writes to the current write region.</span></span>

<span data-ttu-id="dd924-135">Na versão 1.8 e posteriores de cada SDK, o parâmetro ConnectionPolicy do construtor DocumentClient tem uma nova propriedade chamada DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="dd924-135">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="dd924-136">Esse parâmetro é uma matriz de cadeias de caracteres que usa uma lista de nomes de região.</span><span class="sxs-lookup"><span data-stu-id="dd924-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="dd924-137">Os nomes são formatados de acordo com a coluna Nome da Região na página [Regiões do Azure][regions].</span><span class="sxs-lookup"><span data-stu-id="dd924-137">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span></span> <span data-ttu-id="dd924-138">Você também pode usar as constantes predefinidas no objeto de conveniência AzureDocuments.Regions</span><span class="sxs-lookup"><span data-stu-id="dd924-138">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="dd924-139">Os pontos de extremidade atuais de gravação e leitura estão disponíveis em DocumentClient.getWriteEndpoint e DocumentClient.getReadEndpoint, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="dd924-139">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="dd924-140">As URLs para os pontos de extremidade não devem ser consideradas como constantes de vida longa.</span><span class="sxs-lookup"><span data-stu-id="dd924-140">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="dd924-141">O serviço pode atualizá-las a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="dd924-141">The service may update these at any point.</span></span> <span data-ttu-id="dd924-142">O SDK tratará dessa mudança automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dd924-142">The SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="dd924-143">Veja abaixo um exemplo de código para NodeJS/Javascript.</span><span class="sxs-lookup"><span data-stu-id="dd924-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="dd924-144">Python e Java seguirão o mesmo padrão.</span><span class="sxs-lookup"><span data-stu-id="dd924-144">Python and Java will follow the same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in the following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize the connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="dd924-145">REST</span><span class="sxs-lookup"><span data-stu-id="dd924-145">REST</span></span>
<span data-ttu-id="dd924-146">Assim que uma conta de banco de dados tiver sido disponibilizada em várias regiões, os clientes poderão consultar sua disponibilidade executando uma solicitação GET no URI a seguir.</span><span class="sxs-lookup"><span data-stu-id="dd924-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="dd924-147">O serviço retornará uma lista de regiões e seus URIs de pontos de extremidade do Azure Cosmos DB correspondentes para as réplicas.</span><span class="sxs-lookup"><span data-stu-id="dd924-147">The service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for the replicas.</span></span> <span data-ttu-id="dd924-148">A região de gravação atual será indicada na resposta.</span><span class="sxs-lookup"><span data-stu-id="dd924-148">The current write region will be indicated in the response.</span></span> <span data-ttu-id="dd924-149">O cliente pode selecionar o ponto de extremidade apropriado para todas as solicitações adicionais de API REST como se segue.</span><span class="sxs-lookup"><span data-stu-id="dd924-149">The client can then select the appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="dd924-150">Exemplo de resposta</span><span class="sxs-lookup"><span data-stu-id="dd924-150">Example response</span></span>

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


* <span data-ttu-id="dd924-151">Todas as solicitações All PUT, POST e DELETE devem ir para o URI de gravação indicado</span><span class="sxs-lookup"><span data-stu-id="dd924-151">All PUT, POST and DELETE requests must go to the indicated write URI</span></span>
* <span data-ttu-id="dd924-152">Todas as solicitações GET e outras somente leitura (por exemplo: consultas) podem ir para qualquer ponto de extremidade de escolha do cliente</span><span class="sxs-lookup"><span data-stu-id="dd924-152">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span></span>

<span data-ttu-id="dd924-153">As solicitações de gravação para regiões somente leitura falharão com o código de erro 403 de HTTP ("Proibido").</span><span class="sxs-lookup"><span data-stu-id="dd924-153">Write requests to read-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="dd924-154">Se a região de gravação mudar depois da fase de descoberta inicial do cliente, as gravações subsequentes na região de gravação anterior falharão com o código de erro 403 de HTTP ("Proibido").</span><span class="sxs-lookup"><span data-stu-id="dd924-154">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="dd924-155">O cliente deve obter (GET) a lista de regiões novamente para que a região de gravação seja atualizada.</span><span class="sxs-lookup"><span data-stu-id="dd924-155">The client should then GET the list of regions again to get the updated write region.</span></span>

<span data-ttu-id="dd924-156">Assim, concluímos este tutorial.</span><span class="sxs-lookup"><span data-stu-id="dd924-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="dd924-157">Aprenda a gerenciar a consistência de sua conta globalmente replicada lendo [Níveis de consistência no Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="dd924-157">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="dd924-158">E para saber mais sobre como a replicação de banco de dados global funciona no Azure Cosmos DB, veja [Distribuir dados globalmente com o Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="dd924-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd924-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd924-159">Next steps</span></span>

<span data-ttu-id="dd924-160">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="dd924-160">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dd924-161">Configurar a distribuição global usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dd924-161">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="dd924-162">Configurar a distribuição global usando a API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="dd924-162">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="dd924-163">Agora você pode prosseguir para o próximo tutorial e aprender a desenvolver localmente usando o emulador local do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dd924-163">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dd924-164">Desenvolver localmente com o emulador</span><span class="sxs-lookup"><span data-stu-id="dd924-164">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

