---
title: "Como usar o SDK para iOS para os Aplicativos Móveis do Azure"
description: "Como usar o SDK para iOS para os Aplicativos Móveis do Azure"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: 65817208e1b26fb5f9eb56d164f48b44d57dce56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="e52d0-103">Como usar a Biblioteca de Cliente iOS para os Aplicativos Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="e52d0-103">How to Use iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="e52d0-104">Este guia ensina a executar cenários comuns usando o mais recente [SDK de Aplicativos Móveis do Azure para iOS][1].</span><span class="sxs-lookup"><span data-stu-id="e52d0-104">This guide teaches you to perform common scenarios using the latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="e52d0-105">Se você for novo nos Aplicativos Móveis do Azure, primeiro conclua o [Início Rápido dos Aplicativos Móveis do Azure] para criar um back-end, criar uma tabela e baixar um projeto Xcode iOS pré-criado.</span><span class="sxs-lookup"><span data-stu-id="e52d0-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="e52d0-106">Neste guia, abordaremos o SDK para iOS do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="e52d0-106">In this guide, we focus on the client-side iOS SDK.</span></span> <span data-ttu-id="e52d0-107">Para saber mais sobre o SDK do lado do servidor para o back-end, confira os TUTORIAIS do SDK do Servidor.</span><span class="sxs-lookup"><span data-stu-id="e52d0-107">To learn more about the server-side SDK for the backend, see the Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="e52d0-108">Documentação de referência</span><span class="sxs-lookup"><span data-stu-id="e52d0-108">Reference documentation</span></span>
<span data-ttu-id="e52d0-109">A documentação de referência para o SDK do cliente do iOS está aqui: [Referência de cliente do iOS de Aplicativos Móveis do Azure][2].</span><span class="sxs-lookup"><span data-stu-id="e52d0-109">The reference documentation for the iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="e52d0-110">Plataformas com suporte</span><span class="sxs-lookup"><span data-stu-id="e52d0-110">Supported Platforms</span></span>
<span data-ttu-id="e52d0-111">O SDK do iOS dá suporte a projetos de Objective-C, Swift 2.2 e projetos Swift 2.3 para iOS na versão 8.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e52d0-111">The iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="e52d0-112">A autenticação de "fluxo de servidor" usa um modo de exibição da Web para a interface do usuário apresentada.</span><span class="sxs-lookup"><span data-stu-id="e52d0-112">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="e52d0-113">Se o dispositivo não for capaz de apresentar uma interface do usuário para modo de exibição da Web, será necessário outro método de autenticação fora do escopo do produto.</span><span class="sxs-lookup"><span data-stu-id="e52d0-113">If the device is not able to present a WebView UI, then another method of authentication is required that is outside the scope of the product.</span></span>  
<span data-ttu-id="e52d0-114">Esse SDK, portanto, não é adequado para relógios ou dispositivos similarmente restritos.</span><span class="sxs-lookup"><span data-stu-id="e52d0-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="e52d0-115"><a name="Setup"></a>Configuração e Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e52d0-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="e52d0-116">Este guia pressupõe que você tenha criado um back-end com uma tabela.</span><span class="sxs-lookup"><span data-stu-id="e52d0-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="e52d0-117">Este guia pressupõe que a tabela tem o mesmo esquema das tabelas desses tutoriais.</span><span class="sxs-lookup"><span data-stu-id="e52d0-117">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="e52d0-118">Este guia também pressupõe que em seu código, você referencia `MicrosoftAzureMobile.framework` e importa `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="e52d0-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="e52d0-119"><a name="create-client"></a>Como: criar o cliente</span><span class="sxs-lookup"><span data-stu-id="e52d0-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="e52d0-120">Para acessar um back-end de Aplicativos Móveis do Azure em seu projeto, crie um `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="e52d0-120">To access an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="e52d0-121">Substitua `AppUrl` pela URL do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e52d0-121">Replace `AppUrl` with the app URL.</span></span> <span data-ttu-id="e52d0-122">Você pode deixar `gatewayURLString` e `applicationKey` vazios.</span><span class="sxs-lookup"><span data-stu-id="e52d0-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="e52d0-123">Se você configurar um gateway para autenticação, preencha `gatewayURLString` com a URL do gateway.</span><span class="sxs-lookup"><span data-stu-id="e52d0-123">If you set up a gateway for authentication, populate `gatewayURLString` with the gateway URL.</span></span>

<span data-ttu-id="e52d0-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="e52d0-125">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="e52d0-126"><a name="table-reference"></a>Como criar uma referência de tabela</span><span class="sxs-lookup"><span data-stu-id="e52d0-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="e52d0-127">Para acessar ou atualizar dados, crie uma referência à tabela de back-end.</span><span class="sxs-lookup"><span data-stu-id="e52d0-127">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="e52d0-128">Substitua `TodoItem` pelo nome da sua tabela</span><span class="sxs-lookup"><span data-stu-id="e52d0-128">Replace `TodoItem` with the name of your table</span></span>

