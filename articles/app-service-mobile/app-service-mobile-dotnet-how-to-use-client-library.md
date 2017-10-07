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
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a>Como toouse Olá gerenciada do cliente para aplicativos móveis do Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a>Visão geral
Este guia mostra como os cenários comuns de tooperform usando Olá gerenciados biblioteca de cliente para aplicativos do Azure aplicativo serviços móveis aplicativos para Windows e Xamarin. Se você estiver tooMobile de novos aplicativos, você deve considerar primeiro Olá Concluindo [início rápido de aplicativos do Azure Mobile] [ 1] tutorial. Este guia, vamos nos concentrar em saudação do cliente gerenciado SDK. toolearn mais sobre hello SDKs do lado do servidor para aplicativos móveis, consulte a documentação Olá Olá [SDK do .NET Server] [ 2] ou [Node. js servidor SDK] [ 3].

## <a name="reference-documentation"></a>Documentação de referência
Olá documentação de referência do SDK do cliente hello está localizada aqui: [referência de cliente .NET de aplicativos móveis do Azure][4].
Você também pode encontrar vários exemplos de cliente em Olá [repositório GitHub de exemplos do Azure][5].

## <a name="supported-platforms"></a>Plataformas com suporte
Olá plataforma .NET oferece suporte a saudação plataformas a seguir:

* Versões de Xamarin Android para API 19 a 24 (KitKat usando Nougat)
* Versões de Xamarin iOS para versões 8.0 e posteriores do iOS
* Plataforma Universal do Windows
* Windows Phone 8,1
* Windows Phone 8.0, exceto para aplicativos Silverlight

autenticação de "server-fluxo" Hello usa WebView para Olá apresentado da interface do usuário.  Se o dispositivo de saudação não for capaz de toopresent uma UI WebView, outros métodos de autenticação são necessários.  Esse SDK, portanto, não é adequado para relógios ou dispositivos similarmente restritos.

## <a name="setup"></a>Configuração e Pré-requisitos
Supomos que você já criou e publicou o projeto de back-end do Aplicativo Móvel, que inclui pelo menos uma tabela.  No código de saudação usado neste tópico, a tabela de saudação é denominada `TodoItem` e ele tem Olá colunas a seguir: `Id`, `Text`, e `Complete`. Esta tabela é hello mesma tabela criada quando você concluir o [início rápido de aplicativos do Azure Mobile][1].

Olá digitado cliente tipo correspondente no c# é Olá classe a seguir:

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

Olá [JsonPropertyAttribute] [ 6] é usado toodefine hello *PropertyName* mapeamento entre os campos de cliente hello e Olá tabela.

toolearn como toocreate tabelas em seu back-end de aplicativos móveis, consulte Olá [tópico sobre o SDK do .NET Server] [ 7] ou hello [tópico sobre o SDK do servidor Node.js] [ 8] . Se você tiver criado seu back-end do aplicativo móvel no hello Azure portal usando Olá início rápido, você também pode usar o hello **tabelas fácil** definindo no hello [portal do Azure].

### <a name="how-to-install-hello-managed-client-sdk-package"></a>Como: instalar Olá gerenciados pacote do SDK de cliente
Usar um dos Olá Olá de tooinstall métodos a seguir gerenciados pacote do SDK de cliente para aplicativos móveis do [NuGet][9]:

* **O Visual Studio** seu projeto, clique **gerenciar pacotes NuGet**, pesquise Olá `Microsoft.Azure.Mobile.Client` do pacote e, em seguida, clique em **instalar**.
* **Xamarin Studio** seu projeto, clique **adicionar** > **adicionar pacotes do NuGet**, pesquise Olá `Microsoft.Azure.Mobile.Client `do pacote e, em seguida, clique em **adicionar Pacote**.

No arquivo principal de atividade, lembre-se a seguir Olá tooadd **usando** instrução:

```
using Microsoft.WindowsAzure.MobileServices;
```

### <a name="symbolsource"></a>Como trabalhar com símbolos de depuração no Visual Studio
símbolos de Olá Olá Microsoft.Azure.Mobile namespace estão disponíveis em [SymbolSource][10].  Consulte toothe [SymbolSource instruções] [ 11] toointegrate SymbolSource com o Visual Studio.

## <a name="create-client"></a>Crie saudação do cliente de aplicativos móveis
Olá, código a seguir cria Olá [MobileServiceClient] [ 12] objeto que é usado tooaccess seu back-end do aplicativo móvel.

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

Olá anterior do código, substitua `MOBILE_APP_URL` com URL de saudação do back-end de aplicativo móvel Olá, que se encontra na folha para seu back-end do aplicativo móvel no hello [portal do Azure]. objeto MobileServiceClient de saudação deve ser um singleton.

