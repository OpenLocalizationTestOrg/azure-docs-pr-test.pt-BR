---
title: "aaaHow tooUse SDK do iOS para aplicativos móveis do Azure"
description: "Como tooUse SDK do iOS para aplicativos móveis do Azure"
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
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="ec126-103">Como tooUse iOS biblioteca de cliente para aplicativos móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="ec126-103">How tooUse iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="ec126-104">Este guia ensina usando hello mais recente de cenários comuns de tooperform [os aplicativos móveis do Azure SDK do iOS][1].</span><span class="sxs-lookup"><span data-stu-id="ec126-104">This guide teaches you tooperform common scenarios using hello latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="ec126-105">Se você for novo tooAzure os aplicativos móveis, primeiro conclua [início rápido do Azure Mobile aplicativos] toocreate um back-end, crie uma tabela e baixar um projeto do Xcode iOS pré-criado.</span><span class="sxs-lookup"><span data-stu-id="ec126-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="ec126-106">Este guia, vamos nos concentrar no SDK do iOS saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="ec126-106">In this guide, we focus on hello client-side iOS SDK.</span></span> <span data-ttu-id="ec126-107">toolearn mais sobre Olá SDK do lado do servidor de back-end do hello, consulte HOWTOs de SDK do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec126-107">toolearn more about hello server-side SDK for hello backend, see hello Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="ec126-108">Documentação de referência</span><span class="sxs-lookup"><span data-stu-id="ec126-108">Reference documentation</span></span>
<span data-ttu-id="ec126-109">Olá documentação de referência do SDK do cliente de iOS hello está localizada aqui: [os aplicativos móveis do Azure iOS cliente referência][2].</span><span class="sxs-lookup"><span data-stu-id="ec126-109">hello reference documentation for hello iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="ec126-110">Plataformas com suporte</span><span class="sxs-lookup"><span data-stu-id="ec126-110">Supported Platforms</span></span>
<span data-ttu-id="ec126-111">SDK do iOS Olá suporta projetos Objective-C, Swift 2.2 projetos e Swift 2.3 projetos para o iOS versão 8.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ec126-111">hello iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="ec126-112">autenticação de "server-fluxo" Hello usa WebView para Olá apresentado da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="ec126-112">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="ec126-113">Se o dispositivo de Olá não for capaz de toopresent uma UI WebView, em seguida, outro método de autenticação é necessário que está fora do escopo Olá produto hello.</span><span class="sxs-lookup"><span data-stu-id="ec126-113">If hello device is not able toopresent a WebView UI, then another method of authentication is required that is outside hello scope of hello product.</span></span>  
<span data-ttu-id="ec126-114">Esse SDK, portanto, não é adequado para relógios ou dispositivos similarmente restritos.</span><span class="sxs-lookup"><span data-stu-id="ec126-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="ec126-115"><a name="Setup"></a>Configuração e Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ec126-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="ec126-116">Este guia pressupõe que você tenha criado um back-end com uma tabela.</span><span class="sxs-lookup"><span data-stu-id="ec126-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="ec126-117">Este guia pressupõe que dessa tabela Olá tem o mesmo esquema como tabelas Olá esses tutoriais.</span><span class="sxs-lookup"><span data-stu-id="ec126-117">This guide assumes that hello table has the same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="ec126-118">Este guia também pressupõe que em seu código, você referencia `MicrosoftAzureMobile.framework` e importa `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="ec126-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="ec126-119"><a name="create-client"></a>Como: criar o cliente</span><span class="sxs-lookup"><span data-stu-id="ec126-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="ec126-120">tooaccess um back-end de aplicativos do Azure Mobile no seu projeto, criar um `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="ec126-120">tooaccess an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="ec126-121">Substituir `AppUrl` com a URL do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ec126-121">Replace `AppUrl` with hello app URL.</span></span> <span data-ttu-id="ec126-122">Você pode deixar `gatewayURLString` e `applicationKey` vazios.</span><span class="sxs-lookup"><span data-stu-id="ec126-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="ec126-123">Se você configurar um gateway para autenticação, popular `gatewayURLString` com hello gateway URL.</span><span class="sxs-lookup"><span data-stu-id="ec126-123">If you set up a gateway for authentication, populate `gatewayURLString` with hello gateway URL.</span></span>

<span data-ttu-id="ec126-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="ec126-125">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="ec126-126"><a name="table-reference"></a>Como criar uma referência de tabela</span><span class="sxs-lookup"><span data-stu-id="ec126-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="ec126-127">tooaccess ou atualização de dados, crie uma tabela de back-end do toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="ec126-127">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="ec126-128">Substituir `TodoItem` com nome de saudação da tabela</span><span class="sxs-lookup"><span data-stu-id="ec126-128">Replace `TodoItem` with hello name of your table</span></span>