<span data-ttu-id="e52d0-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="e52d0-130">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="e52d0-131"><a name="querying"></a>Como consultar dados</span><span class="sxs-lookup"><span data-stu-id="e52d0-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="e52d0-132">Para criar uma consulta de banco de dados, consulte o objeto `MSTable` .</span><span class="sxs-lookup"><span data-stu-id="e52d0-132">To create a database query, query the `MSTable` object.</span></span> <span data-ttu-id="e52d0-133">A consulta a seguir obtém todos os itens em `TodoItem` e registra o texto de cada item.</span><span class="sxs-lookup"><span data-stu-id="e52d0-133">The following query gets all the items in `TodoItem` and logs the text of each item.</span></span>

<span data-ttu-id="e52d0-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-134">**Objective-C**:</span></span>

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="e52d0-135">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-135">**Swift**:</span></span>

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="e52d0-136"><a name="filtering"></a>Como filtrar dados retornados</span><span class="sxs-lookup"><span data-stu-id="e52d0-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="e52d0-137">Para filtrar os resultados, há muitas opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e52d0-137">To filter results, there are many available options.</span></span>

<span data-ttu-id="e52d0-138">Para filtrar usando um predicado, use `NSPredicate` e `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="e52d0-138">To filter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="e52d0-139">Os filtros a seguir retornaram dados para localizar apenas os itens pendentes não concluídos.</span><span class="sxs-lookup"><span data-stu-id="e52d0-139">The following filters returned data to find only incomplete Todo items.</span></span>

<span data-ttu-id="e52d0-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query the TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="e52d0-141">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query the TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="e52d0-142"><a name="query-object"></a>Como usar o MSQuery</span><span class="sxs-lookup"><span data-stu-id="e52d0-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="e52d0-143">Para executar uma consulta complexa (incluindo classificação e paginação), crie um objeto de `MSQuery` diretamente ou usando um predicado:</span><span class="sxs-lookup"><span data-stu-id="e52d0-143">To perform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="e52d0-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="e52d0-145">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="e52d0-146">`MSQuery` permite que você controle vários comportamentos de consulta.</span><span class="sxs-lookup"><span data-stu-id="e52d0-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="e52d0-147">Especificar a ordem dos resultados</span><span class="sxs-lookup"><span data-stu-id="e52d0-147">Specify order of results</span></span>
* <span data-ttu-id="e52d0-148">Limitar quais campos retornar</span><span class="sxs-lookup"><span data-stu-id="e52d0-148">Limit which fields to return</span></span>
* <span data-ttu-id="e52d0-149">Limitar quantos registros retornar</span><span class="sxs-lookup"><span data-stu-id="e52d0-149">Limit how many records to return</span></span>
* <span data-ttu-id="e52d0-150">Especificar contagem total na resposta</span><span class="sxs-lookup"><span data-stu-id="e52d0-150">Specify total count in response</span></span>
* <span data-ttu-id="e52d0-151">Especificar parâmetros de cadeia de consulta personalizada na solicitação</span><span class="sxs-lookup"><span data-stu-id="e52d0-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="e52d0-152">Aplicar funções adicionais</span><span class="sxs-lookup"><span data-stu-id="e52d0-152">Apply additional functions</span></span>

<span data-ttu-id="e52d0-153">Executar uma consulta `MSQuery` chamando `readWithCompletion` no objeto.</span><span class="sxs-lookup"><span data-stu-id="e52d0-153">Execute an `MSQuery` query by calling `readWithCompletion` on the object.</span></span>

## <span data-ttu-id="e52d0-154"><a name="sorting"></a>Como classificar dados com MSQuery</span><span class="sxs-lookup"><span data-stu-id="e52d0-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="e52d0-155">Para classificar os resultados, vamos examinar um exemplo.</span><span class="sxs-lookup"><span data-stu-id="e52d0-155">To sort results, let's look at an example.</span></span> <span data-ttu-id="e52d0-156">Para classificar por 'texto' de campo em ordem crescente e 'concluído' em ordem decrescente, invoque `MSQuery` desta forma:</span><span class="sxs-lookup"><span data-stu-id="e52d0-156">To sort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="e52d0-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-157">**Objective-C**:</span></span>

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="e52d0-158">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-158">**Swift**:</span></span>

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <span data-ttu-id="e52d0-159"><a name="selecting"></a><a name="parameters"></a>Como limitar campos e expandir os parâmetros de cadeia de caracteres de consulta com MSQuery</span><span class="sxs-lookup"><span data-stu-id="e52d0-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="e52d0-160">Para limitar os campos a serem retornados em uma consulta, especifique os nomes dos campos na propriedade **selectFields** .</span><span class="sxs-lookup"><span data-stu-id="e52d0-160">To limit fields to be returned in a query, specify the names of the fields in the **selectFields** property.</span></span> <span data-ttu-id="e52d0-161">Esse exemplo retorna somente o texto e os campos preenchidos:</span><span class="sxs-lookup"><span data-stu-id="e52d0-161">This example returns only the text and completed fields:</span></span>

<span data-ttu-id="e52d0-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="e52d0-163">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="e52d0-164">Para incluir parâmetros de cadeia de caracteres de consulta adicionais na solicitação do servidor (por exemplo, porque é usado por um script personalizado do lado do servidor), popule `query.parameters` desta forma:</span><span class="sxs-lookup"><span data-stu-id="e52d0-164">To include additional query string parameters in the server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="e52d0-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="e52d0-166">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="e52d0-167"><a name="paging"></a>Como: Configurar o tamanho de página</span><span class="sxs-lookup"><span data-stu-id="e52d0-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="e52d0-168">Com os Aplicativos Móveis do Azure, o tamanho da página controla o número de registros que são extraídos de uma só vez das tabelas do back-end.</span><span class="sxs-lookup"><span data-stu-id="e52d0-168">With Azure Mobile Apps, the page size controls the number of records that are pulled at a time from the backend tables.</span></span> <span data-ttu-id="e52d0-169">Uma chamada para dados `pull`, em seguida, criaria um lote de dados, com base no tamanho de página, até que não haja mais registros para efetuar pull.</span><span class="sxs-lookup"><span data-stu-id="e52d0-169">A call to `pull` data would then batch up data, based on this page size, until there are no more records to pull.</span></span>

<span data-ttu-id="e52d0-170">É possível configurar um tamanho de página usando **MSPullSettings** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e52d0-170">It's possible to configure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="e52d0-171">O tamanho de página padrão é 50, e o exemplo a seguir é alterado para 3.</span><span class="sxs-lookup"><span data-stu-id="e52d0-171">The default page size is 50, and the example below changes it to 3.</span></span>

<span data-ttu-id="e52d0-172">Você pode configurar um tamanho de página diferente por motivos de desempenho.</span><span class="sxs-lookup"><span data-stu-id="e52d0-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="e52d0-173">Se você tiver um grande número de registros de dados pequenos, um tamanho de página alto reduz o número de viagens de ida e volta do servidor.</span><span class="sxs-lookup"><span data-stu-id="e52d0-173">If you have a large number of small data records, a high page size reduces the number of server round-trips.</span></span>

<span data-ttu-id="e52d0-174">Essa configuração controla somente o tamanho da página no lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="e52d0-174">This setting controls only the page size on the client side.</span></span> <span data-ttu-id="e52d0-175">Se o cliente solicita um tamanho de página maior que o suporte oferecido pelo back-end de Aplicativos Móveis, o tamanho da página está limitado ao máximo que o back-end está configurado para suportar.</span><span class="sxs-lookup"><span data-stu-id="e52d0-175">If the client asks for a larger page size than the Mobile Apps backend supports, the page size is capped at the maximum the backend is configured to support.</span></span>

<span data-ttu-id="e52d0-176">Essa configuração também é o *número* de registros de dados, não o *tamanho em bytes*.</span><span class="sxs-lookup"><span data-stu-id="e52d0-176">This setting is also the *number* of data records, not the *byte size*.</span></span>

<span data-ttu-id="e52d0-177">Se você aumentar o tamanho de página de cliente, também deverá aumentar o tamanho de página no servidor.</span><span class="sxs-lookup"><span data-stu-id="e52d0-177">If you increase the client page size, you should also increase the page size on the server.</span></span> <span data-ttu-id="e52d0-178">Consulte ["Como ajustar o tamanho de paginação da tabela"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para conhecer as etapas para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="e52d0-178">See ["How to: Adjust the table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for the steps to do this.</span></span>

<span data-ttu-id="e52d0-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="e52d0-180">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="e52d0-181"><a name="inserting"></a>Como inserir dados</span><span class="sxs-lookup"><span data-stu-id="e52d0-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="e52d0-182">Para inserir uma nova linha na tabela, crie um `NSDictionary` e invoque `table insert`.</span><span class="sxs-lookup"><span data-stu-id="e52d0-182">To insert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="e52d0-183">Se [Esquema Dinâmico] está habilitado, o back-end móvel do Serviço de Aplicativo do Azure gera novas colunas automaticamente com base no `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="e52d0-183">If [Dynamic Schema] is enabled, the Azure App Service mobile backend automatically generates new columns based on the `NSDictionary`.</span></span>

