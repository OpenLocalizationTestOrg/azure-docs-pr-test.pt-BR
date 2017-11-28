---
title: "aaaWorking com hello aplicativos móveis do aplicativo de serviço gerenciado de biblioteca de cliente (Windows | Microsoft Docs"
description: "Saiba como toouse um cliente .NET para aplicativos móveis de serviço de aplicativo do Azure com aplicativos do Windows e Xamarin."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="f0d09-103">Como toouse Olá gerenciada do cliente para aplicativos móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="f0d09-103">How toouse hello managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="f0d09-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f0d09-104">Overview</span></span>
<span data-ttu-id="f0d09-105">Este guia mostra como os cenários comuns de tooperform usando Olá gerenciados biblioteca de cliente para aplicativos do Azure aplicativo serviços móveis aplicativos para Windows e Xamarin.</span><span class="sxs-lookup"><span data-stu-id="f0d09-105">This guide shows you how tooperform common scenarios using hello managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="f0d09-106">Se você estiver tooMobile de novos aplicativos, você deve considerar primeiro Olá Concluindo [início rápido de aplicativos do Azure Mobile] [ 1] tutorial.</span><span class="sxs-lookup"><span data-stu-id="f0d09-106">If you are new tooMobile Apps, you should consider first completing hello [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="f0d09-107">Este guia, vamos nos concentrar em saudação do cliente gerenciado SDK.</span><span class="sxs-lookup"><span data-stu-id="f0d09-107">In this guide, we focus on hello client-side managed SDK.</span></span> <span data-ttu-id="f0d09-108">toolearn mais sobre hello SDKs do lado do servidor para aplicativos móveis, consulte a documentação Olá Olá [SDK do .NET Server] [ 2] ou [Node. js servidor SDK] [ 3].</span><span class="sxs-lookup"><span data-stu-id="f0d09-108">toolearn more about hello server-side SDKs for Mobile Apps, see hello documentation for hello [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="f0d09-109">Documentação de referência</span><span class="sxs-lookup"><span data-stu-id="f0d09-109">Reference documentation</span></span>
<span data-ttu-id="f0d09-110">Olá documentação de referência do SDK do cliente hello está localizada aqui: [referência de cliente .NET de aplicativos móveis do Azure][4].</span><span class="sxs-lookup"><span data-stu-id="f0d09-110">hello reference documentation for hello client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="f0d09-111">Você também pode encontrar vários exemplos de cliente em Olá [repositório GitHub de exemplos do Azure][5].</span><span class="sxs-lookup"><span data-stu-id="f0d09-111">You can also find several client samples in hello [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="f0d09-112">Plataformas com suporte</span><span class="sxs-lookup"><span data-stu-id="f0d09-112">Supported Platforms</span></span>
<span data-ttu-id="f0d09-113">Olá plataforma .NET oferece suporte a saudação plataformas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0d09-113">hello .NET Platform supports hello following platforms:</span></span>

* <span data-ttu-id="f0d09-114">Versões de Xamarin Android para API 19 a 24 (KitKat usando Nougat)</span><span class="sxs-lookup"><span data-stu-id="f0d09-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="f0d09-115">Versões de Xamarin iOS para versões 8.0 e posteriores do iOS</span><span class="sxs-lookup"><span data-stu-id="f0d09-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="f0d09-116">Plataforma Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="f0d09-116">Universal Windows Platform</span></span>
* <span data-ttu-id="f0d09-117">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="f0d09-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="f0d09-118">Windows Phone 8.0, exceto para aplicativos Silverlight</span><span class="sxs-lookup"><span data-stu-id="f0d09-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="f0d09-119">autenticação de "server-fluxo" Hello usa WebView para Olá apresentado da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="f0d09-119">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="f0d09-120">Se o dispositivo de saudação não for capaz de toopresent uma UI WebView, outros métodos de autenticação são necessários.</span><span class="sxs-lookup"><span data-stu-id="f0d09-120">If hello device is not able toopresent a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="f0d09-121">Esse SDK, portanto, não é adequado para relógios ou dispositivos similarmente restritos.</span><span class="sxs-lookup"><span data-stu-id="f0d09-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="f0d09-122"><a name="setup"></a>Configuração e Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f0d09-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="f0d09-123">Supomos que você já criou e publicou o projeto de back-end do Aplicativo Móvel, que inclui pelo menos uma tabela.</span><span class="sxs-lookup"><span data-stu-id="f0d09-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="f0d09-124">No código de saudação usado neste tópico, a tabela de saudação é denominada `TodoItem` e ele tem Olá colunas a seguir: `Id`, `Text`, e `Complete`.</span><span class="sxs-lookup"><span data-stu-id="f0d09-124">In hello code used in this topic, hello table is named `TodoItem` and it has hello following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="f0d09-125">Esta tabela é hello mesma tabela criada quando você concluir o [início rápido de aplicativos do Azure Mobile][1].</span><span class="sxs-lookup"><span data-stu-id="f0d09-125">This table is hello same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="f0d09-126">Olá digitado cliente tipo correspondente no c# é Olá classe a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0d09-126">hello corresponding typed client-side type in C# is hello following class:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

<span data-ttu-id="f0d09-127">Olá [JsonPropertyAttribute] [ 6] é usado toodefine hello *PropertyName* mapeamento entre os campos de cliente hello e Olá tabela.</span><span class="sxs-lookup"><span data-stu-id="f0d09-127">hello [JsonPropertyAttribute][6] is used toodefine hello *PropertyName* mapping between hello client field and hello table field.</span></span>

<span data-ttu-id="f0d09-128">toolearn como toocreate tabelas em seu back-end de aplicativos móveis, consulte Olá [tópico sobre o SDK do .NET Server] [ 7] ou hello [tópico sobre o SDK do servidor Node.js] [ 8] .</span><span class="sxs-lookup"><span data-stu-id="f0d09-128">toolearn how toocreate tables in your Mobile Apps backend, see hello [.NET Server SDK topic][7] or hello [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="f0d09-129">Se você tiver criado seu back-end do aplicativo móvel no hello Azure portal usando Olá início rápido, você também pode usar o hello **tabelas fácil** definindo no hello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="f0d09-129">If you created your Mobile App backend in hello Azure portal using hello QuickStart, you can also use hello **Easy tables** setting in hello [Azure portal].</span></span>

### <a name="how-to-install-hello-managed-client-sdk-package"></a><span data-ttu-id="f0d09-130">Como: instalar Olá gerenciados pacote do SDK de cliente</span><span class="sxs-lookup"><span data-stu-id="f0d09-130">How to: Install hello managed client SDK package</span></span>
<span data-ttu-id="f0d09-131">Usar um dos Olá Olá de tooinstall métodos a seguir gerenciados pacote do SDK de cliente para aplicativos móveis do [NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="f0d09-131">Use one of hello following methods tooinstall hello managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="f0d09-132">**O Visual Studio** seu projeto, clique **gerenciar pacotes NuGet**, pesquise Olá `Microsoft.Azure.Mobile.Client` do pacote e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="f0d09-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="f0d09-133">**Xamarin Studio** seu projeto, clique **adicionar** > **adicionar pacotes do NuGet**, pesquise Olá `Microsoft.Azure.Mobile.Client `do pacote e, em seguida, clique em **adicionar Pacote**.</span><span class="sxs-lookup"><span data-stu-id="f0d09-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="f0d09-134">No arquivo principal de atividade, lembre-se a seguir Olá tooadd **usando** instrução:</span><span class="sxs-lookup"><span data-stu-id="f0d09-134">In your main activity file, remember tooadd hello following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="f0d09-135"><a name="symbolsource"></a>Como trabalhar com símbolos de depuração no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f0d09-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="f0d09-136">símbolos de Olá Olá Microsoft.Azure.Mobile namespace estão disponíveis em [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="f0d09-136">hello symbols for hello Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="f0d09-137">Consulte toothe [SymbolSource instruções] [ 11] toointegrate SymbolSource com o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0d09-137">Refer toothe [SymbolSource instructions][11] toointegrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="f0d09-138"><a name="create-client"></a>Crie saudação do cliente de aplicativos móveis</span><span class="sxs-lookup"><span data-stu-id="f0d09-138"><a name="create-client"></a>Create hello Mobile Apps client</span></span>
<span data-ttu-id="f0d09-139">Olá, código a seguir cria Olá [MobileServiceClient] [ 12] objeto que é usado tooaccess seu back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="f0d09-139">hello following code creates hello [MobileServiceClient][12] object that is used tooaccess your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="f0d09-140">Olá anterior do código, substitua `MOBILE_APP_URL` com URL de saudação do back-end de aplicativo móvel Olá, que se encontra na folha para seu back-end do aplicativo móvel no hello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="f0d09-140">In hello preceding code, replace `MOBILE_APP_URL` with hello URL of hello Mobile App backend, which is found in the blade for your Mobile App backend in hello [Azure portal].</span></span> <span data-ttu-id="f0d09-141">objeto MobileServiceClient de saudação deve ser um singleton.</span><span class="sxs-lookup"><span data-stu-id="f0d09-141">hello MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="f0d09-142">Trabalhar com tabelas</span><span class="sxs-lookup"><span data-stu-id="f0d09-142">Work with Tables</span></span>
<span data-ttu-id="f0d09-143">Olá detalhes da seção a seguir como toosearch e recuperar os registros e modificar dados de saudação na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-143">hello following section details how toosearch and retrieve records and modify hello data within hello table.</span></span>  <span data-ttu-id="f0d09-144">Olá seguintes tópicos é abordado:</span><span class="sxs-lookup"><span data-stu-id="f0d09-144">hello following topics are covered:</span></span>

* [<span data-ttu-id="f0d09-145">Criar uma referência de tabela</span><span class="sxs-lookup"><span data-stu-id="f0d09-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="f0d09-146">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="f0d09-146">Query data</span></span>](#querying)
* [<span data-ttu-id="f0d09-147">Filtrar dados retornados</span><span class="sxs-lookup"><span data-stu-id="f0d09-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="f0d09-148">Classificar dados retornados</span><span class="sxs-lookup"><span data-stu-id="f0d09-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="f0d09-149">Retornar dados em páginas</span><span class="sxs-lookup"><span data-stu-id="f0d09-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="f0d09-150">Selecionar colunas específicas</span><span class="sxs-lookup"><span data-stu-id="f0d09-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="f0d09-151">Pesquisar um registro por ID</span><span class="sxs-lookup"><span data-stu-id="f0d09-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="f0d09-152">Lidando com consultas sem tipo</span><span class="sxs-lookup"><span data-stu-id="f0d09-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="f0d09-153">Inserindo dados</span><span class="sxs-lookup"><span data-stu-id="f0d09-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="f0d09-154">Atualizando dados</span><span class="sxs-lookup"><span data-stu-id="f0d09-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="f0d09-155">Excluindo dados</span><span class="sxs-lookup"><span data-stu-id="f0d09-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="f0d09-156">Resolução de Conflitos e Simultaneidade Otimista</span><span class="sxs-lookup"><span data-stu-id="f0d09-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="f0d09-157">Associação tooa Interface de usuário do Windows</span><span class="sxs-lookup"><span data-stu-id="f0d09-157">Binding tooa Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="f0d09-158">Olá alterar tamanho da página</span><span class="sxs-lookup"><span data-stu-id="f0d09-158">Changing hello Page Size</span></span>](#pagesize)

### <span data-ttu-id="f0d09-159"><a name="instantiating"></a>Como criar uma referência de tabela</span><span class="sxs-lookup"><span data-stu-id="f0d09-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="f0d09-160">Todos os códigos de saudação que acessa ou modificam dados em uma tabela de back-end chama funções em Olá `MobileServiceTable` objeto.</span><span class="sxs-lookup"><span data-stu-id="f0d09-160">All hello code that accesses or modifies data in a backend table calls functions on hello `MobileServiceTable` object.</span></span> <span data-ttu-id="f0d09-161">Obter uma tabela de referência toohello Olá chamada [GetTable] método, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f0d09-161">Obtain a reference toohello table by calling hello [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="f0d09-162">Olá retornou objeto usa o modelo de serialização do tipo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-162">hello returned object uses hello typed serialization model.</span></span> <span data-ttu-id="f0d09-163">Também há suporte para um modelo de serialização não tipado.</span><span class="sxs-lookup"><span data-stu-id="f0d09-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="f0d09-164">O exemplo a seguir [cria uma tabela sem tipo de referência de tooan]:</span><span class="sxs-lookup"><span data-stu-id="f0d09-164">The following example [creates a reference tooan untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="f0d09-165">Consultas sem tipo, você deve especificar Olá subjacente a cadeia de caracteres de consulta OData.</span><span class="sxs-lookup"><span data-stu-id="f0d09-165">In untyped queries, you must specify hello underlying OData query string.</span></span>

### <span data-ttu-id="f0d09-166"><a name="querying"></a>Como consultar dados do seu Aplicativo Móvel</span><span class="sxs-lookup"><span data-stu-id="f0d09-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="f0d09-167">Esta seção descreve como as consultas tooissue toohello aplicativo móvel back-end, que inclui a saudação funcionalidade a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0d09-167">This section describes how tooissue queries toohello Mobile App backend, which includes hello following functionality:</span></span>

* [<span data-ttu-id="f0d09-168">Filtrar dados retornados</span><span class="sxs-lookup"><span data-stu-id="f0d09-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="f0d09-169">Classificar dados retornados</span><span class="sxs-lookup"><span data-stu-id="f0d09-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="f0d09-170">Retornar dados em páginas</span><span class="sxs-lookup"><span data-stu-id="f0d09-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="f0d09-171">Selecionar colunas específicas</span><span class="sxs-lookup"><span data-stu-id="f0d09-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="f0d09-172">Pesquisar dados por ID</span><span class="sxs-lookup"><span data-stu-id="f0d09-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="f0d09-173">Um tamanho de página orientado para servidor é imposta tooprevent todas as linhas sejam retornadas.</span><span class="sxs-lookup"><span data-stu-id="f0d09-173">A server-driven page size is enforced tooprevent all rows from being returned.</span></span>  <span data-ttu-id="f0d09-174">Paginação impede que solicitações de padrão para grandes conjuntos de dados comprometendo o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-174">Paging keeps default requests for large data sets from negatively impacting hello service.</span></span>  <span data-ttu-id="f0d09-175">tooreturn mais de 50 linhas, use Olá `Skip` e `Take` método, conforme descrito em [retornar dados em páginas](#paging).</span><span class="sxs-lookup"><span data-stu-id="f0d09-175">tooreturn more than 50 rows, use hello `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="f0d09-176"><a name="filtering"></a>Como filtrar dados retornados</span><span class="sxs-lookup"><span data-stu-id="f0d09-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="f0d09-177">Olá código a seguir ilustra como dados toofilter, incluindo um `Where` cláusula em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="f0d09-177">hello following code illustrates how toofilter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="f0d09-178">Retorna todos os itens do `todoTable` cujo `Complete` propriedade é igual muito`false`.</span><span class="sxs-lookup"><span data-stu-id="f0d09-178">It returns all items from `todoTable` whose `Complete` property is equal too`false`.</span></span> <span data-ttu-id="f0d09-179">Olá [onde] função aplica uma predicado de consulta de saudação na tabela de saudação de filtragem de linha.</span><span class="sxs-lookup"><span data-stu-id="f0d09-179">hello [Where] function applies a row filtering predicate to hello query against hello table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="f0d09-180">Você pode exibir hello URI de back-end toohello de solicitação enviada hello usando software de inspeção de mensagem, como ferramentas de desenvolvedor do navegador ou [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="f0d09-180">You can view hello URI of hello request sent toohello backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="f0d09-181">Se você observar o URI de solicitação hello, observe que a cadeia de caracteres de consulta de saudação é modificada:</span><span class="sxs-lookup"><span data-stu-id="f0d09-181">If you look at hello request URI, notice that hello query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="f0d09-182">Essa solicitação OData é convertida em uma consulta SQL por Olá SDK do servidor:</span><span class="sxs-lookup"><span data-stu-id="f0d09-182">This OData request is translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="f0d09-183">Olá função que é passada toohello `Where` método pode ter um número arbitrário de condições.</span><span class="sxs-lookup"><span data-stu-id="f0d09-183">hello function that is passed toohello `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="f0d09-184">Este exemplo deve ser convertido em uma consulta SQL por Olá SDK do servidor:</span><span class="sxs-lookup"><span data-stu-id="f0d09-184">This example would be translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="f0d09-185">Essa consulta pode ser dividida em várias cláusulas:</span><span class="sxs-lookup"><span data-stu-id="f0d09-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="f0d09-186">Olá dois métodos são equivalentes e podem ser usados alternadamente.</span><span class="sxs-lookup"><span data-stu-id="f0d09-186">hello two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="f0d09-187">Olá opção&mdash;da concatenação de vários predicados em uma consulta&mdash;é mais compacto e recomendado.</span><span class="sxs-lookup"><span data-stu-id="f0d09-187">hello former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="f0d09-188">Olá `Where` cláusula dá suporte a operações que ser convertido em um subconjunto de OData hello.</span><span class="sxs-lookup"><span data-stu-id="f0d09-188">hello `Where` clause supports operations that be translated into hello OData subset.</span></span> <span data-ttu-id="f0d09-189">As operações incluem:</span><span class="sxs-lookup"><span data-stu-id="f0d09-189">Operations include:</span></span>

* <span data-ttu-id="f0d09-190">Operadores relacionais (==,!=, <, <=, >, >=),</span><span class="sxs-lookup"><span data-stu-id="f0d09-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="f0d09-191">Operadores aritméticos (+, -, /, *, %),</span><span class="sxs-lookup"><span data-stu-id="f0d09-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="f0d09-192">Número de precisão (Math.Floor, Math.Ceiling),</span><span class="sxs-lookup"><span data-stu-id="f0d09-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="f0d09-193">Funções de cadeia de caracteres (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span><span class="sxs-lookup"><span data-stu-id="f0d09-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="f0d09-194">Propriedades de data (ano, mês, dia, hora, minuto, segundo),</span><span class="sxs-lookup"><span data-stu-id="f0d09-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="f0d09-195">Propriedades de acesso de um objeto e</span><span class="sxs-lookup"><span data-stu-id="f0d09-195">Access properties of an object, and</span></span>
* <span data-ttu-id="f0d09-196">Expressões que combinam qualquer uma dessas operações.</span><span class="sxs-lookup"><span data-stu-id="f0d09-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="f0d09-197">Quando considerando o que Olá servidor SDK dá suporte a, você pode considerar Olá [OData v3 documentação].</span><span class="sxs-lookup"><span data-stu-id="f0d09-197">When considering what hello Server SDK supports, you can consider hello [OData v3 Documentation].</span></span>

### <span data-ttu-id="f0d09-198"><a name="sorting"></a>Como classificar dados retornados</span><span class="sxs-lookup"><span data-stu-id="f0d09-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="f0d09-199">Olá código a seguir ilustra como dados toosort, incluindo um [OrderBy] ou [OrderByDescending] função na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-199">hello following code illustrates how toosort data by including an [OrderBy] or [OrderByDescending] function in hello query.</span></span> <span data-ttu-id="f0d09-200">Retorna os itens do `todoTable` classificada em ordem crescente por Olá `Text` campo.</span><span class="sxs-lookup"><span data-stu-id="f0d09-200">It returns items from `todoTable` sorted ascending by hello `Text` field.</span></span>

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <span data-ttu-id="f0d09-201"><a name="paging"></a>Como retornar dados em páginas</span><span class="sxs-lookup"><span data-stu-id="f0d09-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="f0d09-202">Por padrão, Olá back-end retorna apenas Olá primeiras 50 linhas.</span><span class="sxs-lookup"><span data-stu-id="f0d09-202">By default, hello backend returns only hello first 50 rows.</span></span> <span data-ttu-id="f0d09-203">Você pode aumentar o número de saudação de linhas retornados pela chamada hello [levar] método.</span><span class="sxs-lookup"><span data-stu-id="f0d09-203">You can increase hello number of returned rows by calling hello [Take] method.</span></span> <span data-ttu-id="f0d09-204">Use `Take` juntamente com hello [ignorar] método toorequest uma "página específica" do conjunto de dados total Olá retornada pela consulta hello.</span><span class="sxs-lookup"><span data-stu-id="f0d09-204">Use `Take` along with hello [Skip] method toorequest a specific "page" of hello total dataset returned by hello query.</span></span> <span data-ttu-id="f0d09-205">Olá consulta a seguir, quando executada, retorna Olá três principais itens na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-205">hello following query, when executed, returns hello top three items in hello table.</span></span>

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="f0d09-206">ignora a seguinte consulta revisada Olá Olá três primeiros resultados e retorna Olá três resultados.</span><span class="sxs-lookup"><span data-stu-id="f0d09-206">hello following revised query skips hello first three results and returns hello next three results.</span></span> <span data-ttu-id="f0d09-207">Essa consulta gera Olá segunda "página" de dados, onde o tamanho da página Olá é três itens.</span><span class="sxs-lookup"><span data-stu-id="f0d09-207">This query produces hello second "page" of data, where hello page size is three items.</span></span>

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="f0d09-208">Olá [IncludeTotalCount] método solicita a contagem total de saudação para *todos os* Olá registros que teriam sido retornados, ignorando qualquer cláusula de paginação/limite especificada:</span><span class="sxs-lookup"><span data-stu-id="f0d09-208">hello [IncludeTotalCount] method requests hello total count for *all* hello records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="f0d09-209">Em um aplicativo do mundo real, você pode usar consultas toohello semelhante anterior de exemplo com um controle de pager ou a interface de usuário comparável para navegar entre páginas.</span><span class="sxs-lookup"><span data-stu-id="f0d09-209">In a real world app, you can use queries similar toohello preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="f0d09-210">limite de 50 linhas toooverride Olá em um back-end do aplicativo móvel, você deve aplicar Olá [EnableQueryAttribute] toohello público método GET e especifique o comportamento de paginação hello.</span><span class="sxs-lookup"><span data-stu-id="f0d09-210">toooverride hello 50-row limit in a Mobile App backend, you must also apply hello [EnableQueryAttribute] toohello public GET method and specify hello paging behavior.</span></span> <span data-ttu-id="f0d09-211">Quando o método de toohello aplicada, Olá a seguir define too1000 o máximo de linhas retornadas:</span><span class="sxs-lookup"><span data-stu-id="f0d09-211">When applied toohello method, hello following sets the maximum returned rows too1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="f0d09-212"><a name="selecting"></a>Como selecionar colunas específicas</span><span class="sxs-lookup"><span data-stu-id="f0d09-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="f0d09-213">Você pode especificar qual conjunto de propriedades tooinclude em Olá resultados adicionando um [selecione] consulta de tooyour cláusula.</span><span class="sxs-lookup"><span data-stu-id="f0d09-213">You can specify which set of properties tooinclude in hello results by adding a [Select] clause tooyour query.</span></span> <span data-ttu-id="f0d09-214">Olá, por exemplo, o seguinte código mostra como tooselect apenas um campo e também como tooselect e vários campos de formato:</span><span class="sxs-lookup"><span data-stu-id="f0d09-214">For example, hello following code shows how tooselect just one field and also how tooselect and format multiple fields:</span></span>

```
// Select one field -- just hello Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

<span data-ttu-id="f0d09-215">Todos os Olá funções descritas até agora são aditivas, portanto, pode manter encadeamento-los.</span><span class="sxs-lookup"><span data-stu-id="f0d09-215">All hello functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="f0d09-216">Cada chamada encadeada afeta mais consulta hello.</span><span class="sxs-lookup"><span data-stu-id="f0d09-216">Each chained call affects more of hello query.</span></span> <span data-ttu-id="f0d09-217">Mais um exemplo:</span><span class="sxs-lookup"><span data-stu-id="f0d09-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="f0d09-218"><a name="lookingup"></a>Como pesquisar dados pela ID</span><span class="sxs-lookup"><span data-stu-id="f0d09-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="f0d09-219">Olá [LookupAsync] função pode ser usado toolook objetos de banco de dados de saudação com uma ID específica</span><span class="sxs-lookup"><span data-stu-id="f0d09-219">hello [LookupAsync] function can be used toolook up objects from hello database with a particular ID.</span></span>

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="f0d09-220"><a name="untypedqueries"></a>Como executar consultas sem tipo</span><span class="sxs-lookup"><span data-stu-id="f0d09-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="f0d09-221">Ao executar uma consulta usando um objeto de tabela sem tipo, você deve especificar explicitamente a cadeia de caracteres de consulta de OData Olá chamando [ReadAsync], conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f0d09-221">When executing a query using an untyped table object, you must explicitly specify hello OData query string by calling [ReadAsync], as in hello following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="f0d09-222">Você recupera valores JSON que podem ser usados como um recipiente de propriedades.</span><span class="sxs-lookup"><span data-stu-id="f0d09-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="f0d09-223">Para obter mais informações sobre JToken e Newtonsoft Json.NET, consulte Olá [Json.NET] site.</span><span class="sxs-lookup"><span data-stu-id="f0d09-223">For more information on JToken and Newtonsoft Json.NET, see hello [Json.NET] site.</span></span>

### <span data-ttu-id="f0d09-224"><a name="inserting"></a>Como inserir dados em um back-end do Aplicativo Móvel</span><span class="sxs-lookup"><span data-stu-id="f0d09-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="f0d09-225">Todos os tipos de cliente devem conter um membro chamado **Id**, que é por padrão uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f0d09-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="f0d09-226">Isso **Id** é necessário para executar operações CRUD e para sincronização offline. Olá código a seguir ilustra como Olá toouse [InsertAsync] método tooinsert novas linhas em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="f0d09-226">This **Id** is required to perform CRUD operations and for offline sync. hello following code illustrates how toouse hello [InsertAsync] method tooinsert new rows into a table.</span></span> <span data-ttu-id="f0d09-227">parâmetro Hello contém Olá dados toobe inserido como um objeto .NET.</span><span class="sxs-lookup"><span data-stu-id="f0d09-227">hello parameter contains hello data toobe inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="f0d09-228">Se um valor de ID exclusivo personalizado não será incluído no hello `todoItem` durante uma inserção, um GUID gerado pelo servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-228">If a unique custom ID value is not included in hello `todoItem` during an insert, a GUID is generated by hello server.</span></span>
<span data-ttu-id="f0d09-229">Você pode recuperar Olá Id gerada inspecionando o objeto Olá depois Olá chamada retorna.</span><span class="sxs-lookup"><span data-stu-id="f0d09-229">You can retrieve hello generated Id by inspecting hello object after hello call returns.</span></span>

<span data-ttu-id="f0d09-230">tooinsert sem tipo de dados, você pode tirar proveito do Json.NET:</span><span class="sxs-lookup"><span data-stu-id="f0d09-230">tooinsert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="f0d09-231">Aqui está um exemplo usando um endereço de email como uma id de cadeia de caracteres exclusiva:</span><span class="sxs-lookup"><span data-stu-id="f0d09-231">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="f0d09-232">Trabalhando com valores de ID</span><span class="sxs-lookup"><span data-stu-id="f0d09-232">Working with ID values</span></span>
<span data-ttu-id="f0d09-233">Aplicativos móveis dá suporte a valores de cadeia de caracteres personalizada exclusivo para a tabela de saudação **id** coluna.</span><span class="sxs-lookup"><span data-stu-id="f0d09-233">Mobile Apps supports unique custom string values for hello table's **id** column.</span></span> <span data-ttu-id="f0d09-234">Um valor de cadeia de caracteres permite que aplicativos toouse de valores personalizados, como endereços de email ou nomes de usuário para ID de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-234">A string value allows applications toouse custom values such as email addresses or user names for hello ID.</span></span>  <span data-ttu-id="f0d09-235">IDs de cadeia de caracteres fornecem Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0d09-235">String IDs provide you with hello following benefits:</span></span>

* <span data-ttu-id="f0d09-236">IDs são gerados sem fazer um banco de dados de toohello de ida e volta.</span><span class="sxs-lookup"><span data-stu-id="f0d09-236">IDs are generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="f0d09-237">Os registros são toomerge mais fácil de tabelas diferentes ou bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="f0d09-237">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="f0d09-238">Os valores de IDs podem integrar-se melhor a uma lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0d09-238">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="f0d09-239">Quando um valor de ID de cadeia de caracteres não está definido em um registro inserido, o back-end de aplicativo móvel hello gera um valor exclusivo para a ID.</span><span class="sxs-lookup"><span data-stu-id="f0d09-239">When a string ID value is not set on an inserted record, hello Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="f0d09-240">Você pode usar o hello [Guid.NewGuid] toogenerate método sua própria ID de valores, no cliente de saudação ou em Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="f0d09-240">You can use hello [Guid.NewGuid] method toogenerate your own ID values, either on hello client or in hello backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="f0d09-241"><a name="modifying"></a>Como modificar dados em um back-end de Aplicativo Móvel</span><span class="sxs-lookup"><span data-stu-id="f0d09-241"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="f0d09-242">Olá código a seguir ilustra como Olá toouse [UpdateAsync] método tooupdate um registro existente com hello mesmo ID com novas informações.</span><span class="sxs-lookup"><span data-stu-id="f0d09-242">hello following code illustrates how toouse hello [UpdateAsync] method tooupdate an existing record with hello same ID with new information.</span></span> <span data-ttu-id="f0d09-243">parâmetro Hello contém Olá dados toobe atualizada como um objeto .NET.</span><span class="sxs-lookup"><span data-stu-id="f0d09-243">hello parameter contains hello data toobe updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="f0d09-244">tooupdate sem tipo de dados, você pode tirar proveito do [Json.NET] da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f0d09-244">tooupdate untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="f0d09-245">Um campo `id` deve ser especificado ao fazer uma atualização.</span><span class="sxs-lookup"><span data-stu-id="f0d09-245">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="f0d09-246">Olá back-end usa Olá `id` tooidentify campo qual linha tooupdate.</span><span class="sxs-lookup"><span data-stu-id="f0d09-246">hello backend uses hello `id` field tooidentify which row tooupdate.</span></span> <span data-ttu-id="f0d09-247">Olá `id` campo pode ser obtido dos resultados de saudação do hello `InsertAsync` chamar.</span><span class="sxs-lookup"><span data-stu-id="f0d09-247">hello `id` field can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="f0d09-248">Um `ArgumentException` é gerado se você tentar tooupdate um item sem fornecer Olá `id` valor.</span><span class="sxs-lookup"><span data-stu-id="f0d09-248">An `ArgumentException` is raised if you try tooupdate an item without providing hello `id` value.</span></span>

### <span data-ttu-id="f0d09-249"><a name="deleting"></a>Como excluir dados em um back-end do Aplicativo Móvel</span><span class="sxs-lookup"><span data-stu-id="f0d09-249"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="f0d09-250">Olá código a seguir ilustra como Olá toouse [DeleteAsync] método toodelete uma instância existente.</span><span class="sxs-lookup"><span data-stu-id="f0d09-250">hello following code illustrates how toouse hello [DeleteAsync] method toodelete an existing instance.</span></span> <span data-ttu-id="f0d09-251">Olá instância é identificada por Olá `id` campo de conjunto de saudação `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="f0d09-251">hello instance is identified by hello `id` field set on hello `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="f0d09-252">toodelete sem tipo de dados, você pode tirar proveito do Json.NET da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f0d09-252">toodelete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="f0d09-253">Quando você faz uma solicitação de exclusão, uma ID deve ser especificada.</span><span class="sxs-lookup"><span data-stu-id="f0d09-253">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="f0d09-254">Outras propriedades não são passadas para o serviço de toohello ou são ignoradas no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-254">Other properties are not passed toohello service or are ignored at hello service.</span></span> <span data-ttu-id="f0d09-255">Olá o resultado de uma `DeleteAsync` costuma ser chamada `null`.</span><span class="sxs-lookup"><span data-stu-id="f0d09-255">hello result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="f0d09-256">Olá ID toopass no pode ser obtido de resultado de saudação da saudação `InsertAsync` chamar.</span><span class="sxs-lookup"><span data-stu-id="f0d09-256">hello ID toopass in can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="f0d09-257">Um `MobileServiceInvalidOperationException` é gerada quando você tentar toodelete um item sem especificar Olá `id` campo.</span><span class="sxs-lookup"><span data-stu-id="f0d09-257">A `MobileServiceInvalidOperationException` is thrown when you try toodelete an item without specifying hello `id` field.</span></span>

### <span data-ttu-id="f0d09-258"><a name="optimisticconcurrency"></a>Como usar a simultaneidade otimista para resolução de conflitos</span><span class="sxs-lookup"><span data-stu-id="f0d09-258"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="f0d09-259">Dois ou mais clientes podem gravar alterações toohello mesmo item no hello mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="f0d09-259">Two or more clients may write changes toohello same item at hello same time.</span></span> <span data-ttu-id="f0d09-260">Sem detecção de conflito, a última gravação do hello substituiria todas as atualizações anteriores.</span><span class="sxs-lookup"><span data-stu-id="f0d09-260">Without conflict detection, hello last write would overwrite any previous updates.</span></span> <span data-ttu-id="f0d09-261">**Controle de simultaneidade otimista** pressupõe que cada transação possa ser confirmada e, portanto, não usa nenhum recurso de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="f0d09-261">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="f0d09-262">Antes de confirmar uma transação, o controle de simultaneidade otimista verifica que nenhuma outra transação ter modificado os dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-262">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified hello data.</span></span> <span data-ttu-id="f0d09-263">Se dados saudação tem sido modificados, Olá confirmando a transação será revertida.</span><span class="sxs-lookup"><span data-stu-id="f0d09-263">If hello data has been modified, hello committing transaction is rolled back.</span></span>

<span data-ttu-id="f0d09-264">Aplicativos móveis dá suporte ao controle de simultaneidade otimista rastreando o item de tooeach de alterações usando Olá `version` coluna de propriedade do sistema que é definida para cada tabela em seu back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="f0d09-264">Mobile Apps supports optimistic concurrency control by tracking changes tooeach item using hello `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="f0d09-265">Cada vez que um registro é atualizado, os aplicativos móveis define Olá `version` propriedade para que registre tooa novo valor.</span><span class="sxs-lookup"><span data-stu-id="f0d09-265">Each time a record is updated, Mobile Apps sets hello `version` property for that record tooa new value.</span></span> <span data-ttu-id="f0d09-266">Durante cada solicitação de atualização, Olá `version` propriedade de registro de saudação incluído na solicitação de saudação é toohello em comparação com o mesma propriedade de registro de saudação no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-266">During each update request, hello `version` property of hello record included with hello request is compared toohello same property for hello record on hello server.</span></span> <span data-ttu-id="f0d09-267">Se a versão passada com hello solicitação não corresponde a saudação back-end, biblioteca de saudação do cliente gera um `MobileServicePreconditionFailedException<T>` exceção.</span><span class="sxs-lookup"><span data-stu-id="f0d09-267">If the version passed with hello request does not match hello backend, then hello client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="f0d09-268">tipo de saudação incluído com a exceção de saudação é registro Olá Olá versão back-end que contém Olá servidores de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-268">hello type included with hello exception is hello record from hello backend containing hello servers version of hello record.</span></span> <span data-ttu-id="f0d09-269">Olá aplicativo pode usar este toodecide informações se solicitação de atualização de saudação tooexecute novamente com hello correto `version` valor de alterações de toocommit de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-269">hello application can then use this information toodecide whether tooexecute hello update request again with hello correct `version` value from hello backend toocommit changes.</span></span>

<span data-ttu-id="f0d09-270">Definir uma coluna na classe de tabela Olá para Olá `version` simultaneidade otimista de tooenable de propriedade de sistema.</span><span class="sxs-lookup"><span data-stu-id="f0d09-270">Define a column on hello table class for hello `version` system property tooenable optimistic concurrency.</span></span> <span data-ttu-id="f0d09-271">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f0d09-271">For example:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

<span data-ttu-id="f0d09-272">Aplicativos que usam tabelas sem tipo habilitar simultaneidade otimista por configuração Olá `Version` sinalizador no `SystemProperties` de saudação de tabela da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="f0d09-272">Applications using untyped tables enable optimistic concurrency by setting hello `Version` flag on the `SystemProperties` of hello table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="f0d09-273">Em adição tooenabling a simultaneidade otimista, você deve também captura Olá `MobileServicePreconditionFailedException<T>` exceção em seu código ao chamar [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="f0d09-273">In addition tooenabling optimistic concurrency, you must also catch hello `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="f0d09-274">Resolva o conflito de saudação aplicando Olá correto `version` toothe atualizou o registro e chamada [UpdateAsync] com hello resolveu o registro.</span><span class="sxs-lookup"><span data-stu-id="f0d09-274">Resolve hello conflict by applying hello correct `version` toothe updated record and call [UpdateAsync] with hello resolved record.</span></span> <span data-ttu-id="f0d09-275">saudação de código a seguir mostra como tooresolve um conflito de gravação uma vez detectado:</span><span class="sxs-lookup"><span data-stu-id="f0d09-275">hello following code shows how tooresolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="f0d09-276">Para obter mais informações, consulte Olá [sincronização de dados Offline em aplicativos móveis do Azure] tópico.</span><span class="sxs-lookup"><span data-stu-id="f0d09-276">For more information, see hello [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="f0d09-277"><a name="binding"></a>Como: interface de usuário do Windows de tooa de dados de aplicativos móveis de ligação</span><span class="sxs-lookup"><span data-stu-id="f0d09-277"><a name="binding"></a>How to: Bind Mobile Apps data tooa Windows user interface</span></span>
<span data-ttu-id="f0d09-278">Esta seção mostra como toodisplay retornados objetos de dados usando os elementos de interface do usuário em um aplicativo do Windows.</span><span class="sxs-lookup"><span data-stu-id="f0d09-278">This section shows how toodisplay returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="f0d09-279">O exemplo de código a seguir associa toohello fonte da lista de saudação com uma consulta para itens incompletos.</span><span class="sxs-lookup"><span data-stu-id="f0d09-279">The following example code binds toohello source of hello list with a query for incomplete items.</span></span> <span data-ttu-id="f0d09-280">O [MobileServiceCollection] cria uma coleção de associações com reconhecimento de Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="f0d09-280">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="f0d09-281">Alguns controles em Olá gerenciados suporte de tempo de execução chamada de uma interface [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="f0d09-281">Some controls in hello managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="f0d09-282">Essa interface permite que os controles toorequest dados extras ao usuário Olá rolar.</span><span class="sxs-lookup"><span data-stu-id="f0d09-282">This interface allows controls toorequest extra data when hello user scrolls.</span></span> <span data-ttu-id="f0d09-283">Não há suporte interno para esta interface para aplicativos universais do Windows por meio de [MobileServiceIncrementalLoadingCollection], que controla automaticamente as chamadas de controles de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-283">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from hello controls.</span></span> <span data-ttu-id="f0d09-284">Use `MobileServiceIncrementalLoadingCollection` em aplicativos do Windows, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f0d09-284">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="f0d09-285">toouse Olá nova coleção de aplicativos do Windows Phone 8 e "Silverlight", use Olá `ToCollection` métodos de extensão em `IMobileServiceTableQuery<T>` e `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="f0d09-285">toouse hello new collection on Windows Phone 8 and "Silverlight" apps, use hello `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="f0d09-286">dados de tooload, chame `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="f0d09-286">tooload data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="f0d09-287">Quando você usa a coleção de saudação criada chamando `ToCollectionAsync` ou `ToCollection`, você obtém uma coleção que pode ser associado tooUI controles.</span><span class="sxs-lookup"><span data-stu-id="f0d09-287">When you use hello collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound tooUI controls.</span></span>  <span data-ttu-id="f0d09-288">Essa coleção tem reconhecimento de paginação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-288">This collection is paging-aware.</span></span>  <span data-ttu-id="f0d09-289">Desde que a coleção de saudação está carregando os dados da rede, às vezes, há falha no carregamento.</span><span class="sxs-lookup"><span data-stu-id="f0d09-289">Since hello collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="f0d09-290">toohandle essas falhas, substituir Olá `OnException` método `MobileServiceIncrementalLoadingCollection` toohandle exceções resultantes de chamadas muito`LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="f0d09-290">toohandle such failures, override hello `OnException` method on `MobileServiceIncrementalLoadingCollection` toohandle exceptions resulting from calls too`LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="f0d09-291">Considere se sua tabela possui muitos campos, mas deseja toodisplay apenas algumas no seu controle.</span><span class="sxs-lookup"><span data-stu-id="f0d09-291">Consider if your table has many fields but you only want toodisplay some of them in your control.</span></span> <span data-ttu-id="f0d09-292">Você poderá usar orientação Olá Olá anterior a seção "[selecionar colunas específicas](#selecting)" tooselect toodisplay de colunas específicas em Olá da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="f0d09-292">You may use hello guidance in hello preceding section "[Select specific columns](#selecting)" tooselect specific columns toodisplay in hello UI.</span></span>

### <span data-ttu-id="f0d09-293"><a name="pagesize"></a>Saudação de alterar o tamanho de página</span><span class="sxs-lookup"><span data-stu-id="f0d09-293"><a name="pagesize"></a>Change hello Page size</span></span>
<span data-ttu-id="f0d09-294">Os Aplicativos Móveis do Azure retornam, no máximo, 50 itens por solicitação por padrão.</span><span class="sxs-lookup"><span data-stu-id="f0d09-294">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="f0d09-295">Você pode alterar o tamanho de paginação Olá aumentando o tamanho máximo da página de saudação em Olá cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="f0d09-295">You can change hello paging size by increasing hello maximum page size on both hello client and server.</span></span>  <span data-ttu-id="f0d09-296">tooincrease Olá tamanho da página solicitada, especificar `PullOptions` ao usar `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="f0d09-296">tooincrease hello requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="f0d09-297">Supondo que você fez Olá `PageSize` tooor igual maior que 100 no servidor de saudação, uma solicitação retorna até 100 itens.</span><span class="sxs-lookup"><span data-stu-id="f0d09-297">Assuming you have made hello `PageSize` equal tooor greater than 100 within hello server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="f0d09-298"><a name="#offlinesync"></a>Trabalhar com tabelas offline</span><span class="sxs-lookup"><span data-stu-id="f0d09-298"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="f0d09-299">Tabelas offline usam um local SQLite armazenar toostore dados para uso quando estiver offline.</span><span class="sxs-lookup"><span data-stu-id="f0d09-299">Offline tables use a local SQLite store toostore data for use when offline.</span></span>  <span data-ttu-id="f0d09-300">Tabela de todas as operações são feitas em relação a saudação SQLite local armazenar em vez de armazenamento de servidor remoto hello.</span><span class="sxs-lookup"><span data-stu-id="f0d09-300">All table operations are done against hello local SQLite store instead of hello remote server store.</span></span>  <span data-ttu-id="f0d09-301">toocreate uma tabela offline, primeiro prepare seu projeto:</span><span class="sxs-lookup"><span data-stu-id="f0d09-301">toocreate an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="f0d09-302">No Visual Studio, clique com botão direito solução hello > **gerenciar pacotes NuGet para solução...** , em seguida, procurar e instalar o **Microsoft.Azure.Mobile.Client.SQLiteStore** pacote NuGet para todos os projetos na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-302">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="f0d09-303">Dispositivos do Windows toosupport (opcional), instale um dos Olá SQLite pacotes de tempo de execução a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0d09-303">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="f0d09-304">**Tempo de Execução do Windows 8.1**: instale o [SQLite para Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="f0d09-304">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="f0d09-305">**Windows Phone 8.1**: instale o [SQLite para Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="f0d09-305">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="f0d09-306">**Plataforma universal do Windows** instalar [SQLite para Olá Universal do Windows][5].</span><span class="sxs-lookup"><span data-stu-id="f0d09-306">**Universal Windows Platform** Install [SQLite for hello Universal Windows][5].</span></span>
3. <span data-ttu-id="f0d09-307">(Opcional).</span><span class="sxs-lookup"><span data-stu-id="f0d09-307">(Optional).</span></span> <span data-ttu-id="f0d09-308">Para dispositivos do Windows, clique em **referências** > **adicionar referência...** , expanda Olá **Windows** pasta > **extensões**, habilite Olá apropriado **SQLite para Windows** SDK junto com hello  **Visual C++ 2013 em tempo de execução para o Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="f0d09-308">For Windows devices, click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**, then enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="f0d09-309">Hello nomes SQLite SDK variam ligeiramente em cada plataforma do Windows.</span><span class="sxs-lookup"><span data-stu-id="f0d09-309">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="f0d09-310">Antes de uma referência de tabela pode ser criada, deve ser preparado repositório local hello:</span><span class="sxs-lookup"><span data-stu-id="f0d09-310">Before a table reference can be created, hello local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="f0d09-311">Inicialização do repositório normalmente é feita imediatamente após o cliente Olá é criado.</span><span class="sxs-lookup"><span data-stu-id="f0d09-311">Store initialization is normally done immediately after hello client is created.</span></span>  <span data-ttu-id="f0d09-312">Olá **OfflineDbPath** deve ser um nome de arquivo adequado para uso em todas as plataformas que você oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="f0d09-312">hello **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="f0d09-313">Se o caminho de saudação é um caminho totalmente qualificado (ou seja, ele começa com uma barra), em seguida, ele será usado.</span><span class="sxs-lookup"><span data-stu-id="f0d09-313">If hello path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="f0d09-314">Se o caminho de saudação não está totalmente qualificado, o arquivo de saudação é colocado em um local específico da plataforma.</span><span class="sxs-lookup"><span data-stu-id="f0d09-314">If hello path is not fully qualified, hello file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="f0d09-315">Para dispositivos iOS e Android, o caminho de padrão de saudação é hello "pessoal pasta"arquivos.</span><span class="sxs-lookup"><span data-stu-id="f0d09-315">For iOS and Android devices, hello default path is hello "Personal Files" folder.</span></span>
* <span data-ttu-id="f0d09-316">Para dispositivos do Windows, o caminho de padrão de saudação é pasta de "AppData" hello específicas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0d09-316">For Windows devices, hello default path is hello application-specific "AppData" folder.</span></span>

<span data-ttu-id="f0d09-317">Uma referência de tabela pode ser obtida usando Olá `GetSyncTable<>` método:</span><span class="sxs-lookup"><span data-stu-id="f0d09-317">A table reference can be obtained using hello `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="f0d09-318">Não é necessário tooauthenticate toouse uma tabela offline.</span><span class="sxs-lookup"><span data-stu-id="f0d09-318">You do not need tooauthenticate toouse an offline table.</span></span>  <span data-ttu-id="f0d09-319">Você só precisa tooauthenticate quando você está se comunicando com o serviço de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-319">You only need tooauthenticate when you are communicating with hello backend service.</span></span>

### <span data-ttu-id="f0d09-320"><a name="syncoffline"></a>Sincronizando uma tabela Offline</span><span class="sxs-lookup"><span data-stu-id="f0d09-320"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="f0d09-321">Tabelas offline não são sincronizadas com hello back-end por padrão.</span><span class="sxs-lookup"><span data-stu-id="f0d09-321">Offline tables are not synchronized with hello backend by default.</span></span>  <span data-ttu-id="f0d09-322">A sincronização é dividida em duas partes.</span><span class="sxs-lookup"><span data-stu-id="f0d09-322">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="f0d09-323">Você pode enviar alterações separadamente de download de novos itens.</span><span class="sxs-lookup"><span data-stu-id="f0d09-323">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="f0d09-324">Este é um método de sincronização típico:</span><span class="sxs-lookup"><span data-stu-id="f0d09-324">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
            //Use a different query name for each unique query in your program
            "allTodoItems",
            this.todoTable.CreateQuery());
    }
    catch (MobileServicePushFailedException exc)
    {
        if (exc.PushResult != null)
        {
            syncErrors = exc.PushResult.Errors;
        }
    }

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting tooserver's copy.
                await error.CancelAndUpdateItemAsync(error.Result);
            }
            else
            {
                // Discard local change.
                await error.CancelAndDiscardItemAsync();
            }

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

<span data-ttu-id="f0d09-325">Se Olá primeiro argumento muito`PullAsync` for nulo, a sincronização incremental não é usado.</span><span class="sxs-lookup"><span data-stu-id="f0d09-325">If hello first argument too`PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="f0d09-326">Todas as operações de sincronização recuperam todos os registros.</span><span class="sxs-lookup"><span data-stu-id="f0d09-326">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="f0d09-327">Olá SDK executa implícita `PushAsync()` antes de extrair os registros.</span><span class="sxs-lookup"><span data-stu-id="f0d09-327">hello SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="f0d09-328">Manipulação de conflito ocorre em um método `PullAsync()`.</span><span class="sxs-lookup"><span data-stu-id="f0d09-328">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="f0d09-329">Pode lidar com conflitos no hello mesma maneira que as tabelas online.</span><span class="sxs-lookup"><span data-stu-id="f0d09-329">You can deal with conflicts in hello same way as online tables.</span></span>  <span data-ttu-id="f0d09-330">conflito de saudação é produzido quando `PullAsync()` é chamado em vez de durante a saudação insert, update ou delete.</span><span class="sxs-lookup"><span data-stu-id="f0d09-330">hello conflict is produced when `PullAsync()` is called instead of during hello insert, update, or delete.</span></span> <span data-ttu-id="f0d09-331">Se vários conflitos ocorrerem, eles serão agrupados em uma única MobileServicePushFailedException.</span><span class="sxs-lookup"><span data-stu-id="f0d09-331">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="f0d09-332">Gerenciar cada falha separadamente.</span><span class="sxs-lookup"><span data-stu-id="f0d09-332">Handle each failure separately.</span></span>

## <span data-ttu-id="f0d09-333"><a name="#customapi"></a>Trabalhar com uma API personalizada</span><span class="sxs-lookup"><span data-stu-id="f0d09-333"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="f0d09-334">Uma API personalizada permite que você toodefine pontos de extremidade personalizados que expõem a funcionalidade do servidor que não mapeiam tooan inserir, atualizar, excluir ou operação de leitura.</span><span class="sxs-lookup"><span data-stu-id="f0d09-334">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="f0d09-335">Usando uma API personalizada, você pode ter mais controle sobre mensagens, incluindo ler e definir cabeçalhos de mensagens HTTP e definir um formato de corpo de mensagem diferente do JSON.</span><span class="sxs-lookup"><span data-stu-id="f0d09-335">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="f0d09-336">Chamar uma API personalizada chamando uma saudação [InvokeApiAsync] métodos no cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-336">You call a custom API by calling one of hello [InvokeApiAsync] methods on hello client.</span></span> <span data-ttu-id="f0d09-337">Por exemplo, Olá linha de código a seguir envia um toohello de solicitação POST **completeAll** API em Olá back-end:</span><span class="sxs-lookup"><span data-stu-id="f0d09-337">For example, hello following line of code sends a POST request toohello **completeAll** API on hello backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="f0d09-338">Este formulário é uma chamada de método com tipo e requer que Olá **MarkAllResult** retornar o tipo é definido.</span><span class="sxs-lookup"><span data-stu-id="f0d09-338">This form is a typed method call and requires that hello **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="f0d09-339">Os dois métodos, tipado e não tipado, são aceitos.</span><span class="sxs-lookup"><span data-stu-id="f0d09-339">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="f0d09-340">Olá InvokeApiAsync() método precede '/ api /' toohello API que você deseja toocall, a menos que Olá API começa com um '/'.</span><span class="sxs-lookup"><span data-stu-id="f0d09-340">hello InvokeApiAsync() method prepends '/api/' toohello API that you wish toocall unless hello API starts with a '/'.</span></span>
<span data-ttu-id="f0d09-341">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f0d09-341">For example:</span></span>

* <span data-ttu-id="f0d09-342">`InvokeApiAsync("completeAll",...)`chama /api/completeAll Olá back-end</span><span class="sxs-lookup"><span data-stu-id="f0d09-342">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on hello backend</span></span>
* <span data-ttu-id="f0d09-343">`InvokeApiAsync("/.auth/me",...)`chama /.auth/me Olá back-end</span><span class="sxs-lookup"><span data-stu-id="f0d09-343">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on hello backend</span></span>

<span data-ttu-id="f0d09-344">Você pode usar InvokeApiAsync toocall qualquer WebAPI, incluindo os que não estão definidas WebAPIs com aplicativos móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0d09-344">You can use InvokeApiAsync toocall any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="f0d09-345">Quando você usa InvokeApiAsync(), os cabeçalhos apropriados de hello, incluindo os cabeçalhos de autenticação, são enviados com a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-345">When you use InvokeApiAsync(), hello appropriate headers, including authentication headers, are sent with hello request.</span></span>

## <span data-ttu-id="f0d09-346"><a name="authentication"></a>Autenticar usuários</span><span class="sxs-lookup"><span data-stu-id="f0d09-346"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="f0d09-347">Os Aplicativos Móveis dão suporte à autenticação e à autorização de usuários de aplicativo, usando vários provedores de identidade externos: Facebook, Google, Conta da Microsoft, Twitter e o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f0d09-347">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="f0d09-348">Você pode definir permissões de acesso a tabelas toorestrict para operações específicas de tooonly autenticado usuários.</span><span class="sxs-lookup"><span data-stu-id="f0d09-348">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="f0d09-349">Você também pode usar a identidade Olá usuários autenticados tooimplement de regras de autorização nos scripts de servidor.</span><span class="sxs-lookup"><span data-stu-id="f0d09-349">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="f0d09-350">Para obter mais informações, consulte o tutorial Olá [adicionar autenticação tooyour aplicativo].</span><span class="sxs-lookup"><span data-stu-id="f0d09-350">For more information, see hello tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="f0d09-351">Dois fluxos de autenticação têm suporte: fluxo *gerenciado pelo cliente* e fluxo *gerenciado pelo servidor*.</span><span class="sxs-lookup"><span data-stu-id="f0d09-351">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="f0d09-352">fluxo gerenciado pelo servidor de saudação fornece experiência de autenticação mais simples de Olá, como ele se baseia na interface de autenticação do provedor de saudação da web.</span><span class="sxs-lookup"><span data-stu-id="f0d09-352">hello server-managed flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="f0d09-353">fluxo de cliente gerenciado Olá permite integração mais profunda com recursos específicos do dispositivo como depende dos SDKs de específico do dispositivo específico do provedor.</span><span class="sxs-lookup"><span data-stu-id="f0d09-353">hello client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="f0d09-354">Recomendamos o uso de um fluxo gerenciado pelo cliente em seus aplicativos de produção.</span><span class="sxs-lookup"><span data-stu-id="f0d09-354">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="f0d09-355">tooset a autenticação, você deve registrar seu aplicativo com um ou mais provedores de identidade.</span><span class="sxs-lookup"><span data-stu-id="f0d09-355">tooset up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="f0d09-356">provedor de identidade Hello gera uma ID de cliente e um segredo do cliente para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0d09-356">hello identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="f0d09-357">Esses valores, em seguida, são definidos no seu tooenable de back-end do serviço de aplicativo do Azure autenticação/autorização.</span><span class="sxs-lookup"><span data-stu-id="f0d09-357">These values are then set in your backend tooenable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="f0d09-358">Para obter mais informações, execute as instruções detalhadas de saudação do tutorial [adicionar autenticação tooyour aplicativo].</span><span class="sxs-lookup"><span data-stu-id="f0d09-358">For more information, follow hello detailed instructions in the tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="f0d09-359">Olá seguintes tópicos é abordado nesta seção:</span><span class="sxs-lookup"><span data-stu-id="f0d09-359">hello following topics are covered in this section:</span></span>

* [<span data-ttu-id="f0d09-360">Autenticação gerenciada pelo cliente</span><span class="sxs-lookup"><span data-stu-id="f0d09-360">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="f0d09-361">Autenticação gerenciada pelo servidor</span><span class="sxs-lookup"><span data-stu-id="f0d09-361">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="f0d09-362">Token de autenticação do cache Olá</span><span class="sxs-lookup"><span data-stu-id="f0d09-362">Caching hello authentication token</span></span>](#caching)

### <span data-ttu-id="f0d09-363"><a name="clientflow"></a>Autenticação gerenciada pelo cliente</span><span class="sxs-lookup"><span data-stu-id="f0d09-363"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="f0d09-364">Seu aplicativo pode independentemente entre em contato com o provedor de identidade hello e forneça token retornado Olá durante o logon com seu back-end.</span><span class="sxs-lookup"><span data-stu-id="f0d09-364">Your app can independently contact hello identity provider and then provide hello returned token during login with your backend.</span></span> <span data-ttu-id="f0d09-365">Esse fluxo de cliente permite que você tooprovide uma experiência de logon único para usuários ou dados de usuário adicionais tooretrieve saudação do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="f0d09-365">This client flow enables you tooprovide a single sign-on experience for users or tooretrieve additional user data from hello identity provider.</span></span> <span data-ttu-id="f0d09-366">Autenticação de cliente de fluxo é preferencial toousing um fluxo de servidor como o provedor de identidade Olá SDK fornece uma aparência UX mais nativa e permite a personalização adicional.</span><span class="sxs-lookup"><span data-stu-id="f0d09-366">Client flow authentication is preferred toousing a server flow as hello identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="f0d09-367">Exemplos são fornecidos para Olá padrões de autenticação de cliente de fluxo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0d09-367">Examples are provided for hello following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="f0d09-368">Biblioteca de Autenticação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0d09-368">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="f0d09-369">Facebook ou Google</span><span class="sxs-lookup"><span data-stu-id="f0d09-369">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="f0d09-370">Live SDK</span><span class="sxs-lookup"><span data-stu-id="f0d09-370">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="f0d09-371"><a name="adal"></a>Autenticar usuários com hello biblioteca de autenticação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0d09-371"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="f0d09-372">Você pode usar a autenticação de usuário de tooinitiate de biblioteca de autenticação do Active Directory (ADAL) de saudação do cliente hello usando a autenticação do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0d09-372">You can use hello Active Directory Authentication Library (ADAL) tooinitiate user authentication from hello client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="f0d09-373">Configurar seu back-end do aplicativo móvel para o logon do AAD pela seguinte Olá [como tooconfigure aplicativo de serviço de logon do Active Directory] tutorial.</span><span class="sxs-lookup"><span data-stu-id="f0d09-373">Configure your mobile app backend for AAD sign-on by following hello [How tooconfigure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="f0d09-374">Torne-se toocomplete Olá opcional de registro de um aplicativo cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="f0d09-374">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="f0d09-375">No Visual Studio ou no Xamarin Studio, abra seu projeto e adicione uma referência toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="f0d09-375">In Visual Studio or Xamarin Studio, open your project and add a reference toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="f0d09-376">Ao pesquisar, inclua versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="f0d09-376">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="f0d09-377">Adicione Olá aplicativo tooyour de código a seguir, de acordo com a plataforma toohello que você está usando.</span><span class="sxs-lookup"><span data-stu-id="f0d09-377">Add hello following code tooyour application, according toohello platform you are using.</span></span> <span data-ttu-id="f0d09-378">Em cada um, verifique Olá substituições a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0d09-378">In each, make hello following replacements:</span></span>

   * <span data-ttu-id="f0d09-379">Substituir **aqui de autoridade de inserção** com o nome de saudação do locatário Olá no qual você provisionou o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0d09-379">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="f0d09-380">O formato deve ser https://login.microsoftonline.com/contoso.onmicrosoft.com. Esse valor pode ser copiado de guia de saudação do domínio no Active Directory do Azure no hello [portal clássico do Azure].</span><span class="sxs-lookup"><span data-stu-id="f0d09-380">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="f0d09-381">Substituir **inserir recursos-ID aqui** com a ID de cliente Olá para o back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="f0d09-381">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="f0d09-382">Você pode obter a ID do cliente Olá de Olá **avançado** guia **configurações do Active Directory do Azure** no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-382">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="f0d09-383">Substituir **aqui INSERT-CLIENT-ID** com a ID de cliente Olá você copiou do aplicativo cliente nativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-383">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="f0d09-384">Substituir **INSERT-REDIRECT-URI-aqui** com seu site */.auth/login/done* ponto de extremidade, usando o esquema do hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f0d09-384">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="f0d09-385">Esse valor deve ser semelhante muito*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="f0d09-385">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="f0d09-386">código de saudação necessário para cada plataforma segue:</span><span class="sxs-lookup"><span data-stu-id="f0d09-386">hello code needed for each platform follows:</span></span>

     <span data-ttu-id="f0d09-387">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="f0d09-387">**Windows:**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     <span data-ttu-id="f0d09-388">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="f0d09-388">**Xamarin.iOS**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     <span data-ttu-id="f0d09-389">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="f0d09-389">**Xamarin.Android**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <span data-ttu-id="f0d09-390"><a name="client-facebook"></a>Entrada única usando um token do Facebook ou do Google</span><span class="sxs-lookup"><span data-stu-id="f0d09-390"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="f0d09-391">Você pode usar fluxo de saudação do cliente, conforme mostrado neste trecho para o Facebook ou Google.</span><span class="sxs-lookup"><span data-stu-id="f0d09-391">You can use hello client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <span data-ttu-id="f0d09-392"><a name="client-livesdk"></a>O logon único usando Microsoft Account com hello Live SDK</span><span class="sxs-lookup"><span data-stu-id="f0d09-392"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with hello Live SDK</span></span>
<span data-ttu-id="f0d09-393">tooauthenticate usuários, você deve registrar seu aplicativo no hello conta da Microsoft Developer Center.</span><span class="sxs-lookup"><span data-stu-id="f0d09-393">tooauthenticate users, you must register your app at hello Microsoft account Developer Center.</span></span> <span data-ttu-id="f0d09-394">Configure os detalhes do registro no back-end do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="f0d09-394">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="f0d09-395">toocreate Microsoft registro de conta e conecte-o back-end de aplicativo móvel tooyour, Olá concluir as etapas em [registrar seu aplicativo toouse um logon de conta Microsoft].</span><span class="sxs-lookup"><span data-stu-id="f0d09-395">toocreate a Microsoft account registration and connect it tooyour Mobile App backend, complete hello steps in [Register your app toouse a Microsoft account login].</span></span> <span data-ttu-id="f0d09-396">Se você tiver versões da Windows Store e Windows Phone do Silverlight/8 do seu aplicativo, registre a versão de armazenamento do Windows hello primeiro.</span><span class="sxs-lookup"><span data-stu-id="f0d09-396">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register hello Windows Store version first.</span></span>

<span data-ttu-id="f0d09-397">Olá código a seguir autentica usando o Live SDK e usa Olá retornada token toosign no back-end de aplicativo móvel tooyour.</span><span class="sxs-lookup"><span data-stu-id="f0d09-397">hello following code authenticates using Live SDK and uses hello returned token toosign in tooyour Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

<span data-ttu-id="f0d09-398">Para obter mais informações, consulte Olá [Windows Live SDK] documentação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-398">For more information, see hello [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="f0d09-399"><a name="serverflow"></a>Autenticação gerenciada pelo servidor</span><span class="sxs-lookup"><span data-stu-id="f0d09-399"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="f0d09-400">Depois que você registrou o seu provedor de identidade, chamar hello [LoginAsync] método hello [MobileServiceClient] com hello [MobileServiceAuthenticationProvider] valor do provedor.</span><span class="sxs-lookup"><span data-stu-id="f0d09-400">Once you have registered your identity provider, call hello [LoginAsync] method on hello [MobileServiceClient] with hello [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="f0d09-401">Por exemplo, hello código a seguir inicia um servidor fluxo-entrar usando o Facebook.</span><span class="sxs-lookup"><span data-stu-id="f0d09-401">For example, hello following code initiates a server flow sign-in by using Facebook.</span></span>

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

<span data-ttu-id="f0d09-402">Se você estiver usando um provedor de identidade diferente do Facebook, altere o valor de saudação do [MobileServiceAuthenticationProvider] toohello valor para o seu provedor.</span><span class="sxs-lookup"><span data-stu-id="f0d09-402">If you are using an identity provider other than Facebook, change hello value of [MobileServiceAuthenticationProvider] toohello value for your provider.</span></span>

<span data-ttu-id="f0d09-403">Em um fluxo de servidor, do serviço de aplicativo do Azure gerencia o fluxo de autenticação OAuth Olá exibindo Olá página de entrada do provedor selecionado hello.</span><span class="sxs-lookup"><span data-stu-id="f0d09-403">In a server flow, Azure App Service manages hello OAuth authentication flow by displaying hello sign-in page of hello selected provider.</span></span>  <span data-ttu-id="f0d09-404">Uma vez retorna de provedor de identidade hello, serviço de aplicativo do Azure gera um token de autenticação do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0d09-404">Once hello identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="f0d09-405">Olá [LoginAsync] método retorna um [MobileServiceUser], que fornece os dois Olá [UserId] de saudação autenticado o usuário e Olá [ MobileServiceAuthenticationToken], como um JSON web token (JWT).</span><span class="sxs-lookup"><span data-stu-id="f0d09-405">hello [LoginAsync] method returns a [MobileServiceUser], which provides both hello [UserId] of hello authenticated user and hello [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="f0d09-406">Esse token pode ser armazenado em cache e reutilizado até que expire.</span><span class="sxs-lookup"><span data-stu-id="f0d09-406">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="f0d09-407">Para obter mais informações, consulte [token de autenticação do Caching Olá](#caching).</span><span class="sxs-lookup"><span data-stu-id="f0d09-407">For more information, see [Caching hello authentication token](#caching).</span></span>

### <span data-ttu-id="f0d09-408"><a name="caching"></a>Token de autenticação do cache Olá</span><span class="sxs-lookup"><span data-stu-id="f0d09-408"><a name="caching"></a>Caching hello authentication token</span></span>
<span data-ttu-id="f0d09-409">Em alguns casos, o método de logon do hello chamada toohello pode ser evitado após uma autenticação bem-sucedida primeiro Olá armazenando o token de autenticação de saudação do provedor de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-409">In some cases, hello call toohello login method can be avoided after hello first successful authentication by storing hello authentication token from hello provider.</span></span>  <span data-ttu-id="f0d09-410">Os aplicativos da Windows Store e UWP podem usar [PasswordVault] toocache um token de autenticação atual após um bem-sucedida entrar, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f0d09-410">Windows Store and UWP apps can use [PasswordVault] toocache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="f0d09-411">Olá UserId valor é armazenado como Olá nome de usuário da credencial hello e token Olá é hello armazenado como Olá senha.</span><span class="sxs-lookup"><span data-stu-id="f0d09-411">hello UserId value is stored as hello UserName of hello credential and hello token is hello stored as hello Password.</span></span> <span data-ttu-id="f0d09-412">Em iniciante subsequentes, você pode verificar Olá **PasswordVault** para credenciais armazenadas em cache.</span><span class="sxs-lookup"><span data-stu-id="f0d09-412">On subsequent start-ups, you can check hello **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="f0d09-413">Olá exemplo a seguir usa credenciais armazenadas em cache quando eles são encontrados e caso contrário, as tentativas tooauthenticate novamente com hello back-end:</span><span class="sxs-lookup"><span data-stu-id="f0d09-413">hello following example uses cached credentials when they are found, and otherwise attempts tooauthenticate again with hello backend:</span></span>

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

<span data-ttu-id="f0d09-414">Quando você sair de um usuário, você também deve remover credencial Olá armazenado, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f0d09-414">When you sign out a user, you must also remove hello stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="f0d09-415">Saudação de usar aplicativos Xamarin [Xamarin.Auth] credenciais do repositório de APIs toosecurely em uma **conta** objeto.</span><span class="sxs-lookup"><span data-stu-id="f0d09-415">Xamarin    apps use hello [Xamarin.Auth] APIs toosecurely store credentials in an **Account** object.</span></span> <span data-ttu-id="f0d09-416">Para obter um exemplo de como usar essas APIs, consulte Olá [AuthStore.cs] arquivo de código no hello [ContosoMoments foto compartilhamento exemplo](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="f0d09-416">For an example of using these APIs, see hello [AuthStore.cs] code file in hello [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="f0d09-417">Quando você usar a autenticação de cliente gerenciado, você também pode armazenar o token de acesso de saudação obtido do provedor como o Facebook ou Twitter.</span><span class="sxs-lookup"><span data-stu-id="f0d09-417">When you use client-managed authentication, you can also cache hello access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="f0d09-418">Esse token pode ser fornecido toorequest um novo token de autenticação de back-end hello, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f0d09-418">This token can be supplied toorequest a new authentication token from hello backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="f0d09-419"><a name="pushnotifications"></a>Notificações por Push</span><span class="sxs-lookup"><span data-stu-id="f0d09-419"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="f0d09-420">Olá tópicos a seguir cobrem as notificações por Push:</span><span class="sxs-lookup"><span data-stu-id="f0d09-420">hello following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="f0d09-421">Registrar notificações por push</span><span class="sxs-lookup"><span data-stu-id="f0d09-421">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="f0d09-422">Obter um SID do pacote da Windows Store</span><span class="sxs-lookup"><span data-stu-id="f0d09-422">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="f0d09-423">Registrar com modelos de Plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="f0d09-423">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="f0d09-424"><a name="register-for-push"></a>Como se registrar para receber notificações por push</span><span class="sxs-lookup"><span data-stu-id="f0d09-424"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="f0d09-425">cliente de aplicativos móveis Olá permite tooregister para notificações de push com Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0d09-425">hello Mobile Apps client enables you tooregister for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="f0d09-426">Ao registrar, você obter um identificador obtidos específico da plataforma Olá serviço de notificação por Push (PNS).</span><span class="sxs-lookup"><span data-stu-id="f0d09-426">When registering, you obtain a handle that you obtain from hello platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="f0d09-427">Você fornecer esse valor junto com todas as marcas, em seguida, quando você criar o registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-427">You then provide this value along with any tags when you create hello registration.</span></span> <span data-ttu-id="f0d09-428">Olá código a seguir registra seu aplicativo do Windows para notificações por push com hello serviço de notificação do Windows (WNS):</span><span class="sxs-lookup"><span data-stu-id="f0d09-428">hello following code registers your Windows app for push notifications with hello Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="f0d09-429">Se você estiver enviando por push tooWNS, você deve [obter um SID do pacote da Windows Store](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="f0d09-429">If you are pushing tooWNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="f0d09-430">Para obter mais informações sobre aplicativos do Windows, inclusive como tooregister para registros de modelo, consulte [adicionar push notificações tooyour aplicativo].</span><span class="sxs-lookup"><span data-stu-id="f0d09-430">For more information on Windows apps, including how tooregister for template registrations, see [Add push notifications tooyour app].</span></span>

<span data-ttu-id="f0d09-431">Não há suporte para solicitar marcas de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="f0d09-431">Requesting tags from hello client is not supported.</span></span>  <span data-ttu-id="f0d09-432">As solicitações de marca são descartadas silenciosamente do registro.</span><span class="sxs-lookup"><span data-stu-id="f0d09-432">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="f0d09-433">Se você quiser tooregister seu dispositivo com marcas, crie uma API personalizada que usa o registro de Olá Olá API de Hubs de notificação tooperform em seu nome.</span><span class="sxs-lookup"><span data-stu-id="f0d09-433">If you wish tooregister your device with tags, create a Custom API that uses hello Notification Hubs API tooperform hello registration on your behalf.</span></span>  <span data-ttu-id="f0d09-434">[Chamar hello API personalizada](#customapi) em vez da saudação `RegisterNativeAsync()` método.</span><span class="sxs-lookup"><span data-stu-id="f0d09-434">[Call hello Custom API](#customapi) instead of hello `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="f0d09-435"><a name="package-sid"></a>Como obter um SID do pacote da Windows Store</span><span class="sxs-lookup"><span data-stu-id="f0d09-435"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="f0d09-436">Um SID de pacote é necessário para habilitar notificações por push em aplicativos da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="f0d09-436">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="f0d09-437">tooreceive um pacote SID, registrar seu aplicativo com hello da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="f0d09-437">tooreceive a package SID, register your application with hello Windows Store.</span></span>

<span data-ttu-id="f0d09-438">tooobtain este valor:</span><span class="sxs-lookup"><span data-stu-id="f0d09-438">tooobtain this value:</span></span>

1. <span data-ttu-id="f0d09-439">No Visual Studio Solution Explorer, projeto de aplicativo da Windows Store com o botão direito hello, clique em **repositório** > **associar aplicativo hello repositório...** .</span><span class="sxs-lookup"><span data-stu-id="f0d09-439">In Visual Studio Solution Explorer, right-click hello Windows Store app project, click **Store** > **Associate App with hello Store...**.</span></span>
2. <span data-ttu-id="f0d09-440">No Assistente de saudação, clique em **próximo**, entrar com sua conta da Microsoft, digite um nome para seu aplicativo na **reservar um novo nome de aplicativo**, em seguida, clique em **reserva**.</span><span class="sxs-lookup"><span data-stu-id="f0d09-440">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="f0d09-441">Após o registro do aplicativo hello nome do aplicativo foi criado com êxito, selecione hello, clique em **próximo**e, em seguida, clique em **associar**.</span><span class="sxs-lookup"><span data-stu-id="f0d09-441">After hello app registration is successfully created, select hello app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="f0d09-442">Faça logon no toohello [Centro de desenvolvimento do Windows] usando sua Account da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f0d09-442">Log in toohello [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="f0d09-443">Em **meus aplicativos**, clique em um registro de aplicativo hello criado.</span><span class="sxs-lookup"><span data-stu-id="f0d09-443">Under **My apps**, click hello app registration you created.</span></span>
5. <span data-ttu-id="f0d09-444">Clique em **gerenciamento de aplicativo** > **identidade de aplicativo**e, em seguida, role para baixo toofind seu **SID do pacote**.</span><span class="sxs-lookup"><span data-stu-id="f0d09-444">Click **App management** > **App identity**, and then scroll down toofind your **Package SID**.</span></span>

<span data-ttu-id="f0d09-445">Muitos usos do SID do pacote hello tratá-lo como um URI, caso em que você precisa toouse *ms-app: / /* como esquema de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0d09-445">Many uses of hello package SID treat it as a URI, in which case you need toouse *ms-app://* as hello scheme.</span></span> <span data-ttu-id="f0d09-446">Anote a versão de saudação do seu pacote SID formado pela concatenação esse valor como um prefixo.</span><span class="sxs-lookup"><span data-stu-id="f0d09-446">Make note of hello version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="f0d09-447">Aplicativos Xamarin exigem algumas tooregister capaz de toobe código adicional um aplicativo em execução em plataformas Android ou iOS hello.</span><span class="sxs-lookup"><span data-stu-id="f0d09-447">Xamarin apps require some additional code toobe able tooregister an app running on hello iOS or Android platforms.</span></span> <span data-ttu-id="f0d09-448">Para obter mais informações, consulte o tópico de saudação para sua plataforma:</span><span class="sxs-lookup"><span data-stu-id="f0d09-448">For more information, see hello topic for your platform:</span></span>

* [<span data-ttu-id="f0d09-449">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="f0d09-449">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="f0d09-450">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="f0d09-450">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="f0d09-451"><a name="register-xplat"></a>Como: notificações de plataforma cruzada do registro por push modelos toosend</span><span class="sxs-lookup"><span data-stu-id="f0d09-451"><a name="register-xplat"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="f0d09-452">modelos de tooregister, use Olá `RegisterAsync()` método com modelos de hello, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f0d09-452">tooregister templates, use hello `RegisterAsync()` method with hello templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="f0d09-453">Os modelos devem ser `JObject` tipos e pode conter vários modelos em Olá formato JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0d09-453">Your templates should be `JObject` types and can contain multiple templates in hello following JSON format:</span></span>

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

<span data-ttu-id="f0d09-454">Olá método **RegisterAsync()** também aceita blocos secundário:</span><span class="sxs-lookup"><span data-stu-id="f0d09-454">hello method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="f0d09-455">Todas as marcações são retiradas durante o registro para segurança.</span><span class="sxs-lookup"><span data-stu-id="f0d09-455">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="f0d09-456">tooadd marcas tooinstallations ou modelos dentro de instalações, consulte [trabalhar com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure].</span><span class="sxs-lookup"><span data-stu-id="f0d09-456">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="f0d09-457">notificações de toosend utilizando esses modelos registrados, consulte toohello [APIs de Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="f0d09-457">toosend notifications utilizing these registered templates, refer toohello [Notification Hubs APIs].</span></span>

## <span data-ttu-id="f0d09-458"><a name="misc"></a>Tópicos Diversos</span><span class="sxs-lookup"><span data-stu-id="f0d09-458"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="f0d09-459"><a name="errors"></a>Como tratar erros</span><span class="sxs-lookup"><span data-stu-id="f0d09-459"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="f0d09-460">Quando ocorre um erro no back-end do hello, cliente Olá SDK gera um `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="f0d09-460">When an error occurs in hello backend, hello client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="f0d09-461">A exemplo a seguir mostra como uma exceção que é retornado pelo back-end de saudação do toohandle:</span><span class="sxs-lookup"><span data-stu-id="f0d09-461">The following example shows how toohandle an exception that is returned by hello backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

<span data-ttu-id="f0d09-462">Outro exemplo de lidar com condições de erro pode ser encontrado no hello [exemplo de arquivos de aplicativos móveis].</span><span class="sxs-lookup"><span data-stu-id="f0d09-462">Another example of dealing with error conditions can be found in hello [Mobile Apps Files Sample].</span></span> <span data-ttu-id="f0d09-463">O [LoggingHandler] exemplo fornece um delegado de registro em log solicitações de saudação do manipulador toolog sendo feitas toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="f0d09-463">The [LoggingHandler] example provides a logging delegate handler toolog hello requests being made toohello backend.</span></span>

### <span data-ttu-id="f0d09-464"><a name="headers"></a>Como personalizar cabeçalhos de solicitação</span><span class="sxs-lookup"><span data-stu-id="f0d09-464"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="f0d09-465">toosupport seu cenário de aplicativo específico, talvez seja necessário toocustomize comunicação com o back-end de aplicativo móvel hello.</span><span class="sxs-lookup"><span data-stu-id="f0d09-465">toosupport your specific app scenario, you might need toocustomize communication with hello Mobile App backend.</span></span> <span data-ttu-id="f0d09-466">Por exemplo, você pode desejar tooadd uma solicitação de saída de cabeçalho personalizado tooevery ou até mesmo alterar códigos de status de respostas.</span><span class="sxs-lookup"><span data-stu-id="f0d09-466">For example, you may want tooadd a custom header tooevery outgoing request or even change responses status codes.</span></span> <span data-ttu-id="f0d09-467">Você pode usar um personalizado [DelegatingHandler], conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f0d09-467">You can use a custom [DelegatingHandler], as in hello following example:</span></span>

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

[adicionar autenticação tooyour aplicativo]: app-service-mobile-windows-store-dotnet-get-started-users.md
[sincronização de dados Offline em aplicativos móveis do Azure]: app-service-mobile-offline-data-sync.md
[adicionar push notificações tooyour aplicativo]: app-service-mobile-windows-store-dotnet-get-started-push.md
[registrar seu aplicativo toouse um logon de conta Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md
[como tooconfigure aplicativo de serviço de logon do Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[cria uma tabela sem tipo de referência de tooan]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[levar]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[selecione]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[ignorar]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[onde]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[portal do Azure]: https://portal.azure.com/
[portal clássico do Azure]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[Centro de desenvolvimento do Windows]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[APIs de Hubs de notificação]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[exemplo de arquivos de aplicativos móveis]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[OData v3 documentação]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