<span data-ttu-id="ec126-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="ec126-130">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="ec126-131"><a name="querying"></a>Como consultar dados</span><span class="sxs-lookup"><span data-stu-id="ec126-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="ec126-132">toocreate uma consulta de banco de dados, Olá consulta `MSTable` objeto.</span><span class="sxs-lookup"><span data-stu-id="ec126-132">toocreate a database query, query hello `MSTable` object.</span></span> <span data-ttu-id="ec126-133">Olá consulta a seguir obtém todos os itens de saudação `TodoItem` e logs Olá texto de cada item.</span><span class="sxs-lookup"><span data-stu-id="ec126-133">hello following query gets all hello items in `TodoItem` and logs hello text of each item.</span></span>

<span data-ttu-id="ec126-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-134">**Objective-C**:</span></span>

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

<span data-ttu-id="ec126-135">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-135">**Swift**:</span></span>

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

## <span data-ttu-id="ec126-136"><a name="filtering"></a>Como filtrar dados retornados</span><span class="sxs-lookup"><span data-stu-id="ec126-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="ec126-137">resultados de toofilter, há muitas opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ec126-137">toofilter results, there are many available options.</span></span>

<span data-ttu-id="ec126-138">toofilter usando um predicado, use um `NSPredicate` e `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="ec126-138">toofilter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="ec126-139">seguinte Olá filtra dados retornados toofind incompletas apenas itens de tarefas.</span><span class="sxs-lookup"><span data-stu-id="ec126-139">hello following filters returned data toofind only incomplete Todo items.</span></span>

<span data-ttu-id="ec126-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
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

<span data-ttu-id="ec126-141">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
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

## <span data-ttu-id="ec126-142"><a name="query-object"></a>Como usar o MSQuery</span><span class="sxs-lookup"><span data-stu-id="ec126-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="ec126-143">tooperform criar uma consulta complexa (incluindo classificação e paginação), um `MSQuery` de objeto, diretamente ou por meio de um predicado:</span><span class="sxs-lookup"><span data-stu-id="ec126-143">tooperform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="ec126-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="ec126-145">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="ec126-146">`MSQuery` permite que você controle vários comportamentos de consulta.</span><span class="sxs-lookup"><span data-stu-id="ec126-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="ec126-147">Especificar a ordem dos resultados</span><span class="sxs-lookup"><span data-stu-id="ec126-147">Specify order of results</span></span>
* <span data-ttu-id="ec126-148">Limitar quais campos tooreturn</span><span class="sxs-lookup"><span data-stu-id="ec126-148">Limit which fields tooreturn</span></span>
* <span data-ttu-id="ec126-149">Limitar quantos registros tooreturn</span><span class="sxs-lookup"><span data-stu-id="ec126-149">Limit how many records tooreturn</span></span>
* <span data-ttu-id="ec126-150">Especificar contagem total na resposta</span><span class="sxs-lookup"><span data-stu-id="ec126-150">Specify total count in response</span></span>
* <span data-ttu-id="ec126-151">Especificar parâmetros de cadeia de consulta personalizada na solicitação</span><span class="sxs-lookup"><span data-stu-id="ec126-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="ec126-152">Aplicar funções adicionais</span><span class="sxs-lookup"><span data-stu-id="ec126-152">Apply additional functions</span></span>

<span data-ttu-id="ec126-153">Executar um `MSQuery` consulta chamando `readWithCompletion` no objeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec126-153">Execute an `MSQuery` query by calling `readWithCompletion` on hello object.</span></span>

## <span data-ttu-id="ec126-154"><a name="sorting"></a>Como classificar dados com MSQuery</span><span class="sxs-lookup"><span data-stu-id="ec126-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="ec126-155">resultados de toosort, vamos examinar um exemplo.</span><span class="sxs-lookup"><span data-stu-id="ec126-155">toosort results, let's look at an example.</span></span> <span data-ttu-id="ec126-156">toosort por 'text' campo em ordem crescente e decrescente 'completa', invocar `MSQuery` da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="ec126-156">toosort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="ec126-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-157">**Objective-C**:</span></span>

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

<span data-ttu-id="ec126-158">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-158">**Swift**:</span></span>

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


## <span data-ttu-id="ec126-159"><a name="selecting"></a><a name="parameters"></a>Como limitar campos e expandir os parâmetros de cadeia de caracteres de consulta com MSQuery</span><span class="sxs-lookup"><span data-stu-id="ec126-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="ec126-160">toolimit toobe de campos retornado em uma consulta, especificar nomes de saudação de campos de saudação no hello **selectFields** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ec126-160">toolimit fields toobe returned in a query, specify hello names of hello fields in hello **selectFields** property.</span></span> <span data-ttu-id="ec126-161">Este exemplo retorna somente o texto de saudação e campos concluídos:</span><span class="sxs-lookup"><span data-stu-id="ec126-161">This example returns only hello text and completed fields:</span></span>

<span data-ttu-id="ec126-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="ec126-163">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="ec126-164">parâmetros de cadeia de caracteres de consulta adicionais tooinclude no servidor de saudação solicitar (por exemplo, porque usa um script do lado do servidor personalizado), popular `query.parameters` da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="ec126-164">tooinclude additional query string parameters in hello server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="ec126-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="ec126-166">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="ec126-167"><a name="paging"></a>Como: Configurar o tamanho de página</span><span class="sxs-lookup"><span data-stu-id="ec126-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="ec126-168">Com aplicativos móveis do Azure, controles de tamanho de página Olá Olá número de registros que são extraídas por vez de tabelas de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec126-168">With Azure Mobile Apps, hello page size controls hello number of records that are pulled at a time from hello backend tables.</span></span> <span data-ttu-id="ec126-169">Uma chamada muito`pull` dados seriam do lote, em seguida, os dados, com base no tamanho de página, até que não haja nenhum toopull registros mais.</span><span class="sxs-lookup"><span data-stu-id="ec126-169">A call too`pull` data would then batch up data, based on this page size, until there are no more records toopull.</span></span>

<span data-ttu-id="ec126-170">É possível tooconfigure um tamanho de página usando **MSPullSettings** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ec126-170">It's possible tooconfigure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="ec126-171">tamanho de página saudação padrão é 50, e o exemplo hello abaixo altera too3.</span><span class="sxs-lookup"><span data-stu-id="ec126-171">hello default page size is 50, and hello example below changes it too3.</span></span>

<span data-ttu-id="ec126-172">Você pode configurar um tamanho de página diferente por motivos de desempenho.</span><span class="sxs-lookup"><span data-stu-id="ec126-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="ec126-173">Se você tiver um grande número de registros de dados pequeno, um tamanho de página de alta reduz o número de saudação de ida e volta do servidor.</span><span class="sxs-lookup"><span data-stu-id="ec126-173">If you have a large number of small data records, a high page size reduces hello number of server round-trips.</span></span>

<span data-ttu-id="ec126-174">Essa configuração controla apenas o tamanho de página Olá no lado do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec126-174">This setting controls only hello page size on hello client side.</span></span> <span data-ttu-id="ec126-175">Se o cliente Olá solicita um tamanho de página maior que oferece suporte a aplicativos móveis de saudação back-end, o tamanho da página de saudação é controlada no back-end do Olá Olá máximo é toosupport configurado.</span><span class="sxs-lookup"><span data-stu-id="ec126-175">If hello client asks for a larger page size than hello Mobile Apps backend supports, hello page size is capped at hello maximum hello backend is configured toosupport.</span></span>

<span data-ttu-id="ec126-176">Essa configuração também é hello *número* de registros de dados, não Olá *tamanho em bytes*.</span><span class="sxs-lookup"><span data-stu-id="ec126-176">This setting is also hello *number* of data records, not hello *byte size*.</span></span>

<span data-ttu-id="ec126-177">Se você aumentar o tamanho de página do cliente hello, você também deve aumentar o tamanho de página Olá no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec126-177">If you increase hello client page size, you should also increase hello page size on hello server.</span></span> <span data-ttu-id="ec126-178">Consulte ["como: ajustar o tamanho da paginação tabela hello"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para Olá etapas toodo isso.</span><span class="sxs-lookup"><span data-stu-id="ec126-178">See ["How to: Adjust hello table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for hello steps toodo this.</span></span>

<span data-ttu-id="ec126-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="ec126-180">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="ec126-181"><a name="inserting"></a>Como inserir dados</span><span class="sxs-lookup"><span data-stu-id="ec126-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="ec126-182">criar uma nova linha de tabela, de tooinsert um `NSDictionary` e invocar `table insert`.</span><span class="sxs-lookup"><span data-stu-id="ec126-182">tooinsert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="ec126-183">Se [esquema dinâmico] é habilitado, hello Azure do serviço de aplicativo móvel back-end automaticamente gera novas colunas com base em Olá `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="ec126-183">If [Dynamic Schema] is enabled, hello Azure App Service mobile backend automatically generates new columns based on hello `NSDictionary`.</span></span>