<span data-ttu-id="e52d0-184">Se não for fornecida uma `id` , o back-end gera automaticamente uma ID exclusiva.</span><span class="sxs-lookup"><span data-stu-id="e52d0-184">If `id` is not provided, the backend automatically generates a new unique ID.</span></span> <span data-ttu-id="e52d0-185">Forneça sua própria `id` para usar endereços de email, nomes de usuários, ou seus próprios valores personalizados como ID.</span><span class="sxs-lookup"><span data-stu-id="e52d0-185">Provide your own `id` to use email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="e52d0-186">Fornecer sua própria identificação pode facilitar junções e lógicas de banco de dados comerciais.</span><span class="sxs-lookup"><span data-stu-id="e52d0-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="e52d0-187">O `result` contém o novo item que foi inserido.</span><span class="sxs-lookup"><span data-stu-id="e52d0-187">The `result` contains the new item that was inserted.</span></span> <span data-ttu-id="e52d0-188">Dependendo de sua lógica de servidor, ele pode ter dados adicionais ou modificados em comparação com o que foi passado para o servidor.</span><span class="sxs-lookup"><span data-stu-id="e52d0-188">Depending on your server logic, it may have additional or modified data compared to what was passed to the server.</span></span>

<span data-ttu-id="e52d0-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-189">**Objective-C**:</span></span>

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="e52d0-190">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-190">**Swift**:</span></span>

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <span data-ttu-id="e52d0-191"><a name="modifying"></a>Como modificar dados</span><span class="sxs-lookup"><span data-stu-id="e52d0-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="e52d0-192">Para atualizar uma linha existente, modifique um item e chame `update`:</span><span class="sxs-lookup"><span data-stu-id="e52d0-192">To update an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="e52d0-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-193">**Objective-C**:</span></span>

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="e52d0-194">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-194">**Swift**:</span></span>

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

