---
title: 'Tutorial do ASP.NET MVC para Azure Cosmos DB: desenvolvimento de aplicativo Web | Microsoft Docs'
description: "ASP.NET MVC tutorial toocreate um aplicativo web do MVC usando o banco de dados do Azure Cosmos. Você armazenará o JSON e acessará dados de um aplicativo de lista de tarefas pendentes hospedado em sites do Azure ‒ tutorial passo a passo do ASP NET MVC."
keywords: tutorial do asp.net mvc, desenvolvimento de aplicativos web, aplicativo web mvc, passo a passo do tutorial do asp net mvc
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395809351"></a>Tutorial do ASP.NET MVC: desenvolvimento de aplicativo Web com o Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

toohighlight como com eficiência, você pode aproveitar o banco de dados do Azure Cosmos toostore e consultar documentos JSON, este artigo fornece uma passo a passo a-ponta mostrando como toobuild um aplicativo todo usando o banco de dados do Azure Cosmos. tarefas de saudação serão armazenadas como documentos JSON no banco de dados do Azure Cosmos.

![Captura de tela da lista de tarefas Olá aplicativo da web MVC criado por este tutorial - tutorial de ASP NET MVC passo a passo](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

Este passo a passo mostra como toouse hello Azure Cosmos DB serviço toostore e acessar dados de um aplicativo ASP.NET MVC hospedado no Azure. Se você estiver procurando um tutorial que se concentra somente no banco de dados do Azure Cosmos e não hello componentes do ASP.NET MVC, consulte [criar um aplicativo de console do Azure Cosmos DB c#](documentdb-get-started.md).

> [!TIP]
> Este tutorial pressupõe que você tem experiência anterior com o ASP.NET MVC e com os Sites do Azure. Se você for novo tooASP.NET ou Olá [ferramentas pré-requisito](#_Toc395637760), recomendamos o download do projeto de exemplo completo de saudação do [GitHub] [ GitHub] e seguindo as instruções de saudação de Este exemplo. Depois de criado, você pode examinar informações de toogain este artigo no código Olá no contexto de saudação do projeto hello.
> 
> 

## <a name="_Toc395637760"></a>Pré-requisitos para este tutorial de banco de dados
Antes de seguir as instruções neste artigo hello, você deve garantir que você tenha a seguinte hello:

* Uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 

    OU

    Uma instalação local do hello [emulador de banco de dados do Azure Cosmos](local-emulator.md).
* [Visual Studio 2017](http://www.visualstudio.com/).  
* SDK do Microsoft Azure para .NET para Visual Studio de 2017, disponíveis por meio de saudação instalador do Visual Studio.

Todas as capturas de tela de saudação neste artigo tem sido feitas usando o Microsoft Visual Studio Community 2017. Se seu sistema estiver configurado com uma versão diferente, é possível que as opções e telas não correspondem totalmente, mas se você atender a saudação acima pré-requisitos Essa solução deve funcionar.

## <a name="_Toc395637761"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB
Vamos começar criando uma conta do Azure Cosmos DB. Se você já tem uma conta do SQL (documentos) para o banco de dados do Azure Cosmos ou se você estiver usando hello Azure Cosmos DB emulador para este tutorial, você poderá ignorar muito[criar um novo aplicativo ASP.NET MVC](#_Toc395637762).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
Agora vamos percorrer como toocreate um novo aplicativo ASP.NET MVC de saudação Terra-o. 

## <a name="_Toc395637762"></a>Etapa 2: criar um novo aplicativo ASP.NET MVC

1. No Visual Studio, no hello **arquivo** menus, aponte muito**novo**e, em seguida, clique em **projeto**. Olá **novo projeto** caixa de diálogo é exibida.

2. Em Olá **tipos de projeto** painel, expanda **modelos**, **Visual C#**, **Web**e, em seguida, selecione **aplicativo Web ASP.NET** .

      ![Captura de tela da caixa de diálogo Novo projeto Olá com tipo de projeto de aplicativo Web ASP.NET Olá realçado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. Em Olá **nome** caixa, digite o nome de saudação do projeto de saudação. Este tutorial usa nome hello "todo". Se você escolher toouse algo diferente de isso, em seguida, sempre que este tutorial aborda Olá todo namespace, você precisa toouse de exemplos de código tooadjust Olá fornecido tudo o que você nomeou seu aplicativo. 
4. Clique em **procurar** toonavigate toohello pasta onde você deseja como projeto de saudação toocreate e clique **Okey**.
   
      Olá **novo aplicativo Web ASP.NET** caixa de diálogo é exibida.
   
    ![Captura de tela da caixa de diálogo Novo aplicativo Web ASP.NET Olá com modelo de aplicativo MVC Olá realçado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. No painel de modelos hello, selecione **MVC**.

6. Clique em **Okey** e deixar o Visual Studio fazer seu trabalho em torno do modelo de ASP.NET MVC scaffolding Olá vazio. 

          
7. Depois que o Visual Studio terminar a criação do aplicativo do hello boilerplate MVC, você tem um aplicativo ASP.NET vazio que pode ser executado localmente.
   
    Será ignorada projeto de saudação em execução localmente como sei temos Olá todos vistas ASP.NET "Hello World" aplicativo. Vamos tooadding reta Azure Cosmos DB toothis projeto e compilar nosso aplicativo.

## <a name="_Toc395637767"></a>Etapa 3: Adicionar um projeto de aplicativo web do banco de dados do Azure Cosmos tooyour MVC
Agora que temos a maioria dos detalhes técnicos saudação do ASP.NET MVC que precisamos para esta solução, vamos toohello propósito deste tutorial, adicionando o aplicativo web do banco de dados do Azure Cosmos tooour MVC.

1. Olá SDK .NET do Azure Cosmos DB empacotado e distribuído como um pacote do NuGet. tooget Olá pacote do NuGet no Visual Studio, use o Gerenciador de pacotes do NuGet Olá no Visual Studio clicando no projeto Olá no **Solution Explorer** e, em seguida, clicando em **gerenciar pacotes NuGet**.
   
    ![Captura de tela de saudação com o botão direito em opções para o projeto de aplicativo web Olá no Gerenciador de soluções, com gerenciar pacotes NuGet realçado.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    Olá **gerenciar pacotes NuGet** caixa de diálogo é exibida.
2. Em Olá NuGet **procurar** , digite ***DocumentDB do Azure***. (nome do pacote de saudação não foi atualizado tooAzure Cosmos DB.)
   
    Resultados de hello, instalar Olá **Microsoft.Azure.DocumentDB pela Microsoft** pacote. Isso baixará e instalará o pacote de banco de dados do Azure Cosmos hello, bem como todas as dependências, como newtonsoft. JSON. Clique em **Okey** em Olá **visualização** janela, e **aceito** em Olá **a aceitação da licença** janela toocomplete Olá instalar.
   
    ![Captura de tela da janela Gerenciar pacotes NuGet Olá com hello biblioteca de cliente do Microsoft Azure DocumentDB realçado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      Como alternativa, você pode usar Olá pacote de saudação tooinstall Package Manager Console. toodo caso, em Olá **ferramentas** menu, clique em **NuGet Package Manager**e, em seguida, clique em **Package Manager Console**. No prompt de hello, digite o seguinte hello.
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. Depois de instalar o pacote de saudação, sua solução do Visual Studio deve se parecer com o seguinte Olá com duas novas referências adicionadas, Microsoft.Azure.Documents.Client e newtonsoft. JSON.
   
    ![Captura de tela de duas referências de saudação adicionado o projeto de dados JSON toohello no Gerenciador de soluções](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <a name="_Toc395637763"></a>Etapa 4: Configurar Olá aplicativo ASP.NET MVC
Agora vamos adicionar Olá modelos, exibições e controladores toothis MVC de aplicativos:

* [Adicionar um modelo](#_Toc395637764).
* [Adicionar um controlador](#_Toc395637765).
* [Adicionar exibições](#_Toc395637766).

### <a name="_Toc395637764"></a>Adicionar um modelo de dados JSON
Vamos começar criando Olá **M** no MVC, Olá modelo. 

1. Em **Gerenciador de soluções**, Olá atalho **modelos** pasta, clique em **adicionar**e, em seguida, clique em **classe**.
   
      Olá **Adicionar Novo Item** caixa de diálogo é exibida.
2. Nomeie a nova classe **Item.cs** e clique em **Adicionar**. 
3. Neste novo **Item.cs** de arquivo, adicione o seguinte de saudação após Olá última *usando a instrução*.
   
        using Newtonsoft.Json;
4. Agora substitua este código 
   
        public class Item
        {
        }
   
    com hello código a seguir.
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    Todos os dados no banco de dados do Azure Cosmos é passada pela transmissão hello e armazenados como JSON. forma de saudação toocontrol os objetos são serializados/desserializados por JSON.NET, você pode usar Olá **JsonProperty** atributo conforme demonstrado no hello **Item** classe que acabamos de criar. Você não **ter** toodo isso mas deseja tooensure Minhas propriedades sigam Olá JSON camelCase convenções de nomenclatura. 
   
    Não só você pode controlar formato Olá Olá do nome da propriedade quando entra em JSON, mas é totalmente possível renomear suas propriedades .NET como fiz com hello **descrição** propriedade. 

### <a name="_Toc395637765"></a>Adicionar um controlador
Que cuida da saudação **M**, agora vamos criar hello **C** no MVC, uma classe de controlador.

1. Em **Solution Explorer**, Olá do botão direito do mouse **controladores** pasta, clique em **adicionar**e, em seguida, clique em **controlador**.
   
    Olá **adicionar Scaffold** caixa de diálogo é exibida.
2. Selecione **Controlador MVC 5 - Vazio** e clique em **Adicionar**.
   
    ![Captura de tela da caixa de diálogo Adicionar Scaffold Olá com hello controlador MVC 5 - opção vazia realçado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. Nomeie o novo Controlador, **ItemController.**
   
    ![Captura de tela da caixa de diálogo Adicionar controlador Olá](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    Depois de criar o arquivo hello, sua solução do Visual Studio deve ser semelhante a seguinte Olá com novo ItemController.cs arquivo hello em **Gerenciador de soluções**. Olá Novo Item.cs arquivo criado anteriormente também é mostrado.
   
    ![Captura de tela de saudação solução do Visual Studio - Gerenciador de soluções com o novo arquivo. ItemController.cs hello e arquivo Item.cs realçado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    Você pode fechar ItemController.cs, voltaremos tooit mais tarde. 

### <a name="_Toc395637766"></a>Adicionar exibições
Agora, vamos criar hello **V** no MVC, Olá modos de exibição:

* [Adicionar uma exibição Índice de Itens](#AddItemIndexView).
* [Adicionar uma exibição Novo Item](#AddNewIndexView).
* [Adicionar uma exibição Editar Item](#_Toc395888515).

#### <a name="AddItemIndexView"></a>Adicionar uma exibição Índice de Itens
1. Em **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito Olá vazio **Item** pasta Visual Studio criado para você quando você adicionou Olá  **ItemController** anteriormente, clique em **adicionar**e, em seguida, clique em **exibição**.
   
    ![Captura de tela do Gerenciador de soluções mostrando a pasta de Item de saudação Visual Studio criado com comandos de exibição adicionar Olá realçados](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. Em Olá **adicionar exibição** caixa de diálogo caixa, Olá a seguir:
   
   * Em Olá **nome de exibição** , digite ***índice***.
   * Em Olá **modelo** selecione ***lista***.
   * Em Olá **classe modelo** selecione ***Item (todo. Modelos)***.
   * Na caixa de página de layout hello, digite ***~/Views/Shared/_Layout.cshtml***.
     
   ![Caixa de diálogo Adicionar modo de exibição do captura de tela mostrando Olá](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. Depois de definir todos esses valores, clique em **Adicionar** e deixe o Visual Studio criar uma nova exibição de modelo. Quando terminar, ele será aberto Olá cshtml um arquivo criado. Podemos pode fechar esse arquivo no Visual Studio como retornaremos tooit mais tarde.

#### <a name="AddNewIndexView"></a>Adicionar uma exibição Novo Item
Toohow semelhante, criamos um **índice do Item** exibição, agora, vamos criar uma nova exibição para criar um novo **itens**.

1. Em **Solution Explorer**, Olá do botão direito do mouse **Item** pasta novamente, clique em **adicionar**e, em seguida, clique em **exibição**.
2. Em Olá **adicionar exibição** caixa de diálogo caixa, Olá a seguir:
   
   * Em Olá **nome de exibição** , digite ***criar***.
   * Em Olá **modelo** selecione ***criar***.
   * Em Olá **classe modelo** selecione ***Item (todo. Modelos)***.
   * Na caixa de página de layout hello, digite ***~/Views/Shared/_Layout.cshtml***.
   * Clique em **Adicionar**.
   
#### <a name="_Toc395888515"></a>Adicionar uma exibição Editar Item
Finalmente, adicione um último modo de exibição para editar um **Item** em Olá mesma forma como antes.

1. Em **Solution Explorer**, Olá do botão direito do mouse **Item** pasta novamente, clique em **adicionar**e, em seguida, clique em **exibição**.
2. Em Olá **adicionar exibição** caixa de diálogo caixa, Olá a seguir:
   
   * Em Olá **nome de exibição** , digite ***editar***.
   * Em Olá **modelo** selecione ***editar***.
   * Em Olá **classe modelo** selecione ***Item (todo. Modelos)***.
   * Na caixa de página de layout hello, digite ***~/Views/Shared/_Layout.cshtml***.
   * Clique em **Adicionar**.

Depois que isso for feito, feche todos os documentos de cshtml de Olá no Visual Studio, como podemos retornarão exibições toothese mais tarde.

## <a name="_Toc395637769"></a>Etapa 5: Conectar o Azure Cosmos DB
Agora que é resolvido Olá MVC padronizado, vamos tooadding código de saudação para o banco de dados do Azure Cosmos. 

Nesta seção, vamos adicionar código seguinte de saudação do toohandle:

* [Listando itens incompletos](#_Toc395637770).
* [Adicionando itens](#_Toc395637771).
* [Editando itens](#_Toc395637772).

### <a name="_Toc395637770"></a>Listando itens incompletos no seu aplicativo Web MVC
Olá toodo coisa primeiro aqui é adicionar uma classe que contém todos os Olá lógica tooconnect tooand uso do Azure Cosmos DB. Para este tutorial, será encapsular toda essa lógica na classe de repositório tooa chamado DocumentDBRepository. 

1. Em **Solution Explorer**, com o botão direito no projeto hello, clique em **adicionar**e, em seguida, clique em **classe**. Nomeie a nova classe de saudação **DocumentDBRepository** e clique em **adicionar**.
2. Em Olá recém-criado **DocumentDBRepository** classe e adicione o seguinte Olá *usando instruções* acima Olá *namespace* declaração
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    Agora substitua este código 
   
        public class DocumentDBRepository
        {
        }
   
    com hello código a seguir.
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. Estamos está lendo alguns valores de configuração, isso abra Olá **Web. config** arquivo do seu aplicativo e adicione Olá linhas em Olá seguintes `<AppSettings>` seção.
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. Agora, atualize os valores hello para *ponto de extremidade* e *authKey* usando a folha de chaves de saudação do hello Portal do Azure. Use Olá **URI** da folha de chaves hello como valor de saudação de configuração de ponto de extremidade de saudação e use Olá **chave primária**, ou **chave SECUNDÁRIA** da folha de chaves hello como valor Olá Olá configuração de authKey.

    Que cuida da conectando com o repositório de banco de dados do Azure Cosmos hello, agora vamos adicionar nossa lógica do aplicativo.

1. Olá primeiro queremos toodo capaz de toobe com um aplicativo de lista de tarefas é itens do toodisplay Olá incompletos.  Copie e cole Olá seguindo o trecho de código em qualquer lugar na Olá **DocumentDBRepository** classe.
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. Olá abrir **ItemController** é adicionada anteriormente e adicione o seguinte Olá *usando instruções* acima da declaração de namespace hello.
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    Se seu projeto não é chamado de "todo", em seguida, você precisa tooupdate usando "todo. Modelos"; nome da saudação tooreflect de seu projeto.
   
    Agora substitua este código
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    com hello código a seguir.
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. Abra **Global.asax.cs** e adicione Olá toohello linha a seguir **Application_Start** método 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

Neste ponto, sua solução deve ser capaz de toobuild sem erros.

Se você tiver executado o aplicativo hello agora, você deve ir toohello **HomeController** e hello **índice** desse controlador de modo de exibição. Este é o comportamento padrão de saudação do projeto de modelo MVC Olá que escolhemos no início de saudação, mas não queremos que! Vamos alterar Olá roteamento neste tooalter de aplicativo MVC esse comportamento.

Abra ***aplicativo\_Start\RouteConfig.cs*** e localize a linha hello começando com "padrões:" e alterá-la Olá tooresemble a seguir.

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

Agora diz que se você não especificou um valor toocontrol de URL Olá Olá comportamento que, em vez de roteamento ASP.NET MVC **início**, use **Item** como controlador de saudação e usuário **índice** como modo de exibição de saudação.

Agora, se você executar o aplicativo hello, ele chamará o **ItemController** que será chamada na classe de repositório toohello e usar Olá GetItems método tooreturn todos os toohello de itens incompletos Olá **modos de exibição** \\ **Item**\\**índice** exibição. 

Se você compilar e executar esse projeto agora, deverá ver algo parecido com isto.    

![Captura de tela do aplicativo de web hello todo lista criado por este tutorial do banco de dados](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <a name="_Toc395637771"></a>Adicionando itens
Vamos colocar alguns itens no nosso banco de dados para que tenhamos algo mais que um toolook de grade vazia no.

Vamos adicionar alguns códigos muito Azure Cosmos DBRepository e ItemController toopersist Olá o registro no banco de dados do Azure Cosmos.

1. Adicionar Olá após o método tooyour **DocumentDBRepository** classe.
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   Este método simplesmente pega um objeto passado tooit e ele é mantida no banco de dados do Azure Cosmos.
2. Abrir o arquivo de ItemController.cs hello e adicione Olá seguindo o trecho de código na classe hello. Isso é como o ASP.NET MVC sabe quais toodo para Olá **criar** ação. Nesse caso renderização apenas Olá associados Create.cshtml exibição criada anteriormente.
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    Agora precisamos de algum código mais neste controlador que aceitará o envio de saudação de saudação **criar** exibição.
3. Adicione Olá próximo bloco de código toohello classe ItemController.cs que informa ao ASP.NET MVC que toodo um formulário POST para esse controlador.
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    Esse código chama em toohello DocumentDBRepository e usa Olá CreateItemAsync método toopersist Olá novo todo item toohello banco de dados. 
   
    **Observação de segurança**: Olá **ValidateAntiForgeryToken** atributo é usado aqui toohelp proteger esse aplicativo contra ataques de falsificação de solicitação entre sites. Não há mais tooit que apenas adicionar esse atributo, suas exibições necessário toowork com esse token antifalsificação também. Para obter mais informações sobre o assunto hello e exemplos de como tooimplement isso corretamente, consulte [impedindo a falsificação de solicitação intersite][Preventing Cross-Site Request Forgery]. Olá fornecido no código-fonte [GitHub] [ GitHub] tem implementação completa Olá em vigor.
   
    **Observação de segurança**: também usamos Olá **associar** atributo toohelp de parâmetro do método hello proteger contra ataques de lançamento excesso. Para obter mais detalhes, consulte [Basic CRUD Operations in ASP.NET MVC (Operações CRUD básicas no ASP.NET MVC)][Basic CRUD Operations in ASP.NET MVC].

Isso conclui Olá código necessário tooadd novos itens tooour banco de dados.

### <a name="_Toc395637772"></a>Editando itens
Há uma última coisa para que possamos toodo e que é tooadd Olá capacidade tooedit **itens** no banco de dados de saudação e toomark-los como concluída. Olá exibição para edição já foi adicionada toohello projeto, por isso, precisamos apenas tooadd alguns código controlador tooour e toohello **DocumentDBRepository** classe novamente.

1. Adicionar Olá após toohello **DocumentDBRepository** classe.
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    Olá primeiro desses métodos, **GetItem** busca um Item do Azure Cosmos DB que é passado back toohello **ItemController** e, em seguida, em toohello **editar** exibição.
   
    Olá segundo dos métodos de saudação que acabamos de adicionar substitui Olá **documento** no banco de dados do Azure Cosmos com versão de saudação do hello **documento** passado do hello **ItemController**.
2. Adicionar Olá após toohello **ItemController** classe.
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    Olá primeiro método trata Olá Http GET que acontece quando Olá usuário clica em Olá **editar** link da saudação **índice** exibição. Esse método busca um [ **documento** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) do banco de dados do Azure Cosmos e transmite toohello **editar** exibição.
   
    Olá **editar** exibição, em seguida, fará um Http POST toohello **IndexController**. 
   
    método segundo Hello, adicionamos identificadores passando Olá atualizado objeto tooAzure Cosmos DB toobe persistentes no banco de dados de saudação.

Isto é, que é tudo que precisamos toorun nosso aplicativo, lista incompleta **itens**, adicionar novos **itens**e editar **itens**.

## <a name="_Toc395637773"></a>Etapa 6: Executar aplicativo hello localmente
aplicativo de hello tootest em seu computador local, Olá a seguir:

1. Pressione F5 no aplicativo do Visual Studio toobuild hello no modo de depuração. Ele deve criar um aplicativo hello e iniciar um navegador com a página de grade vazia Olá que vimos antes:
   
    ![Captura de tela do aplicativo de web hello todo lista criado por este tutorial do banco de dados](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. Clique em Olá **criar novo** link e adicionar valores toohello **nome** e **descrição** campos. Deixe Olá **concluído** caixa de seleção desmarcada caso contrário Olá novo **Item** será adicionado em um estado concluído e não serão exibidos na lista de saudação inicial.
   
    ![Captura de tela de saudação Create view](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. Clique em **criar** e são redirecionada toohello back **índice** exibição e o **Item** aparece na lista de saudação.
   
    ![Captura de tela de saudação exibição índice](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    Sinta-se livre tooadd mais algumas **itens** tooyour lista de tarefas.
    
4. Clique em **editar** tooan próximo **Item** em lista hello e ficam toohello **editar** exibição onde você pode atualizar qualquer propriedade de seu objeto, incluindo Olá  **Concluída** sinalizador. Se você marcar Olá **concluir** sinalizador e clique em **salvar**, Olá **Item** é removido da lista de saudação de tarefas não concluídas.
   
    ![Captura de tela de saudação visualização de índice com hello concluído caixa marcada](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. Depois de testar o aplicativo hello, pressione Ctrl + F5 toostop depurar o aplicativo hello. Você está pronto toodeploy!

## <a name="_Toc395637774"></a>Etapa 7: Implantar Olá tooAzure de aplicativo do serviço de aplicativo 
Agora que você tem o aplicativo completo Olá funcionando corretamente com o banco de dados do Azure Cosmos, vamos toodeploy este tooAzure do aplicativo web do serviço de aplicativo.  

1. toopublish esse aplicativo, todos os toodo é com o botão direito no projeto Olá no **Solution Explorer** e clique em **publicar**.
   
    ![Captura de tela de saudação opção Publicar no Gerenciador de soluções](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. Em Olá **publicar** caixa de diálogo, clique em **serviço de aplicativo do Microsoft Azure**, em seguida, selecione **criar novo** toocreate um aplicativo de serviço de perfil ou clique em **selecionar Existente** toouse um perfil existente.

    ![Caixa de diálogo Publicar no Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. Se você tiver um perfil do Serviço de Aplicativo do Azure existente, digite o nome da assinatura. Saudação de uso **exibição** toosort por grupo de recursos ou o tipo de recurso de filtro, selecione o serviço de aplicativo do Azure. 
   
    ![Caixa de diálogo Serviço de Aplicativo no Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. toocreate um novo perfil de serviço de aplicativo do Azure, clique em **criar novo** em Olá **publicar** caixa de diálogo. Em Olá **criar serviço de aplicativo** caixa de diálogo, digite seu nome do aplicativo Web e a assinatura apropriada, o grupo de recursos e o plano de serviço de aplicativo, clique em **criar**.

    ![Caixa de diálogo Criar Serviço de Aplicativo no Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

Em poucos segundos, o Visual Studio terminará de publicar seu aplicativo Web e iniciará um navegador no qual você poderá ver seu trabalho sendo executado no Azure!



## <a name="_Toc395637775"></a>Próximas etapas
Parabéns! Você acabou de criado o ASP.NET MVC primeiro aplicativo web usando o banco de dados do Azure Cosmos e publicá-la tooAzure. Olá código-fonte para o aplicativo concluído hello, incluindo detalhes hello e excluir funcionalidade que não foram incluídos neste tutorial pode ser baixado ou clonado de [GitHub][GitHub]. Então se você estiver interessado em Adicionar aplicativo tooyour, pegue código hello e adicioná-lo toothis aplicativo.

aplicativo de tooyour tooadd funcionalidade adicional, Olá revisão APIs disponíveis no hello [biblioteca .NET do Azure Cosmos DB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) e se sentir livre toocontribute toohello Azure Cosmos DB-Library do .NET em [GitHub] [GitHub]. 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