<span data-ttu-id="ec126-184">Se `id` não for fornecido, Olá back-end gera automaticamente uma nova ID exclusiva.</span><span class="sxs-lookup"><span data-stu-id="ec126-184">If `id` is not provided, hello backend automatically generates a new unique ID.</span></span> <span data-ttu-id="ec126-185">Fornecer sua própria `id` toouse seus próprios valores personalizados, nomes de usuário ou endereços de email como ID.</span><span class="sxs-lookup"><span data-stu-id="ec126-185">Provide your own `id` toouse email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="ec126-186">Fornecer sua própria identificação pode facilitar junções e lógicas de banco de dados comerciais.</span><span class="sxs-lookup"><span data-stu-id="ec126-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="ec126-187">Olá `result` contém Olá novo item que foi inserida.</span><span class="sxs-lookup"><span data-stu-id="ec126-187">hello `result` contains hello new item that was inserted.</span></span> <span data-ttu-id="ec126-188">Dependendo de sua lógica de servidor, pode ter adicionais em comparação comparados os dados modificados toowhat foi passado ou toohello server.</span><span class="sxs-lookup"><span data-stu-id="ec126-188">Depending on your server logic, it may have additional or modified data compared toowhat was passed toohello server.</span></span>

<span data-ttu-id="ec126-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-189">**Objective-C**:</span></span>

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