<span data-ttu-id="e52d0-195">Como alternativa, forneça a ID da linha e o campo atualizado:</span><span class="sxs-lookup"><span data-stu-id="e52d0-195">Alternatively, supply the row ID and the updated field:</span></span>

<span data-ttu-id="e52d0-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="e52d0-197">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="e52d0-198">No mínimo, o atributo `id` deve ser definido quando você faz atualizações.</span><span class="sxs-lookup"><span data-stu-id="e52d0-198">At minimum, the `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="e52d0-199"><a name="deleting"></a>Como excluir dados</span><span class="sxs-lookup"><span data-stu-id="e52d0-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="e52d0-200">Para excluir um item, invoque `delete` com o item:</span><span class="sxs-lookup"><span data-stu-id="e52d0-200">To delete an item, invoke `delete` with the item:</span></span>

<span data-ttu-id="e52d0-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="e52d0-202">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="e52d0-203">Como alternativa, exclua fornecendo uma ID de linha:</span><span class="sxs-lookup"><span data-stu-id="e52d0-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="e52d0-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="e52d0-205">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="e52d0-206">No mínimo, o atributo `id` deve ser definido quando você faz exclusões.</span><span class="sxs-lookup"><span data-stu-id="e52d0-206">At minimum, the `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="e52d0-207"><a name="customapi"></a>Como chamar uma API personalizada</span><span class="sxs-lookup"><span data-stu-id="e52d0-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="e52d0-208">Com uma API personalizada, você pode expor qualquer funcionalidade de back-end.</span><span class="sxs-lookup"><span data-stu-id="e52d0-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="e52d0-209">Ele não precisa mapear para uma operação de tabela.</span><span class="sxs-lookup"><span data-stu-id="e52d0-209">It doesn't have to map to a table operation.</span></span> <span data-ttu-id="e52d0-210">Não só você obtém mais controle sobre mensagens, mas pode até mesmo ler/definir os cabeçalhos e alterar o formato do corpo da resposta.</span><span class="sxs-lookup"><span data-stu-id="e52d0-210">Not only do you gain more control over messaging, you can even read/set headers and change the response body format.</span></span> <span data-ttu-id="e52d0-211">Para saber como criar uma API personalizada no back-end, leia [APIs personalizadas](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="e52d0-211">To learn how to create a custom API on the backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="e52d0-212">Para chamar uma API personalizada, chame `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="e52d0-212">To call a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="e52d0-213">O conteúdo de solicitação e resposta de conteúdo é tratado como JSON.</span><span class="sxs-lookup"><span data-stu-id="e52d0-213">The request and response content are treated as JSON.</span></span> <span data-ttu-id="e52d0-214">Para usar outros tipos de mídia, [use a outra sobrecarga de `invokeAPI`][5].</span><span class="sxs-lookup"><span data-stu-id="e52d0-214">To use other media types, [use the other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="e52d0-215">Para fazer uma solicitação `GET` em vez de uma solicitação `POST`, defina o parâmetro de `HTTPMethod` como `"GET"` e o parâmetro `body` como `nil` (já que as solicitações GET não têm corpos de mensagem). Se sua API personalizada dá suporte a outros verbos HTTP, altere o `HTTPMethod` adequadamente.</span><span class="sxs-lookup"><span data-stu-id="e52d0-215">To make a `GET` request instead of a `POST` request, set parameter `HTTPMethod` to `"GET"` and parameter `body` to `nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="e52d0-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-216">**Objective-C**:</span></span>

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

