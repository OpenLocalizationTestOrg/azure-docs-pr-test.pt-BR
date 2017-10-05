---
title: "Trabalhando com a biblioteca de cliente gerenciado dos Aplicativos Móveis do Serviço de Aplicativo (Windows | Microsoft Docs"
description: "Saiba como usar um cliente do .NET para os Aplicativos Móveis do Serviço de Aplicativo do Azure com aplicativos do Windows e Xamarin."
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
ms.openlocfilehash: 5f4cc3e97ba7adde2aaac471951a3130d79910f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="00058-103">Como usar o cliente gerenciado para Aplicativos Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="00058-103">How to use the managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="00058-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="00058-104">Overview</span></span>
<span data-ttu-id="00058-105">Este guia mostra como executar cenários comuns usando a biblioteca de cliente gerenciado para os Aplicativos Móveis do Serviço de Aplicativo do Azure em aplicativos do Windows e Xamarin.</span><span class="sxs-lookup"><span data-stu-id="00058-105">This guide shows you how to perform common scenarios using the managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="00058-106">Se você for iniciante nos Aplicativos Móveis, primeiro conclua o tutorial [Início rápido dos Aplicativos Móveis do Azure][1] .</span><span class="sxs-lookup"><span data-stu-id="00058-106">If you are new to Mobile Apps, you should consider first completing the [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="00058-107">Neste guia, abordaremos o SDK gerenciado do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="00058-107">In this guide, we focus on the client-side managed SDK.</span></span> <span data-ttu-id="00058-108">Para saber mais sobre os SDKs no lado do servidor para Aplicativos Móveis, veja a documentação do [SDK do .NET Server][2] ou do [SDK do Servidor Node.js][3].</span><span class="sxs-lookup"><span data-stu-id="00058-108">To learn more about the server-side SDKs for Mobile Apps, see the documentation for the [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="00058-109">Documentação de referência</span><span class="sxs-lookup"><span data-stu-id="00058-109">Reference documentation</span></span>
<span data-ttu-id="00058-110">A documentação de referência para o SDK do cliente está localizada aqui: [Referência do cliente .NET dos Aplicativos Móveis do Azure][4].</span><span class="sxs-lookup"><span data-stu-id="00058-110">The reference documentation for the client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="00058-111">Você também pode encontrar vários exemplos de cliente no [Repositório GitHub Azure-Samples][5].</span><span class="sxs-lookup"><span data-stu-id="00058-111">You can also find several client samples in the [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="00058-112">Plataformas com suporte</span><span class="sxs-lookup"><span data-stu-id="00058-112">Supported Platforms</span></span>
<span data-ttu-id="00058-113">A plataforma .NET dá suporte às seguintes plataformas:</span><span class="sxs-lookup"><span data-stu-id="00058-113">The .NET Platform supports the following platforms:</span></span>

* <span data-ttu-id="00058-114">Versões de Xamarin Android para API 19 a 24 (KitKat usando Nougat)</span><span class="sxs-lookup"><span data-stu-id="00058-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="00058-115">Versões de Xamarin iOS para versões 8.0 e posteriores do iOS</span><span class="sxs-lookup"><span data-stu-id="00058-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="00058-116">Plataforma Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="00058-116">Universal Windows Platform</span></span>
* <span data-ttu-id="00058-117">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="00058-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="00058-118">Windows Phone 8.0, exceto para aplicativos Silverlight</span><span class="sxs-lookup"><span data-stu-id="00058-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="00058-119">A autenticação de "fluxo de servidor" usa um modo de exibição da Web para a interface do usuário apresentada.</span><span class="sxs-lookup"><span data-stu-id="00058-119">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="00058-120">Se o dispositivo não for capaz de apresentar uma interface do usuário do modo de exibição da Web, outros métodos de autenticação serão necessários.</span><span class="sxs-lookup"><span data-stu-id="00058-120">If the device is not able to present a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="00058-121">Esse SDK, portanto, não é adequado para relógios ou dispositivos similarmente restritos.</span><span class="sxs-lookup"><span data-stu-id="00058-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="00058-122"><a name="setup"></a>Configuração e Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="00058-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="00058-123">Supomos que você já criou e publicou o projeto de back-end do Aplicativo Móvel, que inclui pelo menos uma tabela.</span><span class="sxs-lookup"><span data-stu-id="00058-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="00058-124">No código usado neste tópico, a tabela é denominada `TodoItem` e tem as seguintes colunas: `Id`, `Text` e `Complete`.</span><span class="sxs-lookup"><span data-stu-id="00058-124">In the code used in this topic, the table is named `TodoItem` and it has the following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="00058-125">Essa tabela é a mesma tabela criada ao concluir o [Início rápido dos Aplicativos Móveis do Azure][1].</span><span class="sxs-lookup"><span data-stu-id="00058-125">This table is the same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="00058-126">O tipo em C# do lado do cliente tipado correspondente é a seguinte classe:</span><span class="sxs-lookup"><span data-stu-id="00058-126">The corresponding typed client-side type in C# is the following class:</span></span>

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

<span data-ttu-id="00058-127">[JsonPropertyAttribute][6] é usada para definir o mapeamento de *PropertyName* entre o campo de cliente e o campo de tabela.</span><span class="sxs-lookup"><span data-stu-id="00058-127">The [JsonPropertyAttribute][6] is used to define the *PropertyName* mapping between the client field and the table field.</span></span>

<span data-ttu-id="00058-128">Para saber como criar tabelas no back-end de Aplicativos Móveis, veja os tópicos [SDK do .NET Server][7] ou [SDK do Servidor Node.js][8].</span><span class="sxs-lookup"><span data-stu-id="00058-128">To learn how to create tables in your Mobile Apps backend, see the [.NET Server SDK topic][7] or the [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="00058-129">Se você tiver criado o back-end do Aplicativo Móvel no portal do Azure usando o Início Rápido, também poderá usar a configuração **Tabelas Fáceis** no [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="00058-129">If you created your Mobile App backend in the Azure portal using the QuickStart, you can also use the **Easy tables** setting in the [Azure portal].</span></span>

### <a name="how-to-install-the-managed-client-sdk-package"></a><span data-ttu-id="00058-130">Como instalar o pacote SDK do cliente gerenciado</span><span class="sxs-lookup"><span data-stu-id="00058-130">How to: Install the managed client SDK package</span></span>
<span data-ttu-id="00058-131">Use um dos métodos a seguir para instalar o pacote SDK do cliente gerenciado para Aplicativos Móveis do [NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="00058-131">Use one of the following methods to install the managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="00058-132">No **Visual Studio**, clique com o botão direito do mouse no projeto, clique em **Gerenciar Pacotes NuGet**, pesquise pelo pacote `Microsoft.Azure.Mobile.Client` e clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="00058-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="00058-133">No **Xamarin Studio**, clique com o botão direito do mouse no projeto, clique em **Adicionar** > **Adicionar Pacotes NuGet**, pesquise pelo pacote `Microsoft.Azure.Mobile.Client ` e clique em **Adicionar Pacote**.</span><span class="sxs-lookup"><span data-stu-id="00058-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="00058-134">No arquivo de atividade principal, lembre-se de adicionar a seguinte instrução **using** :</span><span class="sxs-lookup"><span data-stu-id="00058-134">In your main activity file, remember to add the following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="00058-135"><a name="symbolsource"></a>Como trabalhar com símbolos de depuração no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="00058-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="00058-136">Os símbolos para o namespace Microsoft.Azure.Mobile estão disponíveis em [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="00058-136">The symbols for the Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="00058-137">Veja as [instruções do SymbolSource][11] para integrar o SymbolSource ao Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="00058-137">Refer to the [SymbolSource instructions][11] to integrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="00058-138"><a name="create-client"></a>Criar o cliente dos Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="00058-138"><a name="create-client"></a>Create the Mobile Apps client</span></span>
<span data-ttu-id="00058-139">O código a seguir cria o objeto [MobileServiceClient][12] usado para acessar o back-end do seu Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="00058-139">The following code creates the [MobileServiceClient][12] object that is used to access your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="00058-140">No código anterior, substitua `MOBILE_APP_URL` pela URL do back-end do Aplicativo Móvel, que está localizada na folha de back-end de seu Aplicativo Móvel no [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="00058-140">In the preceding code, replace `MOBILE_APP_URL` with the URL of the Mobile App backend, which is found in the blade for your Mobile App backend in the [Azure portal].</span></span> <span data-ttu-id="00058-141">O objeto MobileServiceClient deve ser um singleton.</span><span class="sxs-lookup"><span data-stu-id="00058-141">The MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="00058-142">Trabalhar com tabelas</span><span class="sxs-lookup"><span data-stu-id="00058-142">Work with Tables</span></span>
<span data-ttu-id="00058-143">A seção a seguir fornece detalhes sobre como pesquisar e recuperar registros e modificar os dados na tabela.</span><span class="sxs-lookup"><span data-stu-id="00058-143">The following section details how to search and retrieve records and modify the data within the table.</span></span>  <span data-ttu-id="00058-144">Os seguintes tópicos são abordados:</span><span class="sxs-lookup"><span data-stu-id="00058-144">The following topics are covered:</span></span>

* [<span data-ttu-id="00058-145">Criar uma referência de tabela</span><span class="sxs-lookup"><span data-stu-id="00058-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="00058-146">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="00058-146">Query data</span></span>](#querying)
* [<span data-ttu-id="00058-147">Filtrar dados retornados</span><span class="sxs-lookup"><span data-stu-id="00058-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="00058-148">Classificar dados retornados</span><span class="sxs-lookup"><span data-stu-id="00058-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="00058-149">Retornar dados em páginas</span><span class="sxs-lookup"><span data-stu-id="00058-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="00058-150">Selecionar colunas específicas</span><span class="sxs-lookup"><span data-stu-id="00058-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="00058-151">Pesquisar um registro por ID</span><span class="sxs-lookup"><span data-stu-id="00058-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="00058-152">Lidando com consultas sem tipo</span><span class="sxs-lookup"><span data-stu-id="00058-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="00058-153">Inserindo dados</span><span class="sxs-lookup"><span data-stu-id="00058-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="00058-154">Atualizando dados</span><span class="sxs-lookup"><span data-stu-id="00058-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="00058-155">Excluindo dados</span><span class="sxs-lookup"><span data-stu-id="00058-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="00058-156">Resolução de Conflitos e Simultaneidade Otimista</span><span class="sxs-lookup"><span data-stu-id="00058-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="00058-157">Associação a uma Interface de Usuário do Windows</span><span class="sxs-lookup"><span data-stu-id="00058-157">Binding to a Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="00058-158">Alterando o Tamanho da Página</span><span class="sxs-lookup"><span data-stu-id="00058-158">Changing the Page Size</span></span>](#pagesize)

### <span data-ttu-id="00058-159"><a name="instantiating"></a>Como criar uma referência de tabela</span><span class="sxs-lookup"><span data-stu-id="00058-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="00058-160">Todos os códigos que acessam e modificam dados em uma tabela de back-end chamam funções no objeto `MobileServiceTable` .</span><span class="sxs-lookup"><span data-stu-id="00058-160">All the code that accesses or modifies data in a backend table calls functions on the `MobileServiceTable` object.</span></span> <span data-ttu-id="00058-161">Obtenha uma referência à tabela chamando o método [GetTable] da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="00058-161">Obtain a reference to the table by calling the [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="00058-162">O objeto retornado usa o modelo de serialização tipado.</span><span class="sxs-lookup"><span data-stu-id="00058-162">The returned object uses the typed serialization model.</span></span> <span data-ttu-id="00058-163">Também há suporte para um modelo de serialização não tipado.</span><span class="sxs-lookup"><span data-stu-id="00058-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="00058-164">O exemplo abaixo [cria uma referência para uma tabela não tipada]:</span><span class="sxs-lookup"><span data-stu-id="00058-164">The following example [creates a reference to an untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="00058-165">Em consultas não tipadas, você deve especificar a cadeia de caracteres de consulta OData subjacente.</span><span class="sxs-lookup"><span data-stu-id="00058-165">In untyped queries, you must specify the underlying OData query string.</span></span>

### <span data-ttu-id="00058-166"><a name="querying"></a>Como consultar dados do seu Aplicativo Móvel</span><span class="sxs-lookup"><span data-stu-id="00058-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="00058-167">Esta seção descreve como emitir consultas para o back-end do Aplicativo Móvel, que inclui as seguintes funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="00058-167">This section describes how to issue queries to the Mobile App backend, which includes the following functionality:</span></span>

* [<span data-ttu-id="00058-168">Filtrar dados retornados</span><span class="sxs-lookup"><span data-stu-id="00058-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="00058-169">Classificar dados retornados</span><span class="sxs-lookup"><span data-stu-id="00058-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="00058-170">Retornar dados em páginas</span><span class="sxs-lookup"><span data-stu-id="00058-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="00058-171">Selecionar colunas específicas</span><span class="sxs-lookup"><span data-stu-id="00058-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="00058-172">Pesquisar dados por ID</span><span class="sxs-lookup"><span data-stu-id="00058-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="00058-173">Um tamanho de página controlado por servidor é usado para impedir que todas as linhas sejam retornadas.</span><span class="sxs-lookup"><span data-stu-id="00058-173">A server-driven page size is enforced to prevent all rows from being returned.</span></span>  <span data-ttu-id="00058-174">A paginação impede que as solicitações padrão de grandes conjuntos de dados prejudiquem o serviço.</span><span class="sxs-lookup"><span data-stu-id="00058-174">Paging keeps default requests for large data sets from negatively impacting the service.</span></span>  <span data-ttu-id="00058-175">Para retornar mais de 50 linhas, use os métodos `Skip` e `Take`, conforme descrito em [Retornar dados em páginas](#paging).</span><span class="sxs-lookup"><span data-stu-id="00058-175">To return more than 50 rows, use the `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="00058-176"><a name="filtering"></a>Como filtrar dados retornados</span><span class="sxs-lookup"><span data-stu-id="00058-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="00058-177">O código a seguir ilustra como filtrar dados incluindo uma cláusula `Where` em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="00058-177">The following code illustrates how to filter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="00058-178">Ele retorna todos os itens de `todoTable`, cuja propriedade `Complete` é igual a `false`.</span><span class="sxs-lookup"><span data-stu-id="00058-178">It returns all items from `todoTable` whose `Complete` property is equal to `false`.</span></span> <span data-ttu-id="00058-179">A função [Where] aplica um predicado de filtragem de linha à consulta na tabela.</span><span class="sxs-lookup"><span data-stu-id="00058-179">The [Where] function applies a row filtering predicate to the query against the table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="00058-180">Você pode exibir o URI da solicitação enviado ao back-end usando um software de inspeção de mensagem, como as ferramentas de desenvolvedor do navegador ou o [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="00058-180">You can view the URI of the request sent to the backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="00058-181">Se você examinar o URI, verá que a própria cadeia de caracteres da consulta está sendo modificada:</span><span class="sxs-lookup"><span data-stu-id="00058-181">If you look at the request URI, notice that the query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="00058-182">Essa solicitação de OData é convertida em uma consulta SQL pelo SDK do Servidor:</span><span class="sxs-lookup"><span data-stu-id="00058-182">This OData request is translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="00058-183">A função passada para o método `Where` pode ter um número arbitrário de condições.</span><span class="sxs-lookup"><span data-stu-id="00058-183">The function that is passed to the `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="00058-184">Esse exemplo deve ser convertido em uma consulta SQL pelo SDK do Servidor:</span><span class="sxs-lookup"><span data-stu-id="00058-184">This example would be translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="00058-185">Essa consulta pode ser dividida em várias cláusulas:</span><span class="sxs-lookup"><span data-stu-id="00058-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="00058-186">Os dois métodos são equivalentes e podem ser usados de maneira intercambiável.</span><span class="sxs-lookup"><span data-stu-id="00058-186">The two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="00058-187">A opção anterior&mdash;de concatenar vários predicados em uma consulta&mdash;é mais compacta e recomendada.</span><span class="sxs-lookup"><span data-stu-id="00058-187">The former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="00058-188">A cláusula `Where` dá suporte a operações que são convertidas para o subconjunto OData.</span><span class="sxs-lookup"><span data-stu-id="00058-188">The `Where` clause supports operations that be translated into the OData subset.</span></span> <span data-ttu-id="00058-189">As operações incluem:</span><span class="sxs-lookup"><span data-stu-id="00058-189">Operations include:</span></span>

* <span data-ttu-id="00058-190">Operadores relacionais (==,!=, <, <=, >, >=),</span><span class="sxs-lookup"><span data-stu-id="00058-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="00058-191">Operadores aritméticos (+, -, /, *, %),</span><span class="sxs-lookup"><span data-stu-id="00058-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="00058-192">Número de precisão (Math.Floor, Math.Ceiling),</span><span class="sxs-lookup"><span data-stu-id="00058-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="00058-193">Funções de cadeia de caracteres (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span><span class="sxs-lookup"><span data-stu-id="00058-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="00058-194">Propriedades de data (ano, mês, dia, hora, minuto, segundo),</span><span class="sxs-lookup"><span data-stu-id="00058-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="00058-195">Propriedades de acesso de um objeto e</span><span class="sxs-lookup"><span data-stu-id="00058-195">Access properties of an object, and</span></span>
* <span data-ttu-id="00058-196">Expressões que combinam qualquer uma dessas operações.</span><span class="sxs-lookup"><span data-stu-id="00058-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="00058-197">Ao considerar o que é compatível com o SDK do Servidor, você pode consultar a [Documentação do OData v3].</span><span class="sxs-lookup"><span data-stu-id="00058-197">When considering what the Server SDK supports, you can consider the [OData v3 Documentation].</span></span>

### <span data-ttu-id="00058-198"><a name="sorting"></a>Como classificar dados retornados</span><span class="sxs-lookup"><span data-stu-id="00058-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="00058-199">O código a seguir ilustra como classificar dados incluindo uma função [OrderBy] ou [OrderByDescending] na consulta.</span><span class="sxs-lookup"><span data-stu-id="00058-199">The following code illustrates how to sort data by including an [OrderBy] or [OrderByDescending] function in the query.</span></span> <span data-ttu-id="00058-200">Ele retorna os itens da `todoTable` classificada em ordem crescente pelo campo `Text`.</span><span class="sxs-lookup"><span data-stu-id="00058-200">It returns items from `todoTable` sorted ascending by the `Text` field.</span></span>

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

### <span data-ttu-id="00058-201"><a name="paging"></a>Como retornar dados em páginas</span><span class="sxs-lookup"><span data-stu-id="00058-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="00058-202">Por padrão, o back-end retorna apenas as primeiras 50 linhas.</span><span class="sxs-lookup"><span data-stu-id="00058-202">By default, the backend returns only the first 50 rows.</span></span> <span data-ttu-id="00058-203">Você pode aumentar o número de linhas retornadas chamando o método [Take] .</span><span class="sxs-lookup"><span data-stu-id="00058-203">You can increase the number of returned rows by calling the [Take] method.</span></span> <span data-ttu-id="00058-204">Use `Take` juntamente com o método [Ignorar] para solicitar uma "página" específica do conjunto de dados total retornado pela consulta.</span><span class="sxs-lookup"><span data-stu-id="00058-204">Use `Take` along with the [Skip] method to request a specific "page" of the total dataset returned by the query.</span></span> <span data-ttu-id="00058-205">A consulta a seguir, quando executada, retorna os três itens principais na tabela.</span><span class="sxs-lookup"><span data-stu-id="00058-205">The following query, when executed, returns the top three items in the table.</span></span>

```
// Define a filtered query that returns the top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="00058-206">A consulta revisada a seguir ignora os três primeiros resultados e retorna os três seguintes.</span><span class="sxs-lookup"><span data-stu-id="00058-206">The following revised query skips the first three results and returns the next three results.</span></span> <span data-ttu-id="00058-207">Essa consulta produz a segunda "página" de dados, onde o tamanho da página é de três itens.</span><span class="sxs-lookup"><span data-stu-id="00058-207">This query produces the second "page" of data, where the page size is three items.</span></span>

```
// Define a filtered query that skips the top 3 items and returns the next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="00058-208">O método [IncludeTotalCount] solicita a contagem total de *todos* os registros que seriam retornados, ignorando cláusulas de paginação/limite especificadas:</span><span class="sxs-lookup"><span data-stu-id="00058-208">The [IncludeTotalCount] method requests the total count for *all* the records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="00058-209">Em um aplicativo de verdade, você pode usar consultas semelhantes ao exemplo anterior com um controle de paginação ou interface do usuário semelhante para navegar entre páginas.</span><span class="sxs-lookup"><span data-stu-id="00058-209">In a real world app, you can use queries similar to the preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="00058-210">Para substituir o limite de 50 linhas em um back-end do Aplicativo Móvel, você também deve aplicar o [EnableQueryAttribute] ao método GET público e especificar o comportamento de paginação.</span><span class="sxs-lookup"><span data-stu-id="00058-210">To override the 50-row limit in a Mobile App backend, you must also apply the [EnableQueryAttribute] to the public GET method and specify the paging behavior.</span></span> <span data-ttu-id="00058-211">Quando aplicado ao método, o seguinte define o máximo de linhas retornadas para 1000:</span><span class="sxs-lookup"><span data-stu-id="00058-211">When applied to the method, the following sets the maximum returned rows to 1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="00058-212"><a name="selecting"></a>Como selecionar colunas específicas</span><span class="sxs-lookup"><span data-stu-id="00058-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="00058-213">Você pode especificar qual conjunto de propriedades incluir nos resultados adicionando uma cláusula [Select] à sua consulta.</span><span class="sxs-lookup"><span data-stu-id="00058-213">You can specify which set of properties to include in the results by adding a [Select] clause to your query.</span></span> <span data-ttu-id="00058-214">Por exemplo, o código a seguir mostra como selecionar apenas um campo e também como selecionar e formatar vários campos:</span><span class="sxs-lookup"><span data-stu-id="00058-214">For example, the following code shows how to select just one field and also how to select and format multiple fields:</span></span>

```
// Select one field -- just the Text
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

<span data-ttu-id="00058-215">Todas as funções descritas até agora são aditivas e, portanto, podemos continuar a encadeá-las.</span><span class="sxs-lookup"><span data-stu-id="00058-215">All the functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="00058-216">Cada chamada encadeada afeta mais a consulta.</span><span class="sxs-lookup"><span data-stu-id="00058-216">Each chained call affects more of the query.</span></span> <span data-ttu-id="00058-217">Mais um exemplo:</span><span class="sxs-lookup"><span data-stu-id="00058-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="00058-218"><a name="lookingup"></a>Como pesquisar dados pela ID</span><span class="sxs-lookup"><span data-stu-id="00058-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="00058-219">A função [LookupAsync] pode ser usada para procurar objetos do banco de dados com uma ID específica.</span><span class="sxs-lookup"><span data-stu-id="00058-219">The [LookupAsync] function can be used to look up objects from the database with a particular ID.</span></span>

```
// This query filters out the item with the ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="00058-220"><a name="untypedqueries"></a>Como executar consultas sem tipo</span><span class="sxs-lookup"><span data-stu-id="00058-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="00058-221">Ao executar uma consulta usando um objeto de tabela sem tipo, você deve especificar expressamente a cadeia de consulta OData chamando [ReadAsync], como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="00058-221">When executing a query using an untyped table object, you must explicitly specify the OData query string by calling [ReadAsync], as in the following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="00058-222">Você recupera valores JSON que podem ser usados como um recipiente de propriedades.</span><span class="sxs-lookup"><span data-stu-id="00058-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="00058-223">Para obter mais informações sobre JToken e Newtonsoft Json.NET, confira o site [Json.NET] .</span><span class="sxs-lookup"><span data-stu-id="00058-223">For more information on JToken and Newtonsoft Json.NET, see the [Json.NET] site.</span></span>

### <span data-ttu-id="00058-224"><a name="inserting"></a>Como inserir dados em um back-end do Aplicativo Móvel</span><span class="sxs-lookup"><span data-stu-id="00058-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="00058-225">Todos os tipos de cliente devem conter um membro chamado **Id**, que é por padrão uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="00058-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="00058-226">Essa **Id** é necessária para executar operações CRUD para sincronização offline.</span><span class="sxs-lookup"><span data-stu-id="00058-226">This **Id** is required to perform CRUD operations and for offline sync.</span></span> <span data-ttu-id="00058-227">O código a seguir ilustra como usar o método [InsertAsync] para inserir novas linhas em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="00058-227">The following code illustrates how to use the [InsertAsync] method to insert new rows into a table.</span></span> <span data-ttu-id="00058-228">O parâmetro contém os dados a serem inseridos como um objeto .NET.</span><span class="sxs-lookup"><span data-stu-id="00058-228">The parameter contains the data to be inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="00058-229">Se um valor exclusivo de ID personalizada não é incluído no `todoItem` durante uma inserção, um GUID é gerado pelo servidor.</span><span class="sxs-lookup"><span data-stu-id="00058-229">If a unique custom ID value is not included in the `todoItem` during an insert, a GUID is generated by the server.</span></span>
<span data-ttu-id="00058-230">Você poderá recuperar a Id gerada ao inspecionar o objeto após o retorno da chamada.</span><span class="sxs-lookup"><span data-stu-id="00058-230">You can retrieve the generated Id by inspecting the object after the call returns.</span></span>

<span data-ttu-id="00058-231">Para inserir dados não tipados, você pode tirar proveito do Json.NET:</span><span class="sxs-lookup"><span data-stu-id="00058-231">To insert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="00058-232">Aqui está um exemplo usando um endereço de email como uma id de cadeia de caracteres exclusiva:</span><span class="sxs-lookup"><span data-stu-id="00058-232">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="00058-233">Trabalhando com valores de ID</span><span class="sxs-lookup"><span data-stu-id="00058-233">Working with ID values</span></span>
<span data-ttu-id="00058-234">Os Aplicativos Móveis dão suporte a valores exclusivos e personalizados de cadeia de caracteres para a coluna **id** da tabela.</span><span class="sxs-lookup"><span data-stu-id="00058-234">Mobile Apps supports unique custom string values for the table's **id** column.</span></span> <span data-ttu-id="00058-235">Um valor de cadeia de caracteres permite que aplicativos usem valores personalizados, como endereços de email ou nomes de usuário para a ID.</span><span class="sxs-lookup"><span data-stu-id="00058-235">A string value allows applications to use custom values such as email addresses or user names for the ID.</span></span>  <span data-ttu-id="00058-236">IDs de cadeia de caracteres fornecem os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="00058-236">String IDs provide you with the following benefits:</span></span>

* <span data-ttu-id="00058-237">As IDs são geradas sem fazer uma varredura no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="00058-237">IDs are generated without making a round trip to the database.</span></span>
* <span data-ttu-id="00058-238">Os registros são mais fáceis de mesclar a partir de tabelas ou bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="00058-238">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="00058-239">Os valores de IDs podem integrar-se melhor a uma lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="00058-239">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="00058-240">Quando um valor de ID de cadeia de caracteres não está definido em um registro inserido, o back-end do Aplicativo Móvel gera um valor exclusivo para a ID.</span><span class="sxs-lookup"><span data-stu-id="00058-240">When a string ID value is not set on an inserted record, the Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="00058-241">Você pode usar o método [Guid.NewGuid] para gerar seus próprios valores de ID, seja no cliente ou no back-end.</span><span class="sxs-lookup"><span data-stu-id="00058-241">You can use the [Guid.NewGuid] method to generate your own ID values, either on the client or in the backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="00058-242"><a name="modifying"></a>Como modificar dados em um back-end de Aplicativo Móvel</span><span class="sxs-lookup"><span data-stu-id="00058-242"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="00058-243">O código a seguir ilustra como usar o método [UpdateAsync] para atualizar um registro existente com a mesma ID com novas informações.</span><span class="sxs-lookup"><span data-stu-id="00058-243">The following code illustrates how to use the [UpdateAsync] method to update an existing record with the same ID with new information.</span></span> <span data-ttu-id="00058-244">O parâmetro contém os dados a serem atualizados como um objeto .NET.</span><span class="sxs-lookup"><span data-stu-id="00058-244">The parameter contains the data to be updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="00058-245">Para atualizar dados não tipados, você pode tirar proveito do [Json.NET] da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="00058-245">To update untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="00058-246">Um campo `id` deve ser especificado ao fazer uma atualização.</span><span class="sxs-lookup"><span data-stu-id="00058-246">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="00058-247">O back-end usa o campo `id` para identificar a linha a ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="00058-247">The backend uses the `id` field to identify which row to update.</span></span> <span data-ttu-id="00058-248">O campo `id` pode ser obtido do resultado da chamada `InsertAsync`.</span><span class="sxs-lookup"><span data-stu-id="00058-248">The `id` field can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="00058-249">Quando você tenta atualizar um item sem fornecer o valor `id`, uma `ArgumentException` é gerada.</span><span class="sxs-lookup"><span data-stu-id="00058-249">An `ArgumentException` is raised if you try to update an item without providing the `id` value.</span></span>

### <span data-ttu-id="00058-250"><a name="deleting"></a>Como excluir dados em um back-end do Aplicativo Móvel</span><span class="sxs-lookup"><span data-stu-id="00058-250"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="00058-251">O código a seguir ilustra como usar o método [DeleteAsync] para excluir uma instância existente.</span><span class="sxs-lookup"><span data-stu-id="00058-251">The following code illustrates how to use the [DeleteAsync] method to delete an existing instance.</span></span> <span data-ttu-id="00058-252">A instância é identificada pelo campo `id` definido em `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="00058-252">The instance is identified by the `id` field set on the `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="00058-253">Para excluir dados não tipados, você pode tirar proveito do Json.NET da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="00058-253">To delete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="00058-254">Quando você faz uma solicitação de exclusão, uma ID deve ser especificada.</span><span class="sxs-lookup"><span data-stu-id="00058-254">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="00058-255">Outras propriedades não são passadas para o serviço ou são ignoradas no serviço.</span><span class="sxs-lookup"><span data-stu-id="00058-255">Other properties are not passed to the service or are ignored at the service.</span></span> <span data-ttu-id="00058-256">O resultado de uma chamada de `DeleteAsync` geralmente é `null`.</span><span class="sxs-lookup"><span data-stu-id="00058-256">The result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="00058-257">A ID a ser passada pode ser obtida do resultado da chamada de `InsertAsync` .</span><span class="sxs-lookup"><span data-stu-id="00058-257">The ID to pass in can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="00058-258">Um `MobileServiceInvalidOperationException` é gerado quando você tenta excluir um item sem especificar o campo `id`.</span><span class="sxs-lookup"><span data-stu-id="00058-258">A `MobileServiceInvalidOperationException` is thrown when you try to delete an item without specifying the `id` field.</span></span>

### <span data-ttu-id="00058-259"><a name="optimisticconcurrency"></a>Como usar a simultaneidade otimista para resolução de conflitos</span><span class="sxs-lookup"><span data-stu-id="00058-259"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="00058-260">Dois ou mais clientes podem gravar alterações no mesmo item ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="00058-260">Two or more clients may write changes to the same item at the same time.</span></span> <span data-ttu-id="00058-261">Sem detecção de conflito, a última gravação substituiria as atualizações anteriores.</span><span class="sxs-lookup"><span data-stu-id="00058-261">Without conflict detection, the last write would overwrite any previous updates.</span></span> <span data-ttu-id="00058-262">**Controle de simultaneidade otimista** pressupõe que cada transação possa ser confirmada e, portanto, não usa nenhum recurso de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="00058-262">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="00058-263">Antes de confirmar uma transação, o controle de simultaneidade otimista verifica se nenhuma outra transação modificou os dados.</span><span class="sxs-lookup"><span data-stu-id="00058-263">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified the data.</span></span> <span data-ttu-id="00058-264">Se os dados foram modificados, a transação de confirmação será revertida.</span><span class="sxs-lookup"><span data-stu-id="00058-264">If the data has been modified, the committing transaction is rolled back.</span></span>

<span data-ttu-id="00058-265">Os Aplicativos Móveis dão suporte ao controle de simultaneidade otimista acompanhando as alterações em cada item na coluna de propriedades do sistema `version` definida para cada tabela no back-end do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="00058-265">Mobile Apps supports optimistic concurrency control by tracking changes to each item using the `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="00058-266">Cada vez que um registro é atualizado, os Aplicativos Móveis definem a propriedade `version` desse registro como um novo valor.</span><span class="sxs-lookup"><span data-stu-id="00058-266">Each time a record is updated, Mobile Apps sets the `version` property for that record to a new value.</span></span> <span data-ttu-id="00058-267">Durante cada solicitação de atualização, a propriedade `version` do registro incluído na solicitação é comparada à mesma propriedade do registro no servidor.</span><span class="sxs-lookup"><span data-stu-id="00058-267">During each update request, the `version` property of the record included with the request is compared to the same property for the record on the server.</span></span> <span data-ttu-id="00058-268">Se a versão transmitida com a solicitação não corresponder ao back-end, a biblioteca de cliente gerará uma exceção `MobileServicePreconditionFailedException<T>` .</span><span class="sxs-lookup"><span data-stu-id="00058-268">If the version passed with the request does not match the backend, then the client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="00058-269">O tipo incluído com a exceção é o registro do back-end que contém a versão do registro dos servidores.</span><span class="sxs-lookup"><span data-stu-id="00058-269">The type included with the exception is the record from the backend containing the servers version of the record.</span></span> <span data-ttu-id="00058-270">O aplicativo poderá, então, usar essas informações para decidir se deve executar a solicitação de atualização novamente com o valor de `version` correto do back-end para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="00058-270">The application can then use this information to decide whether to execute the update request again with the correct `version` value from the backend to commit changes.</span></span>

<span data-ttu-id="00058-271">Define uma coluna na classe da tabela para a propriedade do sistema `version` para habilitar a simultaneidade otimista.</span><span class="sxs-lookup"><span data-stu-id="00058-271">Define a column on the table class for the `version` system property to enable optimistic concurrency.</span></span> <span data-ttu-id="00058-272">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="00058-272">For example:</span></span>

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

<span data-ttu-id="00058-273">Aplicativos que usam tabelas não tipadas habilitam a simultaneidade otimista definindo o sinalizador `Version` nas `SystemProperties` da tabela da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="00058-273">Applications using untyped tables enable optimistic concurrency by setting the `Version` flag on the `SystemProperties` of the table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="00058-274">Além de habilitar a simultaneidade otimista, você também deve capturar a exceção `MobileServicePreconditionFailedException<T>` em seu código ao chamar [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="00058-274">In addition to enabling optimistic concurrency, you must also catch the `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="00058-275">Resolva o conflito aplicando a `version` correta ao registro atualizado e chame [UpdateAsync] com o registro resolvido.</span><span class="sxs-lookup"><span data-stu-id="00058-275">Resolve the conflict by applying the correct `version` to the updated record and call [UpdateAsync] with the resolved record.</span></span> <span data-ttu-id="00058-276">O código a seguir mostra como resolver um conflito de gravação quando detectado:</span><span class="sxs-lookup"><span data-stu-id="00058-276">The following code shows how to resolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at the remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, the item has changed since the last query
        // Resolve the conflict between the local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user to choose the resoltion between versions
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
        // To resolve the conflict, update the version of the item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while the user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="00058-277">Para obter mais informações, confira o tópico [Sincronização de Dados Offline nos Aplicativos Móveis do Azure] .</span><span class="sxs-lookup"><span data-stu-id="00058-277">For more information, see the [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="00058-278"><a name="binding"></a>Como: associar dados dos Aplicativos Móveis a uma interface do usuário do Windows</span><span class="sxs-lookup"><span data-stu-id="00058-278"><a name="binding"></a>How to: Bind Mobile Apps data to a Windows user interface</span></span>
<span data-ttu-id="00058-279">Esta seção mostra como exibir os objetos de dados retornados usando elementos da interface do usuário em um aplicativo do Windows.</span><span class="sxs-lookup"><span data-stu-id="00058-279">This section shows how to display returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="00058-280">O exemplo de código a seguir associa a origem da lista a uma consulta de itens incompletos.</span><span class="sxs-lookup"><span data-stu-id="00058-280">The following example code binds to the source of the list with a query for incomplete items.</span></span> <span data-ttu-id="00058-281">O [MobileServiceCollection] cria uma coleção de associações com reconhecimento de Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="00058-281">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound to a UI list control
IEnumerable itemsControl  = items;

// Bind this to a ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="00058-282">Alguns controles no tempo de execução gerenciado dão suporte a uma interface chamada [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="00058-282">Some controls in the managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="00058-283">Essa interface permite que os controles solicitem dados adicionais quando o usuário rola.</span><span class="sxs-lookup"><span data-stu-id="00058-283">This interface allows controls to request extra data when the user scrolls.</span></span> <span data-ttu-id="00058-284">Há suporte interno para essa interface para aplicativos universais do Windows via [MobileServiceIncrementalLoadingCollection], que processa as chamadas automaticamente por meio dos controles.</span><span class="sxs-lookup"><span data-stu-id="00058-284">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from the controls.</span></span> <span data-ttu-id="00058-285">Use `MobileServiceIncrementalLoadingCollection` em aplicativos do Windows, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="00058-285">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="00058-286">Para usar a nova coleção nos aplicativos do Windows Phone 8 e do “Silverlight”, use os métodos da extensão `ToCollection` em `IMobileServiceTableQuery<T>` e `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="00058-286">To use the new collection on Windows Phone 8 and "Silverlight" apps, use the `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="00058-287">Para carregar dados, chame `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="00058-287">To load data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="00058-288">Quando usa a coleção criada chamando `ToCollectionAsync` ou `ToCollection`, você obtém uma coleção que pode ser vinculada a controles da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="00058-288">When you use the collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound to UI controls.</span></span>  <span data-ttu-id="00058-289">Essa coleção tem reconhecimento de paginação.</span><span class="sxs-lookup"><span data-stu-id="00058-289">This collection is paging-aware.</span></span>  <span data-ttu-id="00058-290">Como a coleção está carregando dados da rede, o carregamento às vezes falha.</span><span class="sxs-lookup"><span data-stu-id="00058-290">Since the collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="00058-291">Para lidar com essas falhas, substitua o método `OnException` na `MobileServiceIncrementalLoadingCollection` para tratar das exceções resultantes de chamadas para `LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="00058-291">To handle such failures, override the `OnException` method on `MobileServiceIncrementalLoadingCollection` to handle exceptions resulting from calls to `LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="00058-292">Pense que sua tabela tem muitos campos, mas você só deseja exibir alguns deles em seu controle.</span><span class="sxs-lookup"><span data-stu-id="00058-292">Consider if your table has many fields but you only want to display some of them in your control.</span></span> <span data-ttu-id="00058-293">Você pode usar as diretrizes contidas na seção anterior "[Selecionar colunas específicas](#selecting)" para selecionar colunas específicas a serem exibidas na interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="00058-293">You may use the guidance in the preceding section "[Select specific columns](#selecting)" to select specific columns to display in the UI.</span></span>

### <span data-ttu-id="00058-294"><a name="pagesize"></a>Alterar o Tamanho da página</span><span class="sxs-lookup"><span data-stu-id="00058-294"><a name="pagesize"></a>Change the Page size</span></span>
<span data-ttu-id="00058-295">Os Aplicativos Móveis do Azure retornam, no máximo, 50 itens por solicitação por padrão.</span><span class="sxs-lookup"><span data-stu-id="00058-295">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="00058-296">Você pode alterar o tamanho de paginação aumentando o tamanho máximo da página no cliente e no servidor.</span><span class="sxs-lookup"><span data-stu-id="00058-296">You can change the paging size by increasing the maximum page size on both the client and server.</span></span>  <span data-ttu-id="00058-297">Para aumentar o tamanho da página solicitada, especifique `PullOptions` ao usar `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="00058-297">To increase the requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="00058-298">Supondo que você deixou o `PageSize` igual ou maior a 100 no servidor, uma solicitação retorna até 100 itens.</span><span class="sxs-lookup"><span data-stu-id="00058-298">Assuming you have made the `PageSize` equal to or greater than 100 within the server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="00058-299"><a name="#offlinesync"></a>Trabalhar com tabelas offline</span><span class="sxs-lookup"><span data-stu-id="00058-299"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="00058-300">Tabelas offline usam um armazenamento local do SQLite para armazenamento de dados para uso no modo offline.</span><span class="sxs-lookup"><span data-stu-id="00058-300">Offline tables use a local SQLite store to store data for use when offline.</span></span>  <span data-ttu-id="00058-301">Todas as operações da tabela são executadas no armazenamento local do SQLite em vez de no armazenamento do servidor remoto.</span><span class="sxs-lookup"><span data-stu-id="00058-301">All table operations are done against the local SQLite store instead of the remote server store.</span></span>  <span data-ttu-id="00058-302">Para criar uma tabela offline, primeiro, prepare seu projeto:</span><span class="sxs-lookup"><span data-stu-id="00058-302">To create an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="00058-303">No Visual Studio, clique com o botão direito do mouse na solução > **Gerenciar Pacotes NuGet para a Solução...**, procure e instale o pacote NuGet **Microsoft.Azure.Mobile.Client.SQLiteStore** para todos os projetos na solução.</span><span class="sxs-lookup"><span data-stu-id="00058-303">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="00058-304">(Opcional) Para dar suporte a dispositivos Windows, instale um dos seguintes pacotes de tempo de execução do SQLite:</span><span class="sxs-lookup"><span data-stu-id="00058-304">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="00058-305">**Tempo de Execução do Windows 8.1**: instale o [SQLite para Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="00058-305">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="00058-306">**Windows Phone 8.1**: instale o [SQLite para Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="00058-306">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="00058-307">**Plataforma Universal do Windows**: instale o [SQLite para a Plataforma Universal do Windows][5].</span><span class="sxs-lookup"><span data-stu-id="00058-307">**Universal Windows Platform** Install [SQLite for the Universal Windows][5].</span></span>
3. <span data-ttu-id="00058-308">(Opcional).</span><span class="sxs-lookup"><span data-stu-id="00058-308">(Optional).</span></span> <span data-ttu-id="00058-309">Para dispositivos Windows, clique com botão direito do mouse em **Referências** > **Adicionar Referência…**, expanda a pasta **Windows** > **Extensões**, habilite o SDK do **SQLite para Windows** apropriado junto com o SDK do **Tempo de Execução do Visual C++ 2013 para Windows**.</span><span class="sxs-lookup"><span data-stu-id="00058-309">For Windows devices, click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**, then enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="00058-310">Os nomes do SDK do SQLite variam ligeiramente de acordo com cada plataforma Windows.</span><span class="sxs-lookup"><span data-stu-id="00058-310">The SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="00058-311">Antes que uma referência de tabela possa ser criada, o armazenamento local precisa ser preparado:</span><span class="sxs-lookup"><span data-stu-id="00058-311">Before a table reference can be created, the local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes the SyncContext using the default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="00058-312">A inicialização do armazenamento normalmente é feita imediatamente depois que o cliente é criado.</span><span class="sxs-lookup"><span data-stu-id="00058-312">Store initialization is normally done immediately after the client is created.</span></span>  <span data-ttu-id="00058-313">O **OfflineDbPath** deve ser um nome de arquivo adequado para uso em todas as plataformas que tem suporte.</span><span class="sxs-lookup"><span data-stu-id="00058-313">The **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="00058-314">Se o caminho for um caminho totalmente qualificado (ou seja, começa com uma barra invertida), então, ele será usado.</span><span class="sxs-lookup"><span data-stu-id="00058-314">If the path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="00058-315">Se o caminho não for totalmente qualificado, o arquivo será colocado em um local específico da plataforma.</span><span class="sxs-lookup"><span data-stu-id="00058-315">If the path is not fully qualified, the file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="00058-316">Para dispositivos Android e iOS, o caminho padrão é a pasta "Arquivos pessoais".</span><span class="sxs-lookup"><span data-stu-id="00058-316">For iOS and Android devices, the default path is the "Personal Files" folder.</span></span>
* <span data-ttu-id="00058-317">Para dispositivos Windows, o caminho padrão é a pasta "AppData" específica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="00058-317">For Windows devices, the default path is the application-specific "AppData" folder.</span></span>

<span data-ttu-id="00058-318">Uma referência de tabela pode ser obtida usando o método `GetSyncTable<>`:</span><span class="sxs-lookup"><span data-stu-id="00058-318">A table reference can be obtained using the `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="00058-319">Você não precisa se autenticar para usar uma tabela offline.</span><span class="sxs-lookup"><span data-stu-id="00058-319">You do not need to authenticate to use an offline table.</span></span>  <span data-ttu-id="00058-320">Você precisa se autenticar apenas quando estiver se comunicando com o serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="00058-320">You only need to authenticate when you are communicating with the backend service.</span></span>

### <span data-ttu-id="00058-321"><a name="syncoffline"></a>Sincronizando uma tabela Offline</span><span class="sxs-lookup"><span data-stu-id="00058-321"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="00058-322">Tabelas off-line não são sincronizadas com o back-end, por padrão.</span><span class="sxs-lookup"><span data-stu-id="00058-322">Offline tables are not synchronized with the backend by default.</span></span>  <span data-ttu-id="00058-323">A sincronização é dividida em duas partes.</span><span class="sxs-lookup"><span data-stu-id="00058-323">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="00058-324">Você pode enviar alterações separadamente de download de novos itens.</span><span class="sxs-lookup"><span data-stu-id="00058-324">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="00058-325">Este é um método de sincronização típico:</span><span class="sxs-lookup"><span data-stu-id="00058-325">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //The first parameter is a query name that is used internally by the client SDK to implement incremental sync.
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

    // Simple error/conflict handling. A real application would handle the various errors like network conditions,
    // server conflicts and others via the IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting to server's copy.
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

<span data-ttu-id="00058-326">Se o primeiro argumento para `PullAsync` for nulo, a sincronização incremental não será usado.</span><span class="sxs-lookup"><span data-stu-id="00058-326">If the first argument to `PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="00058-327">Todas as operações de sincronização recuperam todos os registros.</span><span class="sxs-lookup"><span data-stu-id="00058-327">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="00058-328">O SDK executa um `PushAsync()` implícito antes de extrair os registros.</span><span class="sxs-lookup"><span data-stu-id="00058-328">The SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="00058-329">Manipulação de conflito ocorre em um método `PullAsync()`.</span><span class="sxs-lookup"><span data-stu-id="00058-329">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="00058-330">Você pode lidar com conflitos da mesma maneira que com tabelas on-line.</span><span class="sxs-lookup"><span data-stu-id="00058-330">You can deal with conflicts in the same way as online tables.</span></span>  <span data-ttu-id="00058-331">O conflito é produzido quando `PullAsync()` é chamado em vez de durante a inserção, atualização ou exclusão.</span><span class="sxs-lookup"><span data-stu-id="00058-331">The conflict is produced when `PullAsync()` is called instead of during the insert, update, or delete.</span></span> <span data-ttu-id="00058-332">Se vários conflitos ocorrerem, eles serão agrupados em uma única MobileServicePushFailedException.</span><span class="sxs-lookup"><span data-stu-id="00058-332">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="00058-333">Gerenciar cada falha separadamente.</span><span class="sxs-lookup"><span data-stu-id="00058-333">Handle each failure separately.</span></span>

## <span data-ttu-id="00058-334"><a name="#customapi"></a>Trabalhar com uma API personalizada</span><span class="sxs-lookup"><span data-stu-id="00058-334"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="00058-335">Uma API personalizada permite que você defina pontos de extremidade personalizados que expõem a funcionalidade do servidor que não mapeia para uma inserção, atualização, exclusão ou operação de leitura.</span><span class="sxs-lookup"><span data-stu-id="00058-335">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="00058-336">Usando uma API personalizada, você pode ter mais controle sobre mensagens, incluindo ler e definir cabeçalhos de mensagens HTTP e definir um formato de corpo de mensagem diferente do JSON.</span><span class="sxs-lookup"><span data-stu-id="00058-336">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="00058-337">Você pode chamar uma API personalizada chamando um dos métodos [InvokeApiAsync] no cliente.</span><span class="sxs-lookup"><span data-stu-id="00058-337">You call a custom API by calling one of the [InvokeApiAsync] methods on the client.</span></span> <span data-ttu-id="00058-338">Por exemplo, a seguinte linha de código envia uma solicitação POST à API **completeAll** no back-end:</span><span class="sxs-lookup"><span data-stu-id="00058-338">For example, the following line of code sends a POST request to the **completeAll** API on the backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="00058-339">Essa forma é uma chamada de método tipada e exige que o tipo de retorno **MarkAllResult** seja definido.</span><span class="sxs-lookup"><span data-stu-id="00058-339">This form is a typed method call and requires that the **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="00058-340">Os dois métodos, tipado e não tipado, são aceitos.</span><span class="sxs-lookup"><span data-stu-id="00058-340">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="00058-341">O método InvokeApiAsync() precede '/api /' para a API que você deseja chamar, a menos que a API comece com '/'.</span><span class="sxs-lookup"><span data-stu-id="00058-341">The InvokeApiAsync() method prepends '/api/' to the API that you wish to call unless the API starts with a '/'.</span></span>
<span data-ttu-id="00058-342">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="00058-342">For example:</span></span>

* <span data-ttu-id="00058-343">`InvokeApiAsync("completeAll",...)` chama /api/completeAll no back-end</span><span class="sxs-lookup"><span data-stu-id="00058-343">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on the backend</span></span>
* <span data-ttu-id="00058-344">`InvokeApiAsync("/.auth/me",...)` chama /.auth/me no back-end</span><span class="sxs-lookup"><span data-stu-id="00058-344">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on the backend</span></span>

<span data-ttu-id="00058-345">Você pode usar InvokeApiAsync para chamar qualquer API Web, incluindo as que não são definidas com aplicativos móveis do Azure.</span><span class="sxs-lookup"><span data-stu-id="00058-345">You can use InvokeApiAsync to call any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="00058-346">Ao usar InvokeApiAsync(), os cabeçalhos apropriados, incluindo os cabeçalhos de autenticação, são enviados com a solicitação.</span><span class="sxs-lookup"><span data-stu-id="00058-346">When you use InvokeApiAsync(), the appropriate headers, including authentication headers, are sent with the request.</span></span>

## <span data-ttu-id="00058-347"><a name="authentication"></a>Autenticar usuários</span><span class="sxs-lookup"><span data-stu-id="00058-347"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="00058-348">Os Aplicativos Móveis dão suporte à autenticação e à autorização de usuários de aplicativo, usando vários provedores de identidade externos: Facebook, Google, Conta da Microsoft, Twitter e o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="00058-348">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="00058-349">Você pode definir permissões em tabelas para restringir o acesso a operações específicas apenas para usuários autenticados.</span><span class="sxs-lookup"><span data-stu-id="00058-349">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="00058-350">Você também pode usar a identidade de usuários autenticados para implementar regras de autorização em scripts do servidor.</span><span class="sxs-lookup"><span data-stu-id="00058-350">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="00058-351">Para obter mais informações, consulte o tutorial [Adicionar autenticação ao seu aplicativo].</span><span class="sxs-lookup"><span data-stu-id="00058-351">For more information, see the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="00058-352">Dois fluxos de autenticação têm suporte: fluxo *gerenciado pelo cliente* e fluxo *gerenciado pelo servidor*.</span><span class="sxs-lookup"><span data-stu-id="00058-352">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="00058-353">O fluxo gerenciado pelo servidor fornece a experiência de autenticação mais simples, pois depende da interface de autenticação da web do provedor.</span><span class="sxs-lookup"><span data-stu-id="00058-353">The server-managed flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="00058-354">O fluxo gerenciado pelo cliente permite uma integração mais profunda com recursos específicos ao dispositivo pois depende dos SDKs específicos ao provedor e ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="00058-354">The client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="00058-355">Recomendamos o uso de um fluxo gerenciado pelo cliente em seus aplicativos de produção.</span><span class="sxs-lookup"><span data-stu-id="00058-355">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="00058-356">Para configurar a autenticação, você precisa registrar seu aplicativo com um ou mais provedores de identidade.</span><span class="sxs-lookup"><span data-stu-id="00058-356">To set up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="00058-357">O provedor de identidade gera uma ID de cliente e um segredo do cliente para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="00058-357">The identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="00058-358">Esses valores são definidos no seu back-end para habilitar a autenticação/autorização de Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="00058-358">These values are then set in your backend to enable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="00058-359">Para saber mais, siga as instruções detalhadas no tutorial [Adicionar autenticação ao seu aplicativo].</span><span class="sxs-lookup"><span data-stu-id="00058-359">For more information, follow the detailed instructions in the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="00058-360">Os tópicos a seguir são abordados nesta seção:</span><span class="sxs-lookup"><span data-stu-id="00058-360">The following topics are covered in this section:</span></span>

* [<span data-ttu-id="00058-361">Autenticação gerenciada pelo cliente</span><span class="sxs-lookup"><span data-stu-id="00058-361">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="00058-362">Autenticação gerenciada pelo servidor</span><span class="sxs-lookup"><span data-stu-id="00058-362">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="00058-363">Armazenando o token de autenticação em cache</span><span class="sxs-lookup"><span data-stu-id="00058-363">Caching the authentication token</span></span>](#caching)

### <span data-ttu-id="00058-364"><a name="clientflow"></a>Autenticação gerenciada pelo cliente</span><span class="sxs-lookup"><span data-stu-id="00058-364"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="00058-365">Seu aplicativo pode entrar em contato de forma independente com o provedor de identidade e fornecer o token retornado durante o login com seu backend.</span><span class="sxs-lookup"><span data-stu-id="00058-365">Your app can independently contact the identity provider and then provide the returned token during login with your backend.</span></span> <span data-ttu-id="00058-366">Esse fluxo de cliente permite que você forneça uma experiência de logon único aos usuários ou recupere dados adicionais do usuário do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="00058-366">This client flow enables you to provide a single sign-on experience for users or to retrieve additional user data from the identity provider.</span></span> <span data-ttu-id="00058-367">É melhor usar a autenticação de fluxo de cliente do que usar um fluxo de servidor, já que o SDK do provedor de identidade fornece uma aparência mais nativa do UX e permite uma maior personalização.</span><span class="sxs-lookup"><span data-stu-id="00058-367">Client flow authentication is preferred to using a server flow as the identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="00058-368">Veja exemplos para os seguintes padrões de autenticação de fluxo de cliente:</span><span class="sxs-lookup"><span data-stu-id="00058-368">Examples are provided for the following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="00058-369">Biblioteca de Autenticação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="00058-369">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="00058-370">Facebook ou Google</span><span class="sxs-lookup"><span data-stu-id="00058-370">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="00058-371">Live SDK</span><span class="sxs-lookup"><span data-stu-id="00058-371">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="00058-372"><a name="adal"></a>Autenticar usuários com a Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="00058-372"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="00058-373">Você pode usar a ADAL (Biblioteca de autenticação do Active Directory) para iniciar a autenticação do usuário a partir do cliente usando a autenticação do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="00058-373">You can use the Active Directory Authentication Library (ADAL) to initiate user authentication from the client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="00058-374">Configure o seu back-end de aplicativo móvel para entrada no AAD seguindo o tutorial [Como configurar o Serviço de Aplicativo para logon no Active Directory] .</span><span class="sxs-lookup"><span data-stu-id="00058-374">Configure your mobile app backend for AAD sign-on by following the [How to configure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="00058-375">Complete a etapa opcional de registrar um aplicativo cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="00058-375">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="00058-376">No Visual Studio ou Xamarin Studio, abra o projeto e adicione uma referência ao pacote NuGet `Microsoft.IdentityModel.CLients.ActiveDirectory` .</span><span class="sxs-lookup"><span data-stu-id="00058-376">In Visual Studio or Xamarin Studio, open your project and add a reference to the `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="00058-377">Ao pesquisar, inclua versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="00058-377">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="00058-378">Adicione o código a seguir ao seu aplicativo, de acordo com a plataforma que você está usando.</span><span class="sxs-lookup"><span data-stu-id="00058-378">Add the following code to your application, according to the platform you are using.</span></span> <span data-ttu-id="00058-379">Em cada um, faça as seguintes substituições:</span><span class="sxs-lookup"><span data-stu-id="00058-379">In each, make the following replacements:</span></span>

   * <span data-ttu-id="00058-380">Substitua **INSERT-AUTHORITY-HERE** pelo nome do locatário no qual o aplicativo foi provisionado.</span><span class="sxs-lookup"><span data-stu-id="00058-380">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="00058-381">O formato deve ser https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="00058-381">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="00058-382">Esse valor pode ser copiado da guia Domínio no Azure Active Directory no [portal clássico do Azure].</span><span class="sxs-lookup"><span data-stu-id="00058-382">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="00058-383">Substitua **INSERT-RESOURCE-ID-HERE** pela ID do cliente do seu back-end de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="00058-383">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="00058-384">Você pode obter a ID do cliente na guia **Avançadas** em **Configurações do Azure Active Directory** no portal.</span><span class="sxs-lookup"><span data-stu-id="00058-384">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="00058-385">Substitua **INSERT-CLIENT-ID-HERE** pela ID do cliente copiada do aplicativo cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="00058-385">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="00058-386">Substitua **INSERT-REDIRECT-URI-HERE** pelo ponto de extremidade */.auth/login/done* do site, usando o esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="00058-386">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="00058-387">Esse valor deve ser similar a *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="00058-387">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="00058-388">Veja a seguir o código necessário para cada plataforma:</span><span class="sxs-lookup"><span data-stu-id="00058-388">The code needed for each platform follows:</span></span>

     <span data-ttu-id="00058-389">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="00058-389">**Windows:**</span></span>

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

     <span data-ttu-id="00058-390">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="00058-390">**Xamarin.iOS**</span></span>

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

     <span data-ttu-id="00058-391">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="00058-391">**Xamarin.Android**</span></span>

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

#### <span data-ttu-id="00058-392"><a name="client-facebook"></a>Entrada única usando um token do Facebook ou do Google</span><span class="sxs-lookup"><span data-stu-id="00058-392"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="00058-393">Você pode usar o fluxo de cliente como mostra este trecho de código para o Facebook ou o Google.</span><span class="sxs-lookup"><span data-stu-id="00058-393">You can use the client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using the Facebook or Google SDK.
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
            // to MobileServiceAuthenticationProvider.Google if using Google auth.
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

#### <span data-ttu-id="00058-394"><a name="client-livesdk"></a>Logon único usando a Conta da Microsoft com o Live SDK</span><span class="sxs-lookup"><span data-stu-id="00058-394"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with the Live SDK</span></span>
<span data-ttu-id="00058-395">Para autenticar usuários, você deverá registrar seu aplicativo na Central de desenvolvedores da conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="00058-395">To authenticate users, you must register your app at the Microsoft account Developer Center.</span></span> <span data-ttu-id="00058-396">Configure os detalhes do registro no back-end do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="00058-396">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="00058-397">Para criar um registro de conta da Microsoft e conectá-lo ao back-end do Aplicativo Móvel., conclua as etapas em [Registrar seu aplicativo para usar um logon de conta da Microsoft].</span><span class="sxs-lookup"><span data-stu-id="00058-397">To create a Microsoft account registration and connect it to your Mobile App backend, complete the steps in [Register your app to use a Microsoft account login].</span></span> <span data-ttu-id="00058-398">Se você tiver as versões da Windows Store e do Windows Phone 8/Silverlight de seu aplicativo, registre a versão da Windows Store primeiro.</span><span class="sxs-lookup"><span data-stu-id="00058-398">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register the Windows Store version first.</span></span>

<span data-ttu-id="00058-399">O código a seguir é autenticado usando o Live SDK e usa o token retornado para entrar no back-end do seu Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="00058-399">The following code authenticates using Live SDK and uses the returned token to sign in to your Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get the URL the Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create the authentication client for Windows Store using the service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create the authentication client for Windows Phone using the client ID of the registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request the authentication token from the Live authentication service.
        // The wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about the logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use the Microsoft account auth token to sign in to App Service.
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

<span data-ttu-id="00058-400">Para saber mais, confira a documentação do [SDK do Windows Live] .</span><span class="sxs-lookup"><span data-stu-id="00058-400">For more information, see the [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="00058-401"><a name="serverflow"></a>Autenticação gerenciada pelo servidor</span><span class="sxs-lookup"><span data-stu-id="00058-401"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="00058-402">Depois de registrar seu provedor de identidade, chame o método [LoginAsync] no [MobileServiceClient] com o valor [MobileServiceAuthenticationProvider] de seu provedor.</span><span class="sxs-lookup"><span data-stu-id="00058-402">Once you have registered your identity provider, call the [LoginAsync] method on the [MobileServiceClient] with the [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="00058-403">Por exemplo, o código a seguir inicia uma entrada de fluxo do servidor usando o Facebook.</span><span class="sxs-lookup"><span data-stu-id="00058-403">For example, the following code initiates a server flow sign-in by using Facebook.</span></span>

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

<span data-ttu-id="00058-404">Se você estiver usando um provedor de identidade além do Facebook, altere o valor [MobileServiceAuthenticationProvider] para o valor de seu provedor.</span><span class="sxs-lookup"><span data-stu-id="00058-404">If you are using an identity provider other than Facebook, change the value of [MobileServiceAuthenticationProvider] to the value for your provider.</span></span>

<span data-ttu-id="00058-405">Em um fluxo de servidor, o Serviço de Aplicativo do Azure gerencia o fluxo de autenticação OAuth exibindo a página de entrada do provedor selecionado.</span><span class="sxs-lookup"><span data-stu-id="00058-405">In a server flow, Azure App Service manages the OAuth authentication flow by displaying the sign-in page of the selected provider.</span></span>  <span data-ttu-id="00058-406">Depois que o provedor de identidade retorna, o Serviço de Aplicativo do Azure gera um token de autenticação do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="00058-406">Once the identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="00058-407">O método [LoginAsync] retorna um [MobileServiceUser], que fornece a [UserId] do usuário autenticado e o [MobileServiceAuthenticationToken] como um JWT (token da Web JSON).</span><span class="sxs-lookup"><span data-stu-id="00058-407">The [LoginAsync] method returns a [MobileServiceUser], which provides both the [UserId] of the authenticated user and the [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="00058-408">Esse token pode ser armazenado em cache e reutilizado até que expire.</span><span class="sxs-lookup"><span data-stu-id="00058-408">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="00058-409">Para obter mais informações, consulte [Armazenando o token de autenticação em cache](#caching).</span><span class="sxs-lookup"><span data-stu-id="00058-409">For more information, see [Caching the authentication token](#caching).</span></span>

### <span data-ttu-id="00058-410"><a name="caching"></a>Armazenando o token de autenticação em cache</span><span class="sxs-lookup"><span data-stu-id="00058-410"><a name="caching"></a>Caching the authentication token</span></span>
<span data-ttu-id="00058-411">Em alguns casos, a chamada para o método de logon pode ser evitada após a primeira autenticação bem-sucedida armazenando o token de autenticação do provedor.</span><span class="sxs-lookup"><span data-stu-id="00058-411">In some cases, the call to the login method can be avoided after the first successful authentication by storing the authentication token from the provider.</span></span>  <span data-ttu-id="00058-412">Os aplicativos da Windows Store e UWP podem usar [PasswordVault] para armazenar em cache o token de autenticação atual após uma conexão bem-sucedida, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="00058-412">Windows Store and UWP apps can use [PasswordVault] to cache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="00058-413">O valor de UserId é armazenado como o UserName da credencial e o token é armazenado como a Senha.</span><span class="sxs-lookup"><span data-stu-id="00058-413">The UserId value is stored as the UserName of the credential and the token is the stored as the Password.</span></span> <span data-ttu-id="00058-414">Em inicializações subsequentes, você pode verificar o **PasswordVault** para ter acesso às credenciais armazenadas em cache.</span><span class="sxs-lookup"><span data-stu-id="00058-414">On subsequent start-ups, you can check the **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="00058-415">O exemplo a seguir usa as credenciais armazenadas em cache quando elas forem encontradas e tenta autenticar novamente com o back-end:</span><span class="sxs-lookup"><span data-stu-id="00058-415">The following example uses cached credentials when they are found, and otherwise attempts to authenticate again with the backend:</span></span>

```
// Try to retrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create the current user from the stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache the token as shown above.
}
```

<span data-ttu-id="00058-416">Quando você faz o logoff de um usuário, também deve remover a credencial armazenada, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="00058-416">When you sign out a user, you must also remove the stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="00058-417">Os aplicativos Xamarin usam as APIs [Xamarin.Auth] para armazenar com segurança as credenciais em um objeto **Account** .</span><span class="sxs-lookup"><span data-stu-id="00058-417">Xamarin    apps use the [Xamarin.Auth] APIs to securely store credentials in an **Account** object.</span></span> <span data-ttu-id="00058-418">Para obter um exemplo de como usar essas APIs, confira o arquivo de código [AuthStore.cs] no [exemplo de compartilhamento de fotos de ContosoMoments](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="00058-418">For an example of using these APIs, see the [AuthStore.cs] code file in the [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="00058-419">Quando você usa a autenticação gerenciada pelo cliente, também pode armazenar em cache o token de acesso obtido de seu provedor, como o Facebook ou Twitter.</span><span class="sxs-lookup"><span data-stu-id="00058-419">When you use client-managed authentication, you can also cache the access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="00058-420">Esse token pode ser fornecido para solicitar um novo token de autenticação a partir do back-end, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="00058-420">This token can be supplied to request a new authentication token from the backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using the access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="00058-421"><a name="pushnotifications"></a>Notificações por Push</span><span class="sxs-lookup"><span data-stu-id="00058-421"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="00058-422">Os tópicos a seguir abordam Notificações por Push:</span><span class="sxs-lookup"><span data-stu-id="00058-422">The following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="00058-423">Registrar notificações por push</span><span class="sxs-lookup"><span data-stu-id="00058-423">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="00058-424">Obter um SID do pacote da Windows Store</span><span class="sxs-lookup"><span data-stu-id="00058-424">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="00058-425">Registrar com modelos de Plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="00058-425">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="00058-426"><a name="register-for-push"></a>Como se registrar para receber notificações por push</span><span class="sxs-lookup"><span data-stu-id="00058-426"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="00058-427">O cliente de Aplicativos Móveis permite que você se registrar para notificações por push com Hubs de Notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="00058-427">The Mobile Apps client enables you to register for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="00058-428">Ao se registrar, você obtém um identificador obtido do PNS (Serviço de Notificação por Push) específico da plataforma.</span><span class="sxs-lookup"><span data-stu-id="00058-428">When registering, you obtain a handle that you obtain from the platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="00058-429">Então fornece este valor, juntamente com quaisquer marcas, no momento em que cria o registro.</span><span class="sxs-lookup"><span data-stu-id="00058-429">You then provide this value along with any tags when you create the registration.</span></span> <span data-ttu-id="00058-430">O seguinte código registra seu aplicativo do Windows para notificações de push no WNS (Serviço de Notificação do Windows):</span><span class="sxs-lookup"><span data-stu-id="00058-430">The following code registers your Windows app for push notifications with the Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using the new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="00058-431">Se você estiver enviando WNS, DEVERÁ [obter um SID do pacote da Windows Store](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="00058-431">If you are pushing to WNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="00058-432">Para saber mais sobre os aplicativos do Windows, inclusive como se registrar para obter registros de modelo, confira [Adicionar notificações por push ao seu aplicativo].</span><span class="sxs-lookup"><span data-stu-id="00058-432">For more information on Windows apps, including how to register for template registrations, see [Add push notifications to your app].</span></span>

<span data-ttu-id="00058-433">A solicitação de marcas do cliente não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="00058-433">Requesting tags from the client is not supported.</span></span>  <span data-ttu-id="00058-434">As solicitações de marca são descartadas silenciosamente do registro.</span><span class="sxs-lookup"><span data-stu-id="00058-434">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="00058-435">Se você deseja registrar seu dispositivo com marcas, crie uma API personalizada que usa a API de Hubs de Notificação para realizar o registro em seu nome.</span><span class="sxs-lookup"><span data-stu-id="00058-435">If you wish to register your device with tags, create a Custom API that uses the Notification Hubs API to perform the registration on your behalf.</span></span>  <span data-ttu-id="00058-436">[Chame a API Personalizada](#customapi) em vez do método `RegisterNativeAsync()`.</span><span class="sxs-lookup"><span data-stu-id="00058-436">[Call the Custom API](#customapi) instead of the `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="00058-437"><a name="package-sid"></a>Como obter um SID do pacote da Windows Store</span><span class="sxs-lookup"><span data-stu-id="00058-437"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="00058-438">Um SID de pacote é necessário para habilitar notificações por push em aplicativos da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="00058-438">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="00058-439">Registre seu aplicativo na Windows Store para receber um SID do pacote.</span><span class="sxs-lookup"><span data-stu-id="00058-439">To receive a package SID, register your application with the Windows Store.</span></span>

<span data-ttu-id="00058-440">Para obter esse valor:</span><span class="sxs-lookup"><span data-stu-id="00058-440">To obtain this value:</span></span>

1. <span data-ttu-id="00058-441">No Gerenciador de Soluções do Visual Studio, clique com o botão direito do mouse no projeto do aplicativo da Windows Store, clique em **Armazenar** > **Associar Aplicativo à Store...**.</span><span class="sxs-lookup"><span data-stu-id="00058-441">In Visual Studio Solution Explorer, right-click the Windows Store app project, click **Store** > **Associate App with the Store...**.</span></span>
2. <span data-ttu-id="00058-442">No assistente, clique em **Avançar**, entre com sua conta da Microsoft, digite um nome para seu aplicativo em **Reservar um novo nome de aplicativo** e clique em **Reservar**.</span><span class="sxs-lookup"><span data-stu-id="00058-442">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="00058-443">Depois que o registro do aplicativo for criado com êxito, selecione o nome do aplicativo, clique em **Avançar** e em **Associar**.</span><span class="sxs-lookup"><span data-stu-id="00058-443">After the app registration is successfully created, select the app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="00058-444">Faça logon na [Central de Desenvolvimento do Windows] usando a sua Conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="00058-444">Log in to the [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="00058-445">Em **Meus aplicativos**, clique no registro de aplicativo que você criou.</span><span class="sxs-lookup"><span data-stu-id="00058-445">Under **My apps**, click the app registration you created.</span></span>
5. <span data-ttu-id="00058-446">Clique em **Gerenciamento de aplicativos** > **Identidade de aplicativos** e, em seguida, role para baixo até encontrar o **SID do Pacote**.</span><span class="sxs-lookup"><span data-stu-id="00058-446">Click **App management** > **App identity**, and then scroll down to find your **Package SID**.</span></span>

<span data-ttu-id="00058-447">Muitos usos do SID do pacote o tratam como um URI; nesse caso, você precisa usar *ms-app://* como o esquema.</span><span class="sxs-lookup"><span data-stu-id="00058-447">Many uses of the package SID treat it as a URI, in which case you need to use *ms-app://* as the scheme.</span></span> <span data-ttu-id="00058-448">Anote a versão do SID do pacote formado pela concatenação desse valor como um prefixo.</span><span class="sxs-lookup"><span data-stu-id="00058-448">Make note of the version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="00058-449">Os aplicativos Xamarin exigem mais código para poder registrar um aplicativo em execução nas plataformas iOS ou Android.</span><span class="sxs-lookup"><span data-stu-id="00058-449">Xamarin apps require some additional code to be able to register an app running on the iOS or Android platforms.</span></span> <span data-ttu-id="00058-450">Para saber mais, confira o tópico para sua plataforma:</span><span class="sxs-lookup"><span data-stu-id="00058-450">For more information, see the topic for your platform:</span></span>

* [<span data-ttu-id="00058-451">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="00058-451">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="00058-452">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="00058-452">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="00058-453"><a name="register-xplat"></a>Como registrar modelos de envio por push para enviar notificações entre plataformas</span><span class="sxs-lookup"><span data-stu-id="00058-453"><a name="register-xplat"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="00058-454">Para registrar modelos, use o método `RegisterAsync()` com os modelos, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="00058-454">To register templates, use the `RegisterAsync()` method with the templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="00058-455">Seus modelos devem ser do tipo `JObject` e podem conter vários modelos no seguinte formato JSON:</span><span class="sxs-lookup"><span data-stu-id="00058-455">Your templates should be `JObject` types and can contain multiple templates in the following JSON format:</span></span>

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

<span data-ttu-id="00058-456">O método **RegisterAsync()** também aceita Blocos Secundários:</span><span class="sxs-lookup"><span data-stu-id="00058-456">The method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="00058-457">Todas as marcações são retiradas durante o registro para segurança.</span><span class="sxs-lookup"><span data-stu-id="00058-457">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="00058-458">Para adicionar marcas a instalações ou modelos dentro de instalações, confira [Trabalhar com o SDK do servidor de back-end do .NET para Aplicativos Móveis do Azure].</span><span class="sxs-lookup"><span data-stu-id="00058-458">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="00058-459">Para enviar notificações usando esses modelos registrados, consulte as [APIs dos Hubs de Notificação].</span><span class="sxs-lookup"><span data-stu-id="00058-459">To send notifications utilizing these registered templates, refer to the [Notification Hubs APIs].</span></span>

## <span data-ttu-id="00058-460"><a name="misc"></a>Tópicos Diversos</span><span class="sxs-lookup"><span data-stu-id="00058-460"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="00058-461"><a name="errors"></a>Como tratar erros</span><span class="sxs-lookup"><span data-stu-id="00058-461"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="00058-462">Quando ocorre um erro no back-end, o SDK do cliente dispara uma `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="00058-462">When an error occurs in the backend, the client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="00058-463">O seguinte exemplo mostra como manipular uma exceção que é retornada pelo back-end:</span><span class="sxs-lookup"><span data-stu-id="00058-463">The following example shows how to handle an exception that is returned by the backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into the database. When the operation completes
    // and App Service has assigned an Id, the item is added to the CollectionView
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

<span data-ttu-id="00058-464">Outro exemplo de lidar com condições de erro pode ser encontrado no [exemplo de arquivos de Aplicativos Móveis].</span><span class="sxs-lookup"><span data-stu-id="00058-464">Another example of dealing with error conditions can be found in the [Mobile Apps Files Sample].</span></span> <span data-ttu-id="00058-465">O exemplo de [LoggingHandler] fornece um manipulador de representante de registro em log para registrar as solicitações que estão sendo feitas no back-end.</span><span class="sxs-lookup"><span data-stu-id="00058-465">The [LoggingHandler] example provides a logging delegate handler to log the requests being made to the backend.</span></span>

### <span data-ttu-id="00058-466"><a name="headers"></a>Como personalizar cabeçalhos de solicitação</span><span class="sxs-lookup"><span data-stu-id="00058-466"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="00058-467">Para dar suporte ao seu cenário específico de aplicativo, convém personalizar a comunicação com o back-end do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="00058-467">To support your specific app scenario, you might need to customize communication with the Mobile App backend.</span></span> <span data-ttu-id="00058-468">Por exemplo, convém adicionar um cabeçalho personalizado para cada solicitação de saída, ou até mesmo alterar códigos de status de respostas.</span><span class="sxs-lookup"><span data-stu-id="00058-468">For example, you may want to add a custom header to every outgoing request or even change responses status codes.</span></span> <span data-ttu-id="00058-469">Você pode usar um [DelegatingHandler]personalizado, como no exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="00058-469">You can use a custom [DelegatingHandler], as in the following example:</span></span>

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
        // Change the request-side here based on the HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do the request
        var response = await base.SendAsync(request, cancellationToken);

        // Change the response-side here based on the HttpResponseMessage

        // Return the modified response
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

<span data-ttu-id="00058-470">[Adicionar autenticação ao seu aplicativo]: app-service-mobile-windows-store-dotnet-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="00058-470">[Add authentication to your app]: app-service-mobile-windows-store-dotnet-get-started-users.md</span></span>
<span data-ttu-id="00058-471">[Sincronização de Dados Offline nos Aplicativos Móveis do Azure]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="00058-471">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="00058-472">[Adicionar notificações por push ao seu aplicativo]: app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="00058-472">[Add push notifications to your app]: app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="00058-473">[Registrar seu aplicativo para usar um logon de conta da Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="00058-473">[Register your app to use a Microsoft account login]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="00058-474">[Como configurar o Serviço de Aplicativo para logon no Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="00058-474">[How to configure App Service for Active Directory login]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>

<!-- Microsoft URLs. -->
<span data-ttu-id="00058-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-481">[cria uma referência para uma tabela não tipada]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-481">[creates a reference to an untyped table]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-493">[Ignorar]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span><span class="sxs-lookup"><span data-stu-id="00058-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span></span>
<span data-ttu-id="00058-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span></span>
<span data-ttu-id="00058-497">[portal do Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="00058-497">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="00058-498">[portal clássico do Azure]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="00058-498">[Azure classic portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="00058-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span><span class="sxs-lookup"><span data-stu-id="00058-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span></span>
<span data-ttu-id="00058-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span></span>
<span data-ttu-id="00058-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span><span class="sxs-lookup"><span data-stu-id="00058-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span></span>
<span data-ttu-id="00058-502">[Central de Desenvolvimento do Windows]: https://dev.windows.com/en-us/overview</span><span class="sxs-lookup"><span data-stu-id="00058-502">[Windows Dev Center]: https://dev.windows.com/en-us/overview</span></span>
<span data-ttu-id="00058-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="00058-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span></span>
<span data-ttu-id="00058-504">[SDK do Windows Live]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span><span class="sxs-lookup"><span data-stu-id="00058-504">[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span></span>
<span data-ttu-id="00058-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span><span class="sxs-lookup"><span data-stu-id="00058-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span></span>
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
<span data-ttu-id="00058-506">[APIs dos Hubs de Notificação]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span><span class="sxs-lookup"><span data-stu-id="00058-506">[Notification Hubs APIs]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span></span>
<span data-ttu-id="00058-507">[exemplo de arquivos de Aplicativos Móveis]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span><span class="sxs-lookup"><span data-stu-id="00058-507">[Mobile Apps Files Sample]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span></span>
<span data-ttu-id="00058-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span><span class="sxs-lookup"><span data-stu-id="00058-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span></span>

<!-- External URLs -->
<span data-ttu-id="00058-509">[Documentação do OData v3]: http://www.odata.org/documentation/odata-version-3-0/</span><span class="sxs-lookup"><span data-stu-id="00058-509">[OData v3 Documentation]: http://www.odata.org/documentation/odata-version-3-0/</span></span>
<span data-ttu-id="00058-510">[Fiddler]: http://www.telerik.com/fiddler</span><span class="sxs-lookup"><span data-stu-id="00058-510">[Fiddler]: http://www.telerik.com/fiddler</span></span>
<span data-ttu-id="00058-511">[Json.NET]: http://www.newtonsoft.com/json</span><span class="sxs-lookup"><span data-stu-id="00058-511">[Json.NET]: http://www.newtonsoft.com/json</span></span>
<span data-ttu-id="00058-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span><span class="sxs-lookup"><span data-stu-id="00058-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span></span>
<span data-ttu-id="00058-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span><span class="sxs-lookup"><span data-stu-id="00058-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span></span>
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