<span data-ttu-id="ec126-190">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-190">**Swift**:</span></span>

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

## <span data-ttu-id="ec126-191"><a name="modifying"></a>Como modificar dados</span><span class="sxs-lookup"><span data-stu-id="ec126-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="ec126-192">tooupdate uma linha existente, modifique um item e a chamada `update`:</span><span class="sxs-lookup"><span data-stu-id="ec126-192">tooupdate an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="ec126-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-193">**Objective-C**:</span></span>

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

<span data-ttu-id="ec126-194">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-194">**Swift**:</span></span>

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

<span data-ttu-id="ec126-195">Como alternativa, fornece Olá ID da linha e campo Olá atualizado:</span><span class="sxs-lookup"><span data-stu-id="ec126-195">Alternatively, supply hello row ID and hello updated field:</span></span>

<span data-ttu-id="ec126-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="ec126-197">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="ec126-198">No mínimo, Olá `id` atributo deve ser definido ao fazer atualizações.</span><span class="sxs-lookup"><span data-stu-id="ec126-198">At minimum, hello `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="ec126-199"><a name="deleting"></a>Como excluir dados</span><span class="sxs-lookup"><span data-stu-id="ec126-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="ec126-200">toodelete um item, invocar `delete` com item hello:</span><span class="sxs-lookup"><span data-stu-id="ec126-200">toodelete an item, invoke `delete` with hello item:</span></span>