<span data-ttu-id="e52d0-217">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-217">**Swift**:</span></span>

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <span data-ttu-id="e52d0-218"><a name="templates"></a>Como registrar modelos de envio por push para enviar notificações entre plataformas</span><span class="sxs-lookup"><span data-stu-id="e52d0-218"><a name="templates"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="e52d0-219">Para registrar os modelos, passe modelos com o método **client.push registerDeviceToken** no seu aplicativo de cliente.</span><span class="sxs-lookup"><span data-stu-id="e52d0-219">To register templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="e52d0-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="e52d0-221">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="e52d0-222">Seus modelos são do tipo NSDictionary e podem conter vários modelos no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="e52d0-222">Your templates are of type NSDictionary and can contain multiple templates in the following format:</span></span>

<span data-ttu-id="e52d0-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="e52d0-224">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="e52d0-225">Todas as marcações são eliminadas da solicitação de segurança.</span><span class="sxs-lookup"><span data-stu-id="e52d0-225">All tags are stripped from the request for security.</span></span>  <span data-ttu-id="e52d0-226">Para adicionar marcas a instalações ou modelos dentro de instalações, confira [Trabalhar com o SDK do servidor de back-end do .NET para Aplicativos Móveis do Azure][4].</span><span class="sxs-lookup"><span data-stu-id="e52d0-226">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="e52d0-227">Para enviar notificações usando esses modelos registrados, trabalhe com [APIs de Hubs de Notificação][3].</span><span class="sxs-lookup"><span data-stu-id="e52d0-227">To send notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="e52d0-228"><a name="errors"></a>Como tratar erros</span><span class="sxs-lookup"><span data-stu-id="e52d0-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="e52d0-229">Quando você chama um back-end móvel do Serviço de Aplicativo do Azure, o bloco de conclusão contém um parâmetro `NSError` .</span><span class="sxs-lookup"><span data-stu-id="e52d0-229">When you call an Azure App Service mobile backend, the completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="e52d0-230">Quando ocorre um erro, esse parâmetro é não nulo.</span><span class="sxs-lookup"><span data-stu-id="e52d0-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="e52d0-231">No seu código, você deve marcar esse parâmetro e tratar o erro conforme necessário, conforme demonstrado nos trechos de código anteriores.</span><span class="sxs-lookup"><span data-stu-id="e52d0-231">In your code, you should check this parameter and handle the error as needed, as demonstrated in the preceding code snippets.</span></span>