## <a name="work-with-tables"></a>Trabalhar com tabelas
Olá detalhes da seção a seguir como toosearch e recuperar os registros e modificar dados de saudação na tabela de saudação.  Olá seguintes tópicos é abordado:

* [Criar uma referência de tabela](#instantiating)
* [Consultar dados](#querying)
* [Filtrar dados retornados](#filtering)
* [Classificar dados retornados](#sorting)
* [Retornar dados em páginas](#paging)
* [Selecionar colunas específicas](#selecting)
* [Pesquisar um registro por ID](#lookingup)
* [Lidando com consultas sem tipo](#untypedqueries)
* [Inserindo dados](#inserting)
* [Atualizando dados](#updating)
* [Excluindo dados](#deleting)
* [Resolução de Conflitos e Simultaneidade Otimista](#optimisticconcurrency)
* [Associação tooa Interface de usuário do Windows](#binding)
* [Olá alterar tamanho da página](#pagesize)

### <a name="instantiating"></a>Como criar uma referência de tabela
Todos os códigos de saudação que acessa ou modificam dados em uma tabela de back-end chama funções em Olá `MobileServiceTable` objeto. Obter uma tabela de referência toohello Olá chamada [GetTable] método, da seguinte maneira:

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

Olá retornou objeto usa o modelo de serialização do tipo de saudação. Também há suporte para um modelo de serialização não tipado. O exemplo a seguir [cria uma tabela sem tipo de referência de tooan]:

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

Consultas sem tipo, você deve especificar Olá subjacente a cadeia de caracteres de consulta OData.

### <a name="querying"></a>Como consultar dados do seu Aplicativo Móvel
Esta seção descreve como as consultas tooissue toohello aplicativo móvel back-end, que inclui a saudação funcionalidade a seguir:

* [Filtrar dados retornados](#filtering)
* [Classificar dados retornados](#sorting)
* [Retornar dados em páginas](#paging)
* [Selecionar colunas específicas](#selecting)
* [Pesquisar dados por ID](#lookingup)

> [!NOTE]
> Um tamanho de página orientado para servidor é imposta tooprevent todas as linhas sejam retornadas.  Paginação impede que solicitações de padrão para grandes conjuntos de dados comprometendo o serviço de saudação.  tooreturn mais de 50 linhas, use Olá `Skip` e `Take` método, conforme descrito em [retornar dados em páginas](#paging).

### <a name="filtering"></a>Como filtrar dados retornados
Olá código a seguir ilustra como dados toofilter, incluindo um `Where` cláusula em uma consulta. Retorna todos os itens do `todoTable` cujo `Complete` propriedade é igual muito`false`. Olá [onde] função aplica uma predicado de consulta de saudação na tabela de saudação de filtragem de linha.

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

Você pode exibir hello URI de back-end toohello de solicitação enviada hello usando software de inspeção de mensagem, como ferramentas de desenvolvedor do navegador ou [Fiddler]. Se você observar o URI de solicitação hello, observe que a cadeia de caracteres de consulta de saudação é modificada:

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

Essa solicitação OData é convertida em uma consulta SQL por Olá SDK do servidor:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

Olá função que é passada toohello `Where` método pode ter um número arbitrário de condições.

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

Este exemplo deve ser convertido em uma consulta SQL por Olá SDK do servidor:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

Essa consulta pode ser dividida em várias cláusulas:

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

Olá dois métodos são equivalentes e podem ser usados alternadamente.  Olá opção&mdash;da concatenação de vários predicados em uma consulta&mdash;é mais compacto e recomendado.

Olá `Where` cláusula dá suporte a operações que ser convertido em um subconjunto de OData hello. As operações incluem:

* Operadores relacionais (==,!=, <, <=, >, >=),
* Operadores aritméticos (+, -, /, *, %),
* Número de precisão (Math.Floor, Math.Ceiling),
* Funções de cadeia de caracteres (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),
* Propriedades de data (ano, mês, dia, hora, minuto, segundo),
* Propriedades de acesso de um objeto e
* Expressões que combinam qualquer uma dessas operações.

Quando considerando o que Olá servidor SDK dá suporte a, você pode considerar Olá [OData v3 documentação].

### <a name="sorting"></a>Como classificar dados retornados
Olá código a seguir ilustra como dados toosort, incluindo um [OrderBy] ou [OrderByDescending] função na consulta de saudação. Retorna os itens do `todoTable` classificada em ordem crescente por Olá `Text` campo.

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

### <a name="paging"></a>Como retornar dados em páginas
Por padrão, Olá back-end retorna apenas Olá primeiras 50 linhas. Você pode aumentar o número de saudação de linhas retornados pela chamada hello [levar] método. Use `Take` juntamente com hello [ignorar] método toorequest uma "página específica" do conjunto de dados total Olá retornada pela consulta hello. Olá consulta a seguir, quando executada, retorna Olá três principais itens na tabela de saudação.

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

ignora a seguinte consulta revisada Olá Olá três primeiros resultados e retorna Olá três resultados. Essa consulta gera Olá segunda "página" de dados, onde o tamanho da página Olá é três itens.

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

Olá [IncludeTotalCount] método solicita a contagem total de saudação para *todos os* Olá registros que teriam sido retornados, ignorando qualquer cláusula de paginação/limite especificada:

```
query = query.IncludeTotalCount();
```

Em um aplicativo do mundo real, você pode usar consultas toohello semelhante anterior de exemplo com um controle de pager ou a interface de usuário comparável para navegar entre páginas.

> [!NOTE]
> limite de 50 linhas toooverride Olá em um back-end do aplicativo móvel, você deve aplicar Olá [EnableQueryAttribute] toohello público método GET e especifique o comportamento de paginação hello. Quando o método de toohello aplicada, Olá a seguir define too1000 o máximo de linhas retornadas:
>
> `[EnableQuery(MaxTop=1000)]`


### <a name="selecting"></a>Como selecionar colunas específicas
Você pode especificar qual conjunto de propriedades tooinclude em Olá resultados adicionando um [selecione] consulta de tooyour cláusula. Olá, por exemplo, o seguinte código mostra como tooselect apenas um campo e também como tooselect e vários campos de formato:

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

Todos os Olá funções descritas até agora são aditivas, portanto, pode manter encadeamento-los. Cada chamada encadeada afeta mais consulta hello. Mais um exemplo:

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <a name="lookingup"></a>Como pesquisar dados pela ID
Olá [LookupAsync] função pode ser usado toolook objetos de banco de dados de saudação com uma ID específica

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <a name="untypedqueries"></a>Como executar consultas sem tipo
Ao executar uma consulta usando um objeto de tabela sem tipo, você deve especificar explicitamente a cadeia de caracteres de consulta de OData Olá chamando [ReadAsync], conforme mostrado no exemplo a seguir de saudação:

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

Você recupera valores JSON que podem ser usados como um recipiente de propriedades. Para obter mais informações sobre JToken e Newtonsoft Json.NET, consulte Olá [Json.NET] site.

### <a name="inserting"></a>Como inserir dados em um back-end do Aplicativo Móvel
Todos os tipos de cliente devem conter um membro chamado **Id**, que é por padrão uma cadeia de caracteres. Isso **Id** é necessário para executar operações CRUD e para sincronização offline. Olá código a seguir ilustra como Olá toouse [InsertAsync] método tooinsert novas linhas em uma tabela. parâmetro Hello contém Olá dados toobe inserido como um objeto .NET.

```
await todoTable.InsertAsync(todoItem);
```

Se um valor de ID exclusivo personalizado não será incluído no hello `todoItem` durante uma inserção, um GUID gerado pelo servidor de saudação.
Você pode recuperar Olá Id gerada inspecionando o objeto Olá depois Olá chamada retorna.

tooinsert sem tipo de dados, você pode tirar proveito do Json.NET:

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

Aqui está um exemplo usando um endereço de email como uma id de cadeia de caracteres exclusiva:

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a>Trabalhando com valores de ID
Aplicativos móveis dá suporte a valores de cadeia de caracteres personalizada exclusivo para a tabela de saudação **id** coluna. Um valor de cadeia de caracteres permite que aplicativos toouse de valores personalizados, como endereços de email ou nomes de usuário para ID de saudação.  IDs de cadeia de caracteres fornecem Olá benefícios a seguir:

* IDs são gerados sem fazer um banco de dados de toohello de ida e volta.
* Os registros são toomerge mais fácil de tabelas diferentes ou bancos de dados.
* Os valores de IDs podem integrar-se melhor a uma lógica do aplicativo.

Quando um valor de ID de cadeia de caracteres não está definido em um registro inserido, o back-end de aplicativo móvel hello gera um valor exclusivo para a ID. Você pode usar o hello [Guid.NewGuid] toogenerate método sua própria ID de valores, no cliente de saudação ou em Olá back-end.

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <a name="modifying"></a>Como modificar dados em um back-end de Aplicativo Móvel
Olá código a seguir ilustra como Olá toouse [UpdateAsync] método tooupdate um registro existente com hello mesmo ID com novas informações. parâmetro Hello contém Olá dados toobe atualizada como um objeto .NET.

```
await todoTable.UpdateAsync(todoItem);
```

tooupdate sem tipo de dados, você pode tirar proveito do [Json.NET] da seguinte maneira:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

Um campo `id` deve ser especificado ao fazer uma atualização. Olá back-end usa Olá `id` tooidentify campo qual linha tooupdate. Olá `id` campo pode ser obtido dos resultados de saudação do hello `InsertAsync` chamar. Um `ArgumentException` é gerado se você tentar tooupdate um item sem fornecer Olá `id` valor.

### <a name="deleting"></a>Como excluir dados em um back-end do Aplicativo Móvel
Olá código a seguir ilustra como Olá toouse [DeleteAsync] método toodelete uma instância existente. Olá instância é identificada por Olá `id` campo de conjunto de saudação `todoItem`.

```
await todoTable.DeleteAsync(todoItem);
```

toodelete sem tipo de dados, você pode tirar proveito do Json.NET da seguinte maneira:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

Quando você faz uma solicitação de exclusão, uma ID deve ser especificada. Outras propriedades não são passadas para o serviço de toohello ou são ignoradas no serviço de saudação. Olá o resultado de uma `DeleteAsync` costuma ser chamada `null`. Olá ID toopass no pode ser obtido de resultado de saudação da saudação `InsertAsync` chamar. Um `MobileServiceInvalidOperationException` é gerada quando você tentar toodelete um item sem especificar Olá `id` campo.

### <a name="optimisticconcurrency"></a>Como usar a simultaneidade otimista para resolução de conflitos
Dois ou mais clientes podem gravar alterações toohello mesmo item no hello mesmo tempo. Sem detecção de conflito, a última gravação do hello substituiria todas as atualizações anteriores. **Controle de simultaneidade otimista** pressupõe que cada transação possa ser confirmada e, portanto, não usa nenhum recurso de bloqueio.  Antes de confirmar uma transação, o controle de simultaneidade otimista verifica que nenhuma outra transação ter modificado os dados de saudação. Se dados saudação tem sido modificados, Olá confirmando a transação será revertida.

Aplicativos móveis dá suporte ao controle de simultaneidade otimista rastreando o item de tooeach de alterações usando Olá `version` coluna de propriedade do sistema que é definida para cada tabela em seu back-end do aplicativo móvel. Cada vez que um registro é atualizado, os aplicativos móveis define Olá `version` propriedade para que registre tooa novo valor. Durante cada solicitação de atualização, Olá `version` propriedade de registro de saudação incluído na solicitação de saudação é toohello em comparação com o mesma propriedade de registro de saudação no servidor de saudação. Se a versão passada com hello solicitação não corresponde a saudação back-end, biblioteca de saudação do cliente gera um `MobileServicePreconditionFailedException<T>` exceção. tipo de saudação incluído com a exceção de saudação é registro Olá Olá versão back-end que contém Olá servidores de registro de saudação. Olá aplicativo pode usar este toodecide informações se solicitação de atualização de saudação tooexecute novamente com hello correto `version` valor de alterações de toocommit de back-end de saudação.

Definir uma coluna na classe de tabela Olá para Olá `version` simultaneidade otimista de tooenable de propriedade de sistema. Por exemplo:

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

Aplicativos que usam tabelas sem tipo habilitar simultaneidade otimista por configuração Olá `Version` sinalizador no `SystemProperties` de saudação de tabela da seguinte maneira.

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

Em adição tooenabling a simultaneidade otimista, você deve também captura Olá `MobileServicePreconditionFailedException<T>` exceção em seu código ao chamar [UpdateAsync].  Resolva o conflito de saudação aplicando Olá correto `version` toothe atualizou o registro e chamada [UpdateAsync] com hello resolveu o registro. saudação de código a seguir mostra como tooresolve um conflito de gravação uma vez detectado:

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

Para obter mais informações, consulte Olá [sincronização de dados Offline em aplicativos móveis do Azure] tópico.

### <a name="binding"></a>Como: interface de usuário do Windows de tooa de dados de aplicativos móveis de ligação
Esta seção mostra como toodisplay retornados objetos de dados usando os elementos de interface do usuário em um aplicativo do Windows.  O exemplo de código a seguir associa toohello fonte da lista de saudação com uma consulta para itens incompletos. O [MobileServiceCollection] cria uma coleção de associações com reconhecimento de Aplicativos Móveis.

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

Alguns controles em Olá gerenciados suporte de tempo de execução chamada de uma interface [ISupportIncrementalLoading]. Essa interface permite que os controles toorequest dados extras ao usuário Olá rolar. Não há suporte interno para esta interface para aplicativos universais do Windows por meio de [MobileServiceIncrementalLoadingCollection], que controla automaticamente as chamadas de controles de saudação. Use `MobileServiceIncrementalLoadingCollection` em aplicativos do Windows, da seguinte maneira:

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

toouse Olá nova coleção de aplicativos do Windows Phone 8 e "Silverlight", use Olá `ToCollection` métodos de extensão em `IMobileServiceTableQuery<T>` e `IMobileServiceTable<T>`. dados de tooload, chame `LoadMoreItemsAsync()`.

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

Quando você usa a coleção de saudação criada chamando `ToCollectionAsync` ou `ToCollection`, você obtém uma coleção que pode ser associado tooUI controles.  Essa coleção tem reconhecimento de paginação.  Desde que a coleção de saudação está carregando os dados da rede, às vezes, há falha no carregamento. toohandle essas falhas, substituir Olá `OnException` método `MobileServiceIncrementalLoadingCollection` toohandle exceções resultantes de chamadas muito`LoadMoreItemsAsync`.

Considere se sua tabela possui muitos campos, mas deseja toodisplay apenas algumas no seu controle. Você poderá usar orientação Olá Olá anterior a seção "[selecionar colunas específicas](#selecting)" tooselect toodisplay de colunas específicas em Olá da interface do usuário.

### <a name="pagesize"></a>Saudação de alterar o tamanho de página
Os Aplicativos Móveis do Azure retornam, no máximo, 50 itens por solicitação por padrão.  Você pode alterar o tamanho de paginação Olá aumentando o tamanho máximo da página de saudação em Olá cliente e servidor.  tooincrease Olá tamanho da página solicitada, especificar `PullOptions` ao usar `PullAsync()`:

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

Supondo que você fez Olá `PageSize` tooor igual maior que 100 no servidor de saudação, uma solicitação retorna até 100 itens.

## <a name="#offlinesync"></a>Trabalhar com tabelas offline
Tabelas offline usam um local SQLite armazenar toostore dados para uso quando estiver offline.  Tabela de todas as operações são feitas em relação a saudação SQLite local armazenar em vez de armazenamento de servidor remoto hello.  toocreate uma tabela offline, primeiro prepare seu projeto:

1. No Visual Studio, clique com botão direito solução hello > **gerenciar pacotes NuGet para solução...** , em seguida, procurar e instalar o **Microsoft.Azure.Mobile.Client.SQLiteStore** pacote NuGet para todos os projetos na solução de saudação.
2. Dispositivos do Windows toosupport (opcional), instale um dos Olá SQLite pacotes de tempo de execução a seguir:

   * **Tempo de Execução do Windows 8.1**: instale o [SQLite para Windows 8.1][3].
   * **Windows Phone 8.1**: instale o [SQLite para Windows Phone 8.1][4].
   * **Plataforma universal do Windows** instalar [SQLite para Olá Universal do Windows][5].
3. (Opcional). Para dispositivos do Windows, clique em **referências** > **adicionar referência...** , expanda Olá **Windows** pasta > **extensões**, habilite Olá apropriado **SQLite para Windows** SDK junto com hello  **Visual C++ 2013 em tempo de execução para o Windows** SDK.
    Hello nomes SQLite SDK variam ligeiramente em cada plataforma do Windows.

Antes de uma referência de tabela pode ser criada, deve ser preparado repositório local hello:

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

Inicialização do repositório normalmente é feita imediatamente após o cliente Olá é criado.  Olá **OfflineDbPath** deve ser um nome de arquivo adequado para uso em todas as plataformas que você oferece suporte.  Se o caminho de saudação é um caminho totalmente qualificado (ou seja, ele começa com uma barra), em seguida, ele será usado.  Se o caminho de saudação não está totalmente qualificado, o arquivo de saudação é colocado em um local específico da plataforma.

* Para dispositivos iOS e Android, o caminho de padrão de saudação é hello "pessoal pasta"arquivos.
* Para dispositivos do Windows, o caminho de padrão de saudação é pasta de "AppData" hello específicas do aplicativo.

Uma referência de tabela pode ser obtida usando Olá `GetSyncTable<>` método:

```
var table = client.GetSyncTable<TodoItem>();
```

Não é necessário tooauthenticate toouse uma tabela offline.  Você só precisa tooauthenticate quando você está se comunicando com o serviço de back-end de saudação.

### <a name="syncoffline"></a>Sincronizando uma tabela Offline
Tabelas offline não são sincronizadas com hello back-end por padrão.  A sincronização é dividida em duas partes.  Você pode enviar alterações separadamente de download de novos itens.  Este é um método de sincronização típico:

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

Se Olá primeiro argumento muito`PullAsync` for nulo, a sincronização incremental não é usado.  Todas as operações de sincronização recuperam todos os registros.

Olá SDK executa implícita `PushAsync()` antes de extrair os registros.

Manipulação de conflito ocorre em um método `PullAsync()`.  Pode lidar com conflitos no hello mesma maneira que as tabelas online.  conflito de saudação é produzido quando `PullAsync()` é chamado em vez de durante a saudação insert, update ou delete. Se vários conflitos ocorrerem, eles serão agrupados em uma única MobileServicePushFailedException.  Gerenciar cada falha separadamente.

## <a name="#customapi"></a>Trabalhar com uma API personalizada
Uma API personalizada permite que você toodefine pontos de extremidade personalizados que expõem a funcionalidade do servidor que não mapeiam tooan inserir, atualizar, excluir ou operação de leitura. Usando uma API personalizada, você pode ter mais controle sobre mensagens, incluindo ler e definir cabeçalhos de mensagens HTTP e definir um formato de corpo de mensagem diferente do JSON.

Chamar uma API personalizada chamando uma saudação [InvokeApiAsync] métodos no cliente de saudação. Por exemplo, Olá linha de código a seguir envia um toohello de solicitação POST **completeAll** API em Olá back-end:

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

Este formulário é uma chamada de método com tipo e requer que Olá **MarkAllResult** retornar o tipo é definido. Os dois métodos, tipado e não tipado, são aceitos.

Olá InvokeApiAsync() método precede '/ api /' toohello API que você deseja toocall, a menos que Olá API começa com um '/'.
Por exemplo:

* `InvokeApiAsync("completeAll",...)`chama /api/completeAll Olá back-end
* `InvokeApiAsync("/.auth/me",...)`chama /.auth/me Olá back-end

Você pode usar InvokeApiAsync toocall qualquer WebAPI, incluindo os que não estão definidas WebAPIs com aplicativos móveis do Azure.  Quando você usa InvokeApiAsync(), os cabeçalhos apropriados de hello, incluindo os cabeçalhos de autenticação, são enviados com a solicitação de saudação.

## <a name="authentication"></a>Autenticar usuários
Os Aplicativos Móveis dão suporte à autenticação e à autorização de usuários de aplicativo, usando vários provedores de identidade externos: Facebook, Google, Conta da Microsoft, Twitter e o Azure Active Directory. Você pode definir permissões de acesso a tabelas toorestrict para operações específicas de tooonly autenticado usuários. Você também pode usar a identidade Olá usuários autenticados tooimplement de regras de autorização nos scripts de servidor. Para obter mais informações, consulte o tutorial Olá [adicionar autenticação tooyour aplicativo].

Dois fluxos de autenticação têm suporte: fluxo *gerenciado pelo cliente* e fluxo *gerenciado pelo servidor*. fluxo gerenciado pelo servidor de saudação fornece experiência de autenticação mais simples de Olá, como ele se baseia na interface de autenticação do provedor de saudação da web. fluxo de cliente gerenciado Olá permite integração mais profunda com recursos específicos do dispositivo como depende dos SDKs de específico do dispositivo específico do provedor.

> [!NOTE]
> Recomendamos o uso de um fluxo gerenciado pelo cliente em seus aplicativos de produção.

tooset a autenticação, você deve registrar seu aplicativo com um ou mais provedores de identidade.  provedor de identidade Hello gera uma ID de cliente e um segredo do cliente para seu aplicativo.  Esses valores, em seguida, são definidos no seu tooenable de back-end do serviço de aplicativo do Azure autenticação/autorização.  Para obter mais informações, execute as instruções detalhadas de saudação do tutorial [adicionar autenticação tooyour aplicativo].

Olá seguintes tópicos é abordado nesta seção:

* [Autenticação gerenciada pelo cliente](#clientflow)
* [Autenticação gerenciada pelo servidor](#serverflow)
* [Token de autenticação do cache Olá](#caching)

### <a name="clientflow"></a>Autenticação gerenciada pelo cliente
Seu aplicativo pode independentemente entre em contato com o provedor de identidade hello e forneça token retornado Olá durante o logon com seu back-end. Esse fluxo de cliente permite que você tooprovide uma experiência de logon único para usuários ou dados de usuário adicionais tooretrieve saudação do provedor de identidade. Autenticação de cliente de fluxo é preferencial toousing um fluxo de servidor como o provedor de identidade Olá SDK fornece uma aparência UX mais nativa e permite a personalização adicional.

Exemplos são fornecidos para Olá padrões de autenticação de cliente de fluxo a seguir:

* [Biblioteca de Autenticação do Active Directory](#adal)
* [Facebook ou Google](#client-facebook)
* [Live SDK](#client-livesdk)

#### <a name="adal"></a>Autenticar usuários com hello biblioteca de autenticação do Active Directory
Você pode usar a autenticação de usuário de tooinitiate de biblioteca de autenticação do Active Directory (ADAL) de saudação do cliente hello usando a autenticação do Active Directory do Azure.

1. Configurar seu back-end do aplicativo móvel para o logon do AAD pela seguinte Olá [como tooconfigure aplicativo de serviço de logon do Active Directory] tutorial. Torne-se toocomplete Olá opcional de registro de um aplicativo cliente nativo.
2. No Visual Studio ou no Xamarin Studio, abra seu projeto e adicione uma referência toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` pacote NuGet. Ao pesquisar, inclua versões de pré-lançamento.
3. Adicione Olá aplicativo tooyour de código a seguir, de acordo com a plataforma toohello que você está usando. Em cada um, verifique Olá substituições a seguir:

   * Substituir **aqui de autoridade de inserção** com o nome de saudação do locatário Olá no qual você provisionou o seu aplicativo. O formato deve ser https://login.microsoftonline.com/contoso.onmicrosoft.com. Esse valor pode ser copiado de guia de saudação do domínio no Active Directory do Azure no hello [portal clássico do Azure].
   * Substituir **inserir recursos-ID aqui** com a ID de cliente Olá para o back-end do aplicativo móvel. Você pode obter a ID do cliente Olá de Olá **avançado** guia **configurações do Active Directory do Azure** no portal de saudação.
   * Substituir **aqui INSERT-CLIENT-ID** com a ID de cliente Olá você copiou do aplicativo cliente nativo de saudação.
   * Substituir **INSERT-REDIRECT-URI-aqui** com seu site */.auth/login/done* ponto de extremidade, usando o esquema do hello HTTPS. Esse valor deve ser semelhante muito*https://contoso.azurewebsites.net/.auth/login/done*.

     código de saudação necessário para cada plataforma segue:

     **Windows:**

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

     **Xamarin.iOS**

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

     **Xamarin.Android**

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

#### <a name="client-facebook"></a>Entrada única usando um token do Facebook ou do Google
Você pode usar fluxo de saudação do cliente, conforme mostrado neste trecho para o Facebook ou Google.

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

#### <a name="client-livesdk"></a>O logon único usando Microsoft Account com hello Live SDK
tooauthenticate usuários, você deve registrar seu aplicativo no hello conta da Microsoft Developer Center. Configure os detalhes do registro no back-end do Aplicativo Móvel. toocreate Microsoft registro de conta e conecte-o back-end de aplicativo móvel tooyour, Olá concluir as etapas em [registrar seu aplicativo toouse um logon de conta Microsoft]. Se você tiver versões da Windows Store e Windows Phone do Silverlight/8 do seu aplicativo, registre a versão de armazenamento do Windows hello primeiro.

Olá código a seguir autentica usando o Live SDK e usa Olá retornada token toosign no back-end de aplicativo móvel tooyour.

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

Para obter mais informações, consulte Olá [Windows Live SDK] documentação.

### <a name="serverflow"></a>Autenticação gerenciada pelo servidor
Depois que você registrou o seu provedor de identidade, chamar hello [LoginAsync] método hello [MobileServiceClient] com hello [MobileServiceAuthenticationProvider] valor do provedor. Por exemplo, hello código a seguir inicia um servidor fluxo-entrar usando o Facebook.

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

Se você estiver usando um provedor de identidade diferente do Facebook, altere o valor de saudação do [MobileServiceAuthenticationProvider] toohello valor para o seu provedor.

Em um fluxo de servidor, do serviço de aplicativo do Azure gerencia o fluxo de autenticação OAuth Olá exibindo Olá página de entrada do provedor selecionado hello.  Uma vez retorna de provedor de identidade hello, serviço de aplicativo do Azure gera um token de autenticação do serviço de aplicativo. Olá [LoginAsync] método retorna um [MobileServiceUser], que fornece os dois Olá [UserId] de saudação autenticado o usuário e Olá [ MobileServiceAuthenticationToken], como um JSON web token (JWT). Esse token pode ser armazenado em cache e reutilizado até que expire. Para obter mais informações, consulte [token de autenticação do Caching Olá](#caching).

### <a name="caching"></a>Token de autenticação do cache Olá
Em alguns casos, o método de logon do hello chamada toohello pode ser evitado após uma autenticação bem-sucedida primeiro Olá armazenando o token de autenticação de saudação do provedor de saudação.  Os aplicativos da Windows Store e UWP podem usar [PasswordVault] toocache um token de autenticação atual após um bem-sucedida entrar, da seguinte maneira:

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

Olá UserId valor é armazenado como Olá nome de usuário da credencial hello e token Olá é hello armazenado como Olá senha. Em iniciante subsequentes, você pode verificar Olá **PasswordVault** para credenciais armazenadas em cache. Olá exemplo a seguir usa credenciais armazenadas em cache quando eles são encontrados e caso contrário, as tentativas tooauthenticate novamente com hello back-end:

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

Quando você sair de um usuário, você também deve remover credencial Olá armazenado, da seguinte maneira:

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

Saudação de usar aplicativos Xamarin [Xamarin.Auth] credenciais do repositório de APIs toosecurely em uma **conta** objeto. Para obter um exemplo de como usar essas APIs, consulte Olá [AuthStore.cs] arquivo de código no hello [ContosoMoments foto compartilhamento exemplo](https://github.com/azure-appservice-samples/ContosoMoments).

Quando você usar a autenticação de cliente gerenciado, você também pode armazenar o token de acesso de saudação obtido do provedor como o Facebook ou Twitter. Esse token pode ser fornecido toorequest um novo token de autenticação de back-end hello, da seguinte maneira:

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <a name="pushnotifications"></a>Notificações por Push
Olá tópicos a seguir cobrem as notificações por Push:

* [Registrar notificações por push](#register-for-push)
* [Obter um SID do pacote da Windows Store](#package-sid)
* [Registrar com modelos de Plataforma cruzada](#register-xplat)

### <a name="register-for-push"></a>Como se registrar para receber notificações por push
cliente de aplicativos móveis Olá permite tooregister para notificações de push com Hubs de notificação do Azure. Ao registrar, você obter um identificador obtidos específico da plataforma Olá serviço de notificação por Push (PNS). Você fornecer esse valor junto com todas as marcas, em seguida, quando você criar o registro de saudação. Olá código a seguir registra seu aplicativo do Windows para notificações por push com hello serviço de notificação do Windows (WNS):

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

Se você estiver enviando por push tooWNS, você deve [obter um SID do pacote da Windows Store](#package-sid).  Para obter mais informações sobre aplicativos do Windows, inclusive como tooregister para registros de modelo, consulte [adicionar push notificações tooyour aplicativo].

Não há suporte para solicitar marcas de cliente hello.  As solicitações de marca são descartadas silenciosamente do registro.
Se você quiser tooregister seu dispositivo com marcas, crie uma API personalizada que usa o registro de Olá Olá API de Hubs de notificação tooperform em seu nome.  [Chamar hello API personalizada](#customapi) em vez da saudação `RegisterNativeAsync()` método.

### <a name="package-sid"></a>Como obter um SID do pacote da Windows Store
Um SID de pacote é necessário para habilitar notificações por push em aplicativos da Windows Store.  tooreceive um pacote SID, registrar seu aplicativo com hello da Windows Store.

tooobtain este valor:

1. No Visual Studio Solution Explorer, projeto de aplicativo da Windows Store com o botão direito hello, clique em **repositório** > **associar aplicativo hello repositório...** .
2. No Assistente de saudação, clique em **próximo**, entrar com sua conta da Microsoft, digite um nome para seu aplicativo na **reservar um novo nome de aplicativo**, em seguida, clique em **reserva**.
3. Após o registro do aplicativo hello nome do aplicativo foi criado com êxito, selecione hello, clique em **próximo**e, em seguida, clique em **associar**.
4. Faça logon no toohello [Centro de desenvolvimento do Windows] usando sua Account da Microsoft. Em **meus aplicativos**, clique em um registro de aplicativo hello criado.
5. Clique em **gerenciamento de aplicativo** > **identidade de aplicativo**e, em seguida, role para baixo toofind seu **SID do pacote**.

Muitos usos do SID do pacote hello tratá-lo como um URI, caso em que você precisa toouse *ms-app: / /* como esquema de saudação. Anote a versão de saudação do seu pacote SID formado pela concatenação esse valor como um prefixo.

Aplicativos Xamarin exigem algumas tooregister capaz de toobe código adicional um aplicativo em execução em plataformas Android ou iOS hello. Para obter mais informações, consulte o tópico de saudação para sua plataforma:

* [Xamarin.Android](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [Xamarin.iOS](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <a name="register-xplat"></a>Como: notificações de plataforma cruzada do registro por push modelos toosend
modelos de tooregister, use Olá `RegisterAsync()` método com modelos de hello, da seguinte maneira:

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

Os modelos devem ser `JObject` tipos e pode conter vários modelos em Olá formato JSON a seguir:

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

Olá método **RegisterAsync()** também aceita blocos secundário:

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

Todas as marcações são retiradas durante o registro para segurança. tooadd marcas tooinstallations ou modelos dentro de instalações, consulte [trabalhar com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure].

notificações de toosend utilizando esses modelos registrados, consulte toohello [APIs de Hubs de notificação].

## <a name="misc"></a>Tópicos Diversos
### <a name="errors"></a>Como tratar erros
Quando ocorre um erro no back-end do hello, cliente Olá SDK gera um `MobileServiceInvalidOperationException`.  A exemplo a seguir mostra como uma exceção que é retornado pelo back-end de saudação do toohandle:

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

Outro exemplo de lidar com condições de erro pode ser encontrado no hello [exemplo de arquivos de aplicativos móveis]. O [LoggingHandler] exemplo fornece um delegado de registro em log solicitações de saudação do manipulador toolog sendo feitas toohello back-end.

### <a name="headers"></a>Como personalizar cabeçalhos de solicitação
toosupport seu cenário de aplicativo específico, talvez seja necessário toocustomize comunicação com o back-end de aplicativo móvel hello. Por exemplo, você pode desejar tooadd uma solicitação de saída de cabeçalho personalizado tooevery ou até mesmo alterar códigos de status de respostas. Você pode usar um personalizado [DelegatingHandler], conforme mostrado no exemplo a seguir de saudação:

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