<span data-ttu-id="ec126-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="ec126-202">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="ec126-203">Como alternativa, exclua fornecendo uma ID de linha:</span><span class="sxs-lookup"><span data-stu-id="ec126-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="ec126-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="ec126-205">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="ec126-206">No mínimo, Olá `id` atributo deve ser definido quando fazer exclui.</span><span class="sxs-lookup"><span data-stu-id="ec126-206">At minimum, hello `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="ec126-207"><a name="customapi"></a>Como chamar uma API personalizada</span><span class="sxs-lookup"><span data-stu-id="ec126-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="ec126-208">Com uma API personalizada, você pode expor qualquer funcionalidade de back-end.</span><span class="sxs-lookup"><span data-stu-id="ec126-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="ec126-209">Operação de tabela tooa toomap não é necessário.</span><span class="sxs-lookup"><span data-stu-id="ec126-209">It doesn't have toomap tooa table operation.</span></span> <span data-ttu-id="ec126-210">Não só você obter mais controle sobre o sistema de mensagens, você pode até mesmo conjunto de cabeçalhos de leitura/e alterar o formato do corpo de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec126-210">Not only do you gain more control over messaging, you can even read/set headers and change hello response body format.</span></span> <span data-ttu-id="ec126-211">toolearn como toocreate uma API personalizada no back-end hello, ler [APIs personalizadas](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="ec126-211">toolearn how toocreate a custom API on hello backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="ec126-212">toocall uma API personalizada, chame `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="ec126-212">toocall a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="ec126-213">saudação de solicitação e resposta de conteúdo são tratados como JSON.</span><span class="sxs-lookup"><span data-stu-id="ec126-213">hello request and response content are treated as JSON.</span></span> <span data-ttu-id="ec126-214">toouse outros tipos de mídia, [use Olá outra sobrecarga do `invokeAPI` ] [ 5].</span><span class="sxs-lookup"><span data-stu-id="ec126-214">toouse other media types, [use hello other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="ec126-215">toomake um `GET` solicitação em vez de um `POST` solicitação, o parâmetro de conjunto de `HTTPMethod` muito`"GET"` e parâmetro `body` muito`nil` (como solicitações GET não ter corpos de mensagens.) Se sua API personalizada dá suporte a outros verbos HTTP, altere o `HTTPMethod` adequadamente.</span><span class="sxs-lookup"><span data-stu-id="ec126-215">toomake a `GET` request instead of a `POST` request, set parameter `HTTPMethod` too`"GET"` and parameter `body` too`nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="ec126-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-216">**Objective-C**:</span></span>

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

<span data-ttu-id="ec126-217">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-217">**Swift**:</span></span>

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

## <span data-ttu-id="ec126-218"><a name="templates"></a>Como: notificações de plataforma cruzada do registro por push modelos toosend</span><span class="sxs-lookup"><span data-stu-id="ec126-218"><a name="templates"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="ec126-219">modelos de tooregister passar modelos com seu **client.push registerDeviceToken** método no seu aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="ec126-219">tooregister templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="ec126-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="ec126-221">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="ec126-222">Os modelos são do tipo NSDictionary e podem conter vários modelos em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec126-222">Your templates are of type NSDictionary and can contain multiple templates in hello following format:</span></span>

<span data-ttu-id="ec126-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="ec126-224">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="ec126-225">Todas as marcas são eliminadas da solicitação de saudação de segurança.</span><span class="sxs-lookup"><span data-stu-id="ec126-225">All tags are stripped from hello request for security.</span></span>  <span data-ttu-id="ec126-226">tooadd marcas tooinstallations ou modelos dentro de instalações, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure][4].</span><span class="sxs-lookup"><span data-stu-id="ec126-226">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="ec126-227">notificações de toosend usando esses modelos registrados, trabalhar com [APIs de Hubs de notificação][3].</span><span class="sxs-lookup"><span data-stu-id="ec126-227">toosend notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="ec126-228"><a name="errors"></a>Como tratar erros</span><span class="sxs-lookup"><span data-stu-id="ec126-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="ec126-229">Quando você chama um back-end móvel do serviço de aplicativo do Azure, o bloco de conclusão de saudação contém um `NSError` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="ec126-229">When you call an Azure App Service mobile backend, hello completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="ec126-230">Quando ocorre um erro, esse parâmetro é não nulo.</span><span class="sxs-lookup"><span data-stu-id="ec126-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="ec126-231">No seu código, você deve verificar esse parâmetro e tratar o erro Olá conforme necessário, como demonstrado no hello anterior trechos de código.</span><span class="sxs-lookup"><span data-stu-id="ec126-231">In your code, you should check this parameter and handle hello error as needed, as demonstrated in hello preceding code snippets.</span></span>

<span data-ttu-id="ec126-232">arquivo Hello [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] define constantes Olá `MSErrorResponseKey`, `MSErrorRequestKey`, e `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="ec126-232">hello file [`<WindowsAzureMobileServices/MSError.h>`][6] defines hello constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="ec126-233">tooget mais dados relacionados ao erro toohello:</span><span class="sxs-lookup"><span data-stu-id="ec126-233">tooget more data related toohello error:</span></span>

<span data-ttu-id="ec126-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="ec126-235">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="ec126-236">Além disso, o arquivo hello define constantes para cada código de erro:</span><span class="sxs-lookup"><span data-stu-id="ec126-236">In addition, hello file defines constants for each error code:</span></span>

<span data-ttu-id="ec126-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="ec126-238">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="ec126-239"><a name="adal"></a>Como: autenticar usuários com hello biblioteca de autenticação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec126-239"><a name="adal"></a>How to: Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="ec126-240">Você pode usar usuários do hello biblioteca de autenticação do Active Directory (ADAL) toosign em seu aplicativo usando o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec126-240">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="ec126-241">Autenticação de fluxo de cliente usando um provedor de identidade SDK é preferível toousing Olá `loginWithProvider:completion:` método.</span><span class="sxs-lookup"><span data-stu-id="ec126-241">Client flow authentication using an identity provider SDK is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="ec126-242">Autenticação de fluxo de cliente fornece uma aparência mais nativa do UX e permite uma maior personalização.</span><span class="sxs-lookup"><span data-stu-id="ec126-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="ec126-243">Configurar seu back-end do aplicativo móvel para entrar no AAD pela seguinte Olá [como tooconfigure aplicativo de serviço de logon do Active Directory] [ 7] tutorial.</span><span class="sxs-lookup"><span data-stu-id="ec126-243">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="ec126-244">Torne-se toocomplete Olá opcional de registro de um aplicativo cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="ec126-244">Make sure toocomplete hello optional step of registering a native client application.</span></span> <span data-ttu-id="ec126-245">Para iOS, é recomendável que direcionam Olá URI tem formato Olá `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="ec126-245">For iOS, we recommend that hello redirect URI is of hello form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="ec126-246">Para obter mais informações, consulte Olá [quickstart iOS ADAL][8].</span><span class="sxs-lookup"><span data-stu-id="ec126-246">For more information, see hello [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="ec126-247">Instale o ADAL usando o Cocoapods.</span><span class="sxs-lookup"><span data-stu-id="ec126-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="ec126-248">Editar a saudação de tooinclude Podfile definição a seguir, substituindo **seu projeto** com nome de saudação do seu projeto Xcode:</span><span class="sxs-lookup"><span data-stu-id="ec126-248">Edit your Podfile tooinclude hello following definition, replacing **YOUR-PROJECT** with hello name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="ec126-249">e hello Pod:</span><span class="sxs-lookup"><span data-stu-id="ec126-249">and hello Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="ec126-250">Usando Olá Terminal, execute `pod install` do diretório Olá contendo seu projeto e abra Olá gerado Xcode espaço de trabalho (não o projeto de saudação).</span><span class="sxs-lookup"><span data-stu-id="ec126-250">Using hello Terminal, run `pod install` from hello directory containing your project, and then open hello generated Xcode workspace (not hello project).</span></span>
4. <span data-ttu-id="ec126-251">Adicione Olá aplicativo tooyour de código a seguir, de acordo com a linguagem de toohello que você está usando.</span><span class="sxs-lookup"><span data-stu-id="ec126-251">Add hello following code tooyour application, according toohello language you are using.</span></span> <span data-ttu-id="ec126-252">Em cada um, faça estas substituições:</span><span class="sxs-lookup"><span data-stu-id="ec126-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="ec126-253">Substituir **aqui de autoridade de inserção** com o nome de saudação do locatário Olá no qual você provisionou o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ec126-253">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="ec126-254">O formato deve ser https://login.microsoftonline.com/contoso.onmicrosoft.com. Esse valor pode ser copiado de guia de saudação do domínio no Active Directory do Azure no hello [portal clássico do Azure].</span><span class="sxs-lookup"><span data-stu-id="ec126-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="ec126-255">Substituir **inserir recursos-ID aqui** com a ID de cliente Olá para o back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="ec126-255">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="ec126-256">Você pode obter a ID do cliente de saudação **avançado** guia **configurações do Active Directory do Azure** no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec126-256">You can obtain the client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="ec126-257">Substituir **aqui INSERT-CLIENT-ID** com a ID de cliente Olá você copiou do aplicativo cliente nativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec126-257">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="ec126-258">Substituir **INSERT-REDIRECT-URI-aqui** com seu site */.auth/login/done* ponto de extremidade, usando o esquema do hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ec126-258">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="ec126-259">Esse valor deve ser semelhante muito*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="ec126-259">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="ec126-260">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-260">**Objective-C**:</span></span>

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


<span data-ttu-id="ec126-261">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-261">**Swift**:</span></span>

    // add hello following imports tooyour bridging header:
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

## <span data-ttu-id="ec126-262"><a name="facebook-sdk"></a>Como: autenticar usuários com hello Facebook SDK para iOS</span><span class="sxs-lookup"><span data-stu-id="ec126-262"><a name="facebook-sdk"></a>How to: Authenticate users with hello Facebook SDK for iOS</span></span>
<span data-ttu-id="ec126-263">Você pode usar o hello Facebook SDK para iOS toosign usuários em seu aplicativo usando o Facebook.</span><span class="sxs-lookup"><span data-stu-id="ec126-263">You can use hello Facebook SDK for iOS toosign users into your application using Facebook.</span></span>  <span data-ttu-id="ec126-264">Usando a autenticação de um fluxo de cliente é preferível toousing Olá `loginWithProvider:completion:` método.</span><span class="sxs-lookup"><span data-stu-id="ec126-264">Using a client flow authentication is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="ec126-265">autenticação de fluxo de cliente Olá fornece uma aparência UX mais nativa e permite a personalização adicional.</span><span class="sxs-lookup"><span data-stu-id="ec126-265">hello client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="ec126-266">Configure seu back-end do aplicativo móvel para entrar no Facebook seguindo o [como tooconfigure aplicativo de serviço de logon do Facebook] [ 9] tutorial.</span><span class="sxs-lookup"><span data-stu-id="ec126-266">Configure your mobile app backend for Facebook sign-in by following the [How tooconfigure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="ec126-267">Instalar Olá Facebook SDK para iOS pela seguinte Olá [Facebook SDK para iOS - Introdução] [ 10] documentação.</span><span class="sxs-lookup"><span data-stu-id="ec126-267">Install hello Facebook SDK for iOS by following hello [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="ec126-268">Em vez de criar um aplicativo, você pode adicionar um registro existente de tooyour Olá de plataforma iOS.</span><span class="sxs-lookup"><span data-stu-id="ec126-268">Instead of creating an app, you can add hello iOS platform tooyour existing registration.</span></span>
3. <span data-ttu-id="ec126-269">Documentação do Facebook inclui um código Objective-C em Olá representante do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ec126-269">Facebook's documentation includes some Objective-C code in hello App Delegate.</span></span> <span data-ttu-id="ec126-270">Se você estiver usando **Swift**, você pode usar o hello traduções para appdelegate. SWIFT a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec126-270">If you are using **Swift**, you can use hello following translations for AppDelegate.swift:</span></span>

        // Add hello following import tooyour bridging header:
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
4. <span data-ttu-id="ec126-271">Em adição tooadding `FBSDKCoreKit.framework` tooyour de projeto, também adicionar uma referência muito`FBSDKLoginKit.framework` em Olá mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="ec126-271">In addition tooadding `FBSDKCoreKit.framework` tooyour project, also add a reference too`FBSDKLoginKit.framework` in hello same way.</span></span>
5. <span data-ttu-id="ec126-272">Adicione Olá aplicativo tooyour de código a seguir, de acordo com a linguagem de toohello que você está usando.</span><span class="sxs-lookup"><span data-stu-id="ec126-272">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="ec126-273">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-273">**Objective-C**:</span></span>

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

<span data-ttu-id="ec126-274">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-274">**Swift**:</span></span>

    // Add hello following imports tooyour bridging header:
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

## <span data-ttu-id="ec126-275"><a name="twitter-fabric"></a>Instruções: autenticar usuários com a Twitter Fabric para iOS</span><span class="sxs-lookup"><span data-stu-id="ec126-275"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="ec126-276">Você pode usar a malha para usuários do iOS toosign em seu aplicativo usando o Twitter.</span><span class="sxs-lookup"><span data-stu-id="ec126-276">You can use Fabric for iOS toosign users into your application using Twitter.</span></span> <span data-ttu-id="ec126-277">Autenticação de cliente de fluxo é preferível toousing Olá `loginWithProvider:completion:` método, como ele fornece uma aparência UX mais nativa e permite a personalização adicional.</span><span class="sxs-lookup"><span data-stu-id="ec126-277">Client Flow authentication is preferable toousing hello `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="ec126-278">Para configurar seu back-end do aplicativo móvel para entrar no Twitter, Olá após [como tooconfigure de serviço de aplicativo para o logon do Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="ec126-278">Configure your mobile app backend for Twitter sign-in by following hello [How tooconfigure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="ec126-279">Adicionar projeto de tooyour de malha, Olá seguir [malha para iOS - Introdução] documentação e a configuração TwitterKit.</span><span class="sxs-lookup"><span data-stu-id="ec126-279">Add Fabric tooyour project by following hello [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ec126-280">Por padrão, o Fabric cria um aplicativo do Twitter para você.</span><span class="sxs-lookup"><span data-stu-id="ec126-280">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="ec126-281">Você pode evitar a criação de um aplicativo registrando Olá chave do consumidor e o segredo do consumidor criado anteriormente usando o hello trechos de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="ec126-281">You can avoid creating an application by registering hello Consumer Key and Consumer Secret you created earlier using hello following code snippets.</span></span>    <span data-ttu-id="ec126-282">Como alternativa, você pode substituir Olá chave do consumidor e valores de segredo do consumidor que você forneça valores tooApp serviço com hello consulte Olá [painel da malha].</span><span class="sxs-lookup"><span data-stu-id="ec126-282">Alternatively, you can replace hello Consumer Key and Consumer Secret values that you provide tooApp Service with hello values you see in hello [Fabric Dashboard].</span></span> <span data-ttu-id="ec126-283">Se você escolher essa opção, ser se tooset Olá retorno de chamada URL tooa valor de espaço reservado, como `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="ec126-283">If you choose this option, be sure tooset hello callback URL tooa placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="ec126-284">Se você escolher toouse segredos Olá criado anteriormente, adicione Olá código tooyour representante do aplicativo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec126-284">If you choose toouse hello secrets you created earlier, add hello following code tooyour App Delegate:</span></span>

    <span data-ttu-id="ec126-285">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-285">**Objective-C**:</span></span>

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

    <span data-ttu-id="ec126-286">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-286">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="ec126-287">Adicione Olá aplicativo tooyour de código a seguir, de acordo com a linguagem de toohello que você está usando.</span><span class="sxs-lookup"><span data-stu-id="ec126-287">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="ec126-288">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-288">**Objective-C**:</span></span>

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

<span data-ttu-id="ec126-289">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-289">**Swift**:</span></span>

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

## <span data-ttu-id="ec126-290"><a name="google-sdk"></a>Como: autenticar usuários com hello Google entrar SDK para iOS</span><span class="sxs-lookup"><span data-stu-id="ec126-290"><a name="google-sdk"></a>How to: Authenticate users with hello Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="ec126-291">Você pode usar o hello Google entrar SDK para iOS toosign usuários em seu aplicativo usando uma conta do Google.</span><span class="sxs-lookup"><span data-stu-id="ec126-291">You can use hello Google Sign-In SDK for iOS toosign users into your application using a Google account.</span></span>  <span data-ttu-id="ec126-292">Google recentemente anunciado alterações tootheir OAuth as políticas de segurança.</span><span class="sxs-lookup"><span data-stu-id="ec126-292">Google recently announced changes tootheir OAuth security policies.</span></span>  <span data-ttu-id="ec126-293">Essas alterações de política requerem Olá uso do SDK do Google no hello futuras.</span><span class="sxs-lookup"><span data-stu-id="ec126-293">These policy changes will require hello use of the Google SDK in hello future.</span></span>

1. <span data-ttu-id="ec126-294">Configurar seu back-end do aplicativo móvel para entrar no Google pelo seguinte Olá [como tooconfigure de serviço de aplicativo para o logon do Google](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="ec126-294">Configure your mobile app backend for Google sign-in by following hello [How tooconfigure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="ec126-295">Instalar Olá Google SDK para iOS pela seguinte Olá [Sign-In Google para iOS - iniciar a integração de](https://developers.google.com/identity/sign-in/ios/start-integrating) documentação.</span><span class="sxs-lookup"><span data-stu-id="ec126-295">Install hello Google SDK for iOS by following hello [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="ec126-296">Você pode ignorar a seção de "Autenticar com um servidor back-end" hello.</span><span class="sxs-lookup"><span data-stu-id="ec126-296">You may skip hello "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="ec126-297">Adicionar saudação do tooyour representante a seguir `signIn:didSignInForUser:withError:` método, de acordo com o idioma toohello que você está usando.</span><span class="sxs-lookup"><span data-stu-id="ec126-297">Add hello following tooyour delegate's `signIn:didSignInForUser:withError:` method, according toohello language you are using.</span></span>

<span data-ttu-id="ec126-298">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-298">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="ec126-299">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-299">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="ec126-300">Certifique-se de também adicionar Olá seguir muito`application:didFinishLaunchingWithOptions:` em seu aplicativo delegar, substituindo "SERVER_CLIENT_ID" com hello mesma ID que você usou tooconfigure do serviço de aplicativo na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="ec126-300">Make sure you also add hello following too`application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with hello same ID that you used tooconfigure App Service in step 1.</span></span>

<span data-ttu-id="ec126-301">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-301">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="ec126-302">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-302">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="ec126-303">Adicionar Olá após o aplicativo de tooyour de código em um UIViewController que implementa Olá `GIDSignInUIDelegate` protocolo, de acordo com a linguagem de toohello que você está usando.</span><span class="sxs-lookup"><span data-stu-id="ec126-303">Add hello following code tooyour application in a UIViewController that implements hello `GIDSignInUIDelegate` protocol, according toohello language you are using.</span></span>  <span data-ttu-id="ec126-304">Você saiu antes que está sendo assinado novamente, e embora não seja necessário tooenter suas credenciais novamente, você verá uma caixa de diálogo de consentimento.</span><span class="sxs-lookup"><span data-stu-id="ec126-304">You are signed out before being signed in again, and although you don't need tooenter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="ec126-305">Chame esse método quando o token de sessão Olá expirou.</span><span class="sxs-lookup"><span data-stu-id="ec126-305">Only call this method when hello session token has expired.</span></span>

   <span data-ttu-id="ec126-306">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ec126-306">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="ec126-307">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ec126-307">**Swift**:</span></span>

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
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[início rápido do Azure Mobile aplicativos]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[esquema dinâmico]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[painel da malha]: https://www.fabric.io/home
[malha para iOS - Introdução]: https://docs.fabric.io/ios/fabric/getting-started.html
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