<span data-ttu-id="e52d0-232">O arquivo [`<WindowsAzureMobileServices/MSError.h>`][6] define as constantes `MSErrorResponseKey`, `MSErrorRequestKey` e `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="e52d0-232">The file [`<WindowsAzureMobileServices/MSError.h>`][6] defines the constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="e52d0-233">Para obter mais dados relacionados ao erro:</span><span class="sxs-lookup"><span data-stu-id="e52d0-233">To get more data related to the error:</span></span>

<span data-ttu-id="e52d0-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="e52d0-235">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="e52d0-236">Além disso, o arquivo define constantes para cada código de erro:</span><span class="sxs-lookup"><span data-stu-id="e52d0-236">In addition, the file defines constants for each error code:</span></span>

<span data-ttu-id="e52d0-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="e52d0-238">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="e52d0-239"><a name="adal"></a>Como autenticar usuários com a Biblioteca de Autenticação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="e52d0-239"><a name="adal"></a>How to: Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="e52d0-240">Você pode usar a ADAL (Biblioteca de autenticação do Active Directory) para conectar os usuários ao seu aplicativo usando o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="e52d0-240">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="e52d0-241">É melhor usar a autenticação de fluxo de cliente usando SDK do provedor de identidade do que usar o método `loginWithProvider:completion:` .</span><span class="sxs-lookup"><span data-stu-id="e52d0-241">Client flow authentication using an identity provider SDK is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="e52d0-242">Autenticação de fluxo de cliente fornece uma aparência mais nativa do UX e permite uma maior personalização.</span><span class="sxs-lookup"><span data-stu-id="e52d0-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="e52d0-243">Configure o seu back-end de aplicativo móvel para entrada no AAD seguindo o tutorial [Como configurar o Serviço de Aplicativo para logon no Active Directory][7].</span><span class="sxs-lookup"><span data-stu-id="e52d0-243">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="e52d0-244">Complete a etapa opcional de registrar um aplicativo cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="e52d0-244">Make sure to complete the optional step of registering a native client application.</span></span> <span data-ttu-id="e52d0-245">Para iOS, recomendamos que o URI de redirecionamento tenha o formato `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="e52d0-245">For iOS, we recommend that the redirect URI is of the form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="e52d0-246">Para saber mais, confira o [Início rápido da ADAL para iOS][8].</span><span class="sxs-lookup"><span data-stu-id="e52d0-246">For more information, see the [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="e52d0-247">Instale o ADAL usando o Cocoapods.</span><span class="sxs-lookup"><span data-stu-id="e52d0-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="e52d0-248">Edite o Podfile para incluir a seguinte definição, substituindo **YOUR-PROJECT** pelo nome de seu projeto do Xcode:</span><span class="sxs-lookup"><span data-stu-id="e52d0-248">Edit your Podfile to include the following definition, replacing **YOUR-PROJECT** with the name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="e52d0-249">e o Pod:</span><span class="sxs-lookup"><span data-stu-id="e52d0-249">and the Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="e52d0-250">Usando o Terminal, execute `pod install` no diretório que contém o projeto e abra o espaço de trabalho do Xcode gerado (não o projeto).</span><span class="sxs-lookup"><span data-stu-id="e52d0-250">Using the Terminal, run `pod install` from the directory containing your project, and then open the generated Xcode workspace (not the project).</span></span>
4. <span data-ttu-id="e52d0-251">Adicione o código a seguir ao seu aplicativo, de acordo com a linguagem que você está usando.</span><span class="sxs-lookup"><span data-stu-id="e52d0-251">Add the following code to your application, according to the language you are using.</span></span> <span data-ttu-id="e52d0-252">Em cada um, faça estas substituições:</span><span class="sxs-lookup"><span data-stu-id="e52d0-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="e52d0-253">Substitua **INSERT-AUTHORITY-HERE** pelo nome do locatário no qual o aplicativo foi provisionado.</span><span class="sxs-lookup"><span data-stu-id="e52d0-253">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="e52d0-254">O formato deve ser https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="e52d0-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="e52d0-255">Esse valor pode ser copiado da guia Domínio no Azure Active Directory no [portal clássico do Azure].</span><span class="sxs-lookup"><span data-stu-id="e52d0-255">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="e52d0-256">Substitua **INSERT-RESOURCE-ID-HERE** pela ID do cliente do seu back-end de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="e52d0-256">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="e52d0-257">Você pode obter a ID do cliente na guia **Avançadas** em **Configurações do Azure Active Directory** no portal.</span><span class="sxs-lookup"><span data-stu-id="e52d0-257">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="e52d0-258">Substitua **INSERT-CLIENT-ID-HERE** pela ID do cliente copiada do aplicativo cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="e52d0-258">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="e52d0-259">Substitua **INSERT-REDIRECT-URI-HERE** pelo ponto de extremidade */.auth/login/done* do site, usando o esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e52d0-259">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="e52d0-260">Esse valor deve ser similar a *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="e52d0-260">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="e52d0-261">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-261">**Objective-C**:</span></span>

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


<span data-ttu-id="e52d0-262">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-262">**Swift**:</span></span>

    // add the following imports to your bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <span data-ttu-id="e52d0-263"><a name="facebook-sdk"></a>Instruções: autenticar usuários com o SDK do Facebook para iOS</span><span class="sxs-lookup"><span data-stu-id="e52d0-263"><a name="facebook-sdk"></a>How to: Authenticate users with the Facebook SDK for iOS</span></span>
<span data-ttu-id="e52d0-264">Você pode usar o SDK do Facebook para iOS para conectar os usuários ao seu aplicativo usando o Facebook.</span><span class="sxs-lookup"><span data-stu-id="e52d0-264">You can use the Facebook SDK for iOS to sign users into your application using Facebook.</span></span>  <span data-ttu-id="e52d0-265">É melhor usar a autenticação de fluxo de cliente do que usar o método `loginWithProvider:completion:` .</span><span class="sxs-lookup"><span data-stu-id="e52d0-265">Using a client flow authentication is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="e52d0-266">A autenticação do fluxo de cliente fornece uma aparência mais nativa de UX e permite uma maior personalização.</span><span class="sxs-lookup"><span data-stu-id="e52d0-266">The client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="e52d0-267">Configure o seu back-end de aplicativo móvel para entrar no Facebook seguindo o tutorial [Como configurar o Serviço de Aplicativo para logon do Facebook][9].</span><span class="sxs-lookup"><span data-stu-id="e52d0-267">Configure your mobile app backend for Facebook sign-in by following the [How to configure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="e52d0-268">Instale o SDK do Facebook para iOS seguindo a documentação [Facebook SDK para iOS - Introdução][10].</span><span class="sxs-lookup"><span data-stu-id="e52d0-268">Install the Facebook SDK for iOS by following the [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="e52d0-269">Em vez de criar um aplicativo, você pode adicionar a plataforma do iOS ao seu registro existente.</span><span class="sxs-lookup"><span data-stu-id="e52d0-269">Instead of creating an app, you can add the iOS platform to your existing registration.</span></span>
3. <span data-ttu-id="e52d0-270">A documentação do Facebook inclui algum código Objective-C no Representante do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e52d0-270">Facebook's documentation includes some Objective-C code in the App Delegate.</span></span> <span data-ttu-id="e52d0-271">Se você estiver usando **Swift**, poderá usar as seguintes conversões para AppDelegate.swift:</span><span class="sxs-lookup"><span data-stu-id="e52d0-271">If you are using **Swift**, you can use the following translations for AppDelegate.swift:</span></span>

        // Add the following import to your bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. <span data-ttu-id="e52d0-272">Além de adicionar `FBSDKCoreKit.framework` ao seu projeto, adicione também uma referência ao `FBSDKLoginKit.framework` da mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="e52d0-272">In addition to adding `FBSDKCoreKit.framework` to your project, also add a reference to `FBSDKLoginKit.framework` in the same way.</span></span>
5. <span data-ttu-id="e52d0-273">Adicione o código a seguir ao seu aplicativo, de acordo com a linguagem que você está usando.</span><span class="sxs-lookup"><span data-stu-id="e52d0-273">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="e52d0-274">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-274">**Objective-C**:</span></span>

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

<span data-ttu-id="e52d0-275">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-275">**Swift**:</span></span>

    // Add the following imports to your bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <span data-ttu-id="e52d0-276"><a name="twitter-fabric"></a>Instruções: autenticar usuários com a Twitter Fabric para iOS</span><span class="sxs-lookup"><span data-stu-id="e52d0-276"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="e52d0-277">Você pode usar a Fabric para iOS para desconectar os usuários em seu aplicativo usando o Twitter.</span><span class="sxs-lookup"><span data-stu-id="e52d0-277">You can use Fabric for iOS to sign users into your application using Twitter.</span></span> <span data-ttu-id="e52d0-278">Normalmente, é melhor usar a autenticação de fluxo de cliente do que usar o método `loginWithProvider:completion:` , pois ele fornece uma aparência mais nativa do UX e permite uma maior personalização.</span><span class="sxs-lookup"><span data-stu-id="e52d0-278">Client Flow authentication is preferable to using the `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="e52d0-279">Configurar o seu back-end de aplicativos móveis para entrar no Twitter, seguindo o tutorial [Como configurar o Serviço de Aplicativo para fazer logon no Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="e52d0-279">Configure your mobile app backend for Twitter sign-in by following the [How to configure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="e52d0-280">Adicione a Fabric ao seu projeto seguindo a documentação [Fabric para iOS - Introdução] e a configuração TwitterKit.</span><span class="sxs-lookup"><span data-stu-id="e52d0-280">Add Fabric to your project by following the [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e52d0-281">Por padrão, o Fabric cria um aplicativo do Twitter para você.</span><span class="sxs-lookup"><span data-stu-id="e52d0-281">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="e52d0-282">Você pode evitar a criação de um aplicativo registrando a Chave do Consumidor e o Segredo do Consumidor criados anteriormente usando os trechos de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="e52d0-282">You can avoid creating an application by registering the Consumer Key and Consumer Secret you created earlier using the following code snippets.</span></span>    <span data-ttu-id="e52d0-283">Como alternativa, você pode substituir os valores de chave do consumidor e segredo do consumidor que fornece ao Serviço de Aplicativo com os valores que vê no [Painel do Fabric].</span><span class="sxs-lookup"><span data-stu-id="e52d0-283">Alternatively, you can replace the Consumer Key and Consumer Secret values that you provide to App Service with the values you see in the [Fabric Dashboard].</span></span> <span data-ttu-id="e52d0-284">Se você escolher essa opção, certifique-se de definir a URL de retorno de chamada para um valor de espaço reservado, como `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="e52d0-284">If you choose this option, be sure to set the callback URL to a placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="e52d0-285">Se você optar por usar os segredos que criou anteriormente, adicione o seguinte código ao seu Representante de Aplicativo:</span><span class="sxs-lookup"><span data-stu-id="e52d0-285">If you choose to use the secrets you created earlier, add the following code to your App Delegate:</span></span>

    <span data-ttu-id="e52d0-286">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-286">**Objective-C**:</span></span>

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    <span data-ttu-id="e52d0-287">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-287">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="e52d0-288">Adicione o código a seguir ao seu aplicativo, de acordo com a linguagem que você está usando.</span><span class="sxs-lookup"><span data-stu-id="e52d0-288">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="e52d0-289">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-289">**Objective-C**:</span></span>

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

<span data-ttu-id="e52d0-290">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-290">**Swift**:</span></span>

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <span data-ttu-id="e52d0-291"><a name="google-sdk"></a>Instruções: autenticar usuários com o SDK do Login do Google para iOS</span><span class="sxs-lookup"><span data-stu-id="e52d0-291"><a name="google-sdk"></a>How to: Authenticate users with the Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="e52d0-292">Você pode usar o SDK do Login do Google para iOS para conectar os usuários ao seu aplicativo usando uma conta do Google.</span><span class="sxs-lookup"><span data-stu-id="e52d0-292">You can use the Google Sign-In SDK for iOS to sign users into your application using a Google account.</span></span>  <span data-ttu-id="e52d0-293">O Google anunciou alterações em suas políticas de segurança OAuth recentemente.</span><span class="sxs-lookup"><span data-stu-id="e52d0-293">Google recently announced changes to their OAuth security policies.</span></span>  <span data-ttu-id="e52d0-294">Essas alterações de política exigirão o uso do SDK do Google.</span><span class="sxs-lookup"><span data-stu-id="e52d0-294">These policy changes will require the use of the Google SDK in the future.</span></span>

1. <span data-ttu-id="e52d0-295">Configurar o seu back-end de aplicativos móveis para entrar no Google, seguindo o tutorial [How to configure App Service for Google login (Como configurar o Serviço de Aplicativo para fazer login no Google)](app-service-mobile-how-to-configure-google-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="e52d0-295">Configure your mobile app backend for Google sign-in by following the [How to configure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="e52d0-296">Instale o SDK do Google para iOS seguindo a documentação [Google Sign-In for iOS - Start integrating (Login do Google para iOS - iniciar a integração)](https://developers.google.com/identity/sign-in/ios/start-integrating) .</span><span class="sxs-lookup"><span data-stu-id="e52d0-296">Install the Google SDK for iOS by following the [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="e52d0-297">Você pode ignorar a seção "Autenticar com um servidor de back-end".</span><span class="sxs-lookup"><span data-stu-id="e52d0-297">You may skip the "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="e52d0-298">Adicione o seguinte ao método `signIn:didSignInForUser:withError:` do seu representante, de acordo com a linguagem que você estiver usando.</span><span class="sxs-lookup"><span data-stu-id="e52d0-298">Add the following to your delegate's `signIn:didSignInForUser:withError:` method, according to the language you are using.</span></span>

<span data-ttu-id="e52d0-299">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-299">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="e52d0-300">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-300">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="e52d0-301">Adicione também o seguinte ao `application:didFinishLaunchingWithOptions:` em seu representante de aplicativo, substituindo "SERVER_CLIENT_ID" pela mesma ID que você usou para configurar o Serviço de Aplicativo na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="e52d0-301">Make sure you also add the following to `application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with the same ID that you used to configure App Service in step 1.</span></span>

<span data-ttu-id="e52d0-302">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-302">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="e52d0-303">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-303">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="e52d0-304">Adicione o código a seguir ao seu aplicativo em um UIViewController que implementa o protocolo `GIDSignInUIDelegate` , de acordo com a linguagem que você está usando.</span><span class="sxs-lookup"><span data-stu-id="e52d0-304">Add the following code to your application in a UIViewController that implements the `GIDSignInUIDelegate` protocol, according to the language you are using.</span></span>  <span data-ttu-id="e52d0-305">Você é desconectado antes de ser conectado novamente e, embora não precise digitar suas credenciais novamente, um diálogo de consentimento é exibido.</span><span class="sxs-lookup"><span data-stu-id="e52d0-305">You are signed out before being signed in again, and although you don't need to enter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="e52d0-306">Só chame esse método quando o token de sessão tiver expirado.</span><span class="sxs-lookup"><span data-stu-id="e52d0-306">Only call this method when the session token has expired.</span></span>

   <span data-ttu-id="e52d0-307">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-307">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="e52d0-308">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e52d0-308">**Swift**:</span></span>

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create the Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data to the user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize the client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="e52d0-309">[Início Rápido dos Aplicativos Móveis do Azure]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="e52d0-309">[Azure Mobile Apps Quick Start]: app-service-mobile-ios-get-started.md</span></span>

[Add Mobile Services to Existing App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts to authorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
<span data-ttu-id="e52d0-310">[Esquema Dinâmico]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span><span class="sxs-lookup"><span data-stu-id="e52d0-310">[Dynamic Schema]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span></span>
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI to manage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

<span data-ttu-id="e52d0-311">[Painel do Fabric]: https://www.fabric.io/home</span><span class="sxs-lookup"><span data-stu-id="e52d0-311">[Fabric Dashboard]: https://www.fabric.io/home</span></span>
<span data-ttu-id="e52d0-312">[Fabric para iOS - Introdução]: https://docs.fabric.io/ios/fabric/getting-started.html</span><span class="sxs-lookup"><span data-stu-id="e52d0-312">[Fabric for iOS - Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html</span></span>
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
