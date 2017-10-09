---
title: "aaaCreate um aplicativo .NET para a malha do serviço | Microsoft Docs"
description: "Saiba como toocreate um aplicativo com um front-end do ASP.NET Core e um confiável com monitoração de estado de back-end do serviço e implantar Olá aplicativo tooa cluster."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: bab331b9f8616c50a2794b6c048aace15579c8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a>Criar e implantar um aplicativo com um serviço de front-end de API Web do ASP.NET Core e um serviço de back-end com estado
Este tutorial é a primeira parte de uma série.  Você aprenderá como toocreate um aplicativo de malha do serviço do Azure com o início de uma API da Web do ASP.NET Core terminar e um serviço de back-end com monitoração de estado toostore seus dados. Quando você terminar, você tiver um aplicativo votação com um front-end para que salva os resultados de votação em um serviço de back-end com monitoração de estado no cluster de saudação de web do ASP.NET Core. Se você não quiser toomanually criar hello votação de aplicativo, você pode [baixar o código-fonte Olá](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) Olá concluída aplicativo e pular muito[percorrer Olá votação de aplicativo de exemplo](#walkthrough_anchor).

![Diagrama de aplicativo](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Na parte de saudação série, você aprenderá como:

> [!div class="checklist"]
> * Criar um serviço de API Web do ASP.NET Core como um Reliable Services com estado
> * Criar um serviço de Aplicativo Web do ASP.NET Core como um serviço Web sem estado
> * Use Olá proxy reverso toocommunicate com o serviço de monitoração de estado Olá

Nesta série de tutoriais, você aprenderá a:
> [!div class="checklist"]
> * Criar um aplicativo do Service Fabric .NET
> * [Implantar aplicativos de saudação tooa cluster remoto](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [Configurar CI/CD usando o Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial:
- Se você não tem uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Instalar o Visual Studio de 2017](https://www.visualstudio.com/) e instalar Olá **desenvolvimento do Azure** e **desenvolvimento ASP.NET e web** cargas de trabalho.
- [Instalar Olá SDK do Service Fabric](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a>Criar um serviço de API Web ASP.NET como um serviço confiável
Primeiro, crie Olá web front-end de saudação votação de aplicativo usando o ASP.NET Core. ASP.NET Core é uma estrutura de desenvolvimento de web leve e várias plataformas, você pode usar a interface da web modernos toocreate e APIs da web. tooget uma compreensão completa de como o ASP.NET Core se integra com o Service Fabric, é altamente recomendável ler Olá [ASP.NET Core em serviços confiável do serviço do Fabric](service-fabric-reliable-services-communication-aspnetcore.md) artigo. Por enquanto, você pode seguir este tutorial tooget iniciado rapidamente. toolearn mais sobre o ASP.NET Core, consulte Olá [documentação do ASP.NET Core](https://docs.microsoft.com/aspnet/core/).

> [!NOTE]
> Este tutorial baseia-se a saudação [ASP.NET Core ferramentas para Visual Studio de 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc). ferramentas do .NET Core Olá para Visual Studio 2015 não estão sendo atualizadas.

1. Inicie o Visual Studio como um **administrador**.

2. Crie um projeto com **Arquivo**->**Novo**->**Projeto**

3. Em Olá **novo projeto** caixa de diálogo, escolha **nuvem > aplicativo de malha do serviço**.

4. Nome do aplicativo hello **votação** e pressione **Okey**.

   ![Caixa de diálogo Novo projeto no Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. Em Olá **novo serviço do Service Fabric** escolha **sem monitoração de estado do ASP.NET Core**e o nome do seu serviço **VotingWeb**.
   
   ![Escolhendo um serviço web ASP.NET na caixa de diálogo Olá de novo serviço](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. próxima página de saudação fornece um conjunto de ASP.NET Core modelos de projeto. Para este tutorial, escolha **Aplicativo Web**. 
   
   ![Escolha o tipo de projeto do ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   O Visual Studio cria um aplicativo e um projeto de serviço e os exibe no Gerenciador de Soluções.

   ![Gerenciador de Soluções após a criação de aplicativo com serviço da API Web do ASP.NET Core]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a>Adicionar serviço do AngularJS toohello VotingWeb
Adicionar [AngularJS](http://angularjs.org/) tooyour service usando internas Olá [Bower suporte](/aspnet/core/client-side/bower). Abra *bower.json* e adicione entradas para angular e inicialização angular e depois salve suas alterações.

```json
{
  "name": "asp.net",
  "private": true,
  "dependencies": {
    "bootstrap": "3.3.7",
    "jquery": "2.2.0",
    "jquery-validation": "1.14.0",
    "jquery-validation-unobtrusive": "3.2.6",
    "angular": "v1.6.5",
    "angular-bootstrap": "v1.1.0"
  }
}
```
Após salvar Olá *bower. JSON* arquivo, Angular é instalado em seu projeto *wwwroot/lib* pasta. Além disso, ele é listado em Olá *dependências/Bower* pasta.

### <a name="update-hello-sitejs-file"></a>Atualizar o arquivo de site.js Olá
Olá abrir *wwwroot/js/site.js* arquivo.  Substitua o seu conteúdo com hello JavaScript usados por modos de exibição saudação inicial:

```javascript
var app = angular.module('VotingApp', ['ui.bootstrap']);
app.run(function () { });

app.controller('VotingAppController', ['$rootScope', '$scope', '$http', '$timeout', function ($rootScope, $scope, $http, $timeout) {

    $scope.refresh = function () {
        $http.get('api/Votes?c=' + new Date().getTime())
            .then(function (data, status) {
                $scope.votes = data;
            }, function (data, status) {
                $scope.votes = undefined;
            });
    };

    $scope.remove = function (item) {
        $http.delete('api/Votes/' + item)
            .then(function (data, status) {
                $scope.refresh();
            })
    };

    $scope.add = function (item) {
        var fd = new FormData();
        fd.append('item', item);
        $http.put('api/Votes/' + item, fd, {
            transformRequest: angular.identity,
            headers: { 'Content-Type': undefined }
        })
            .then(function (data, status) {
                $scope.refresh();
                $scope.item = undefined;
            })
    };
}]);
```

### <a name="update-hello-indexcshtml-file"></a>Atualizar Olá cshtml arquivo
Olá abrir *Views/Home/Index.cshtml* arquivo, controlador de Home toohello Olá exibição específico.  Substitua o seu conteúdo com os seguintes hello e salve suas alterações.

```html
@{
    ViewData["Title"] = "Service Fabric Voting Sample";
}

<div ng-controller="VotingAppController" ng-init="refresh()">
    <div class="container-fluid">
        <div class="row">
            <div class="col-xs-8 col-xs-offset-2 text-center">
                <h2>Service Fabric Voting Sample</h2>
            </div>
        </div>

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <form class="col-xs-12 center-block">
                    <div class="col-xs-6 form-group">
                        <input id="txtAdd" type="text" class="form-control" placeholder="Add voting option" ng-model="item" />
                    </div>
                    <button id="btnAdd" class="btn btn-default" ng-click="add(item)">
                        <span class="glyphicon glyphicon-plus" aria-hidden="true"></span>
                        Add
                    </button>
                </form>
            </div>
        </div>

        <hr />

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <div class="row">
                    <div class="col-xs-4">
                        Click toovote
                    </div>
                </div>
                <div class="row top-buffer" ng-repeat="vote in votes.data">
                    <div class="col-xs-8">
                        <button class="btn btn-success text-left btn-block" ng-click="add(vote.key)">
                            <span class="pull-left">
                                {{vote.key}}
                            </span>
                            <span class="badge pull-right">
                                {{vote.value}} Votes
                            </span>
                        </button>
                    </div>
                    <div class="col-xs-4">
                        <button class="btn btn-danger pull-right btn-block" ng-click="remove(vote.key)">
                            <span class="glyphicon glyphicon-remove" aria-hidden="true"></span>
                            Remove
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

### <a name="update-hello-layoutcshtml-file"></a>Atualizar o arquivo de layout. cshtml Olá
Olá abrir *Views/Shared/_Layout.cshtml* arquivo, o layout padrão de saudação do aplicativo do ASP.NET hello.  Substitua o seu conteúdo com os seguintes hello e salve suas alterações.

```html
<!DOCTYPE html>
<html ng-app="VotingApp" xmlns:ng="http://angularjs.org">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"]</title>

    <link href="~/lib/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/site.css" rel="stylesheet" />

</head>
<body>
    <div class="container body-content">
        @RenderBody()
    </div>

    <script src="~/lib/jquery/dist/jquery.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.js"></script>
    <script src="~/lib/angular/angular.js"></script>
    <script src="~/lib/angular-bootstrap/ui-bootstrap-tpls.js"></script>
    <script src="~/js/site.js"></script>

    @RenderSection("Scripts", required: false)
</body>
</html>
```

### <a name="update-hello-votingwebcs-file"></a>Atualizar o arquivo de VotingWeb.cs Olá
Olá abrir *VotingWeb.cs* arquivo, que cria Olá ASP.NET Core WebHost dentro Olá serviço sem monitoração de estado usando Olá WebListener web server.  Adicionar Olá `using System.Net.Http;` toohello diretiva superior do arquivo hello.  Substituir saudação `CreateServiceInstanceListeners()` funcionar com o seguinte hello e salve suas alterações.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
            {
                ServiceEventSource.Current.ServiceMessage(serviceContext, $"Starting WebListener on {url}");

                return new WebHostBuilder().UseWebListener()
                            .ConfigureServices(
                                services => services
                                    .AddSingleton<StatelessServiceContext>(serviceContext)
                                    .AddSingleton<HttpClient>())
                            .UseContentRoot(Directory.GetCurrentDirectory())
                            .UseStartup<Startup>()
                            .UseApplicationInsights()
                            .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                            .UseUrls(url)
                            .Build();
            }))
    };
}
```

### <a name="add-hello-votescontrollercs-file"></a>Adicionar arquivo de VotesController.cs Olá
Adicione um controlador que define as ações de votação. Clique duas vezes em hello **controladores** pasta, selecione **Adicionar -> novo item -> classe**.  Nome de arquivo hello "VotesController.cs" e clique em **adicionar**.  Substitua o conteúdo do arquivo hello pelo seguinte hello e salve suas alterações.  Posteriormente, [arquivo de atualização de VotesController.cs Olá](#updatevotecontroller_anchor), esse arquivo será modificado tooread e gravar dados de votação de serviço de back-end de saudação.  Por enquanto, controlador Olá retorna a exibição de toohello de dados de cadeia de caracteres estática.

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using Newtonsoft.Json;
using System.Text;
using System.Net.Http;
using System.Net.Http.Headers;

namespace VotingWeb.Controllers
{
    [Produces("application/json")]
    [Route("api/Votes")]
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            List<KeyValuePair<string, int>> votes= new List<KeyValuePair<string, int>>();
            votes.Add(new KeyValuePair<string, int>("Pizza", 3));
            votes.Add(new KeyValuePair<string, int>("Ice cream", 4));

            return Json(votes);
        }
     }
}
```



### <a name="deploy-and-run-hello-application-locally"></a>Implantar e executar o aplicativo hello localmente
Você pode prosseguir e executar o aplicativo hello. No Visual Studio, pressione `F5` toodeploy aplicativo de saudação para depuração. O `F5` falhará se você não abriu anteriormente o Visual Studio como **administrador**.

> [!NOTE]
> Olá a primeira vez que você executar e implanta o aplicativo hello localmente, o Visual Studio cria um cluster local para depuração.  A criação do cluster pode demorar um pouco. status de criação de cluster Olá é exibido na janela de saída do Visual Studio hello.

Neste ponto, seu aplicativo Web deve parecer com o seguinte:

![Front-end do ASP.NET Core](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

toostop depuração aplicativo hello, volte tooVisual Studio e pressione **Shift + F5**.

## <a name="add-a-stateful-back-end-service-tooyour-application"></a>Adicionar um aplicativo do serviço de back-end com monitoração de estado tooyour
Agora que temos um serviço de API da Web ASP.NET em execução em nosso aplicativo, vamos em frente e adicione alguns dados de um serviço confiável com monitoração de estado toostore em nosso aplicativo.

Serviço de malha permite tooconsistently e armazenar com segurança seus dados diretamente dentro de seu serviço usando coleções confiáveis. Coleções confiáveis são um conjunto de classes de coleção altamente disponível e confiável que são familiar tooanyone que usou c# coleções.

Neste tutorial, você cria um serviço que armazena um valor de contador em uma coleção confiável.

1. No Gerenciador de soluções, clique com botão direito **serviços** dentro Olá projeto de aplicativo e escolha **Adicionar > novo serviço do Service Fabric**.
   
    ![Adicionando um novo aplicativo de serviço tooan existente](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. Em Olá **novo serviço do Service Fabric** caixa de diálogo, escolha **com monitoração de estado ASP.NET Core**e o serviço de nomes de saudação **VotingData** e pressione **Okey**.

    ![Caixa de diálogo Novo serviço no Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    Depois de criar seu projeto de serviço, você terá dois serviços em seu aplicativo. Enquanto você continua toobuild seu aplicativo, você pode adicionar mais serviços em Olá mesma maneira. Cada um pode seu próprio controle de versão e ser atualizado de forma independente.

3. próxima página de saudação fornece um conjunto de ASP.NET Core modelos de projeto. Neste tutorial, escolhemos **API Web**.

    ![Escolha o tipo de projeto do ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    O Visual Studio cria um projeto de serviço e o exibe no Gerenciador de Soluções.

    ![Gerenciador de Soluções](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a>Adicionar arquivo de VoteDataController.cs Olá

Em Olá **VotingData** projeto com o botão direito em Olá **controladores** pasta, selecione **Adicionar -> novo item -> classe**. Nome de arquivo hello "VoteDataController.cs" e clique em **adicionar**. Substitua o conteúdo do arquivo hello pelo seguinte hello e salve suas alterações.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.ServiceFabric.Data;
using System.Threading;
using Microsoft.ServiceFabric.Data.Collections;

namespace VotingData.Controllers
{
    [Route("api/[controller]")]
    public class VoteDataController : Controller
    {
        private readonly IReliableStateManager stateManager;

        public VoteDataController(IReliableStateManager stateManager)
        {
            this.stateManager = stateManager;
        }

        // GET api/VoteData
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            var ct = new CancellationToken();

            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                var list = await votesDictionary.CreateEnumerableAsync(tx);

                var enumerator = list.GetAsyncEnumerator();

                var result = new List<KeyValuePair<string, int>>();

                while (await enumerator.MoveNextAsync(ct))
                {
                    result.Add(enumerator.Current);
                }

                return Json(result);
            }
        }

        // PUT api/VoteData/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                await votesDictionary.AddOrUpdateAsync(tx, name, 1, (key, oldvalue) => oldvalue + 1);
                await tx.CommitAsync();
            }

            return new OkResult();
        }

        // DELETE api/VoteData/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                if (await votesDictionary.ContainsKeyAsync(tx, name))
                {
                    await votesDictionary.TryRemoveAsync(tx, name);
                    await tx.CommitAsync();
                    return new OkResult();
                }
                else
                {
                    return new NotFoundResult();
                }
            }
        }
    }
}
```


## <a name="connect-hello-services"></a>Conectar os serviços de saudação
A próxima etapa, vamos conectar Olá dois serviços e fazer Olá Web front-end do aplicativo obter e definir informações do serviço de back-end de saudação de votação.

O Service Fabric fornece total flexibilidade na comunicação com Reliable Services. Em um único aplicativo, você pode ter serviços que sejam acessíveis por meio de TCP. Outros serviços que podem ser acessados por meio de uma API REST de HTTP e ainda outros serviços podem estar acessíveis por meio de soquetes da Web. Para obter informações sobre opções de saudação disponíveis e compensações de saudação envolvidas, consulte [se comunicar com serviços](service-fabric-connect-and-communicate-with-services.md).

Neste tutorial, usamos a [API Web ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a>Atualizar o arquivo de VotesController.cs Olá
Em Olá **VotingWeb** projeto, abra Olá *Controllers/VotesController.cs* arquivo.  Substituir saudação `VotesController` classe conteúdo de definição com a seguinte hello e salve suas alterações.

```csharp
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;
        string serviceProxyUrl = "http://localhost:19081/Voting/VotingData/api/VoteData";
        string partitionKind = "Int64Range";
        string partitionKey = "0";

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            IEnumerable<KeyValuePair<string, int>> votes;

            HttpResponseMessage response = await this.httpClient.GetAsync($"{serviceProxyUrl}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            votes = JsonConvert.DeserializeObject<List<KeyValuePair<string, int>>>(await response.Content.ReadAsStringAsync());

            return Json(votes);
        }

        // PUT: api/Votes/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            string payload = $"{{ 'name' : '{name}' }}";
            StringContent putContent = new StringContent(payload, Encoding.UTF8, "application/json");
            putContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");

            string proxyUrl = $"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}";

            HttpResponseMessage response = await this.httpClient.PutAsync(proxyUrl, putContent);

            return new ContentResult()
            {
                StatusCode = (int)response.StatusCode,
                Content = await response.Content.ReadAsStringAsync()
            };
        }

        // DELETE: api/Votes/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            HttpResponseMessage response = await this.httpClient.DeleteAsync($"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            return new OkResult();

        }
    }
```
<a id="walkthrough" name="walkthrough_anchor"></a>

## <a name="walk-through-hello-voting-sample-application"></a>Percorrer Olá votação de aplicativo de exemplo
Olá votação aplicativo consiste em dois serviços:
- (VotingWeb) de serviço front-end da Web – ASP.NET Core um serviço front-end, que serve a página da web de saudação e expõe web toocommunicate APIs com serviço de back-end de saudação.
- Serviço de back-end (VotingData)-um núcleo de ASP.NET web service, que expõe um voto de saudação do API toostore resulta em um dicionário confiável persistidos no disco.

![Diagrama de aplicativo](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Quando você vota em Olá Olá do aplicativo a seguir podem ocorrer eventos:
1. Um JavaScript envia Olá voto solicitação toohello API da web no serviço de front-end de web hello como uma solicitação HTTP PUT.

2. serviço de front-end de web Hello usa um proxy toolocate e encaminhar a um serviço de back-end de toohello de solicitação HTTP PUT.

3. serviço de back-end Olá leva a solicitação de entrada hello e repositórios Olá atualizado resultam em um dicionário confiável, que obtém toomultiple replicado nós no cluster hello e mantidos em disco. Dados do aplicativo hello todos os são armazenados no cluster hello, portanto, nenhum banco de dados é necessária.

## <a name="debug-in-visual-studio"></a>Depuração no Visual Studio
Ao depurar o aplicativo no Visual Studio, você usa um cluster de desenvolvimento local do Service Fabric. Você tem Olá opção tooadjust seu cenário de tooyour experiência de depuração. Neste aplicativo, armazenamos dados em nosso serviço de back-end, usando um dicionário confiável. Visual Studio remove o aplicativo hello por padrão quando você interrompe o depurador hello. Remover o aplicativo hello faz com que dados Olá Olá back-end tooalso serviço ser removido. dados de saudação toopersist entre as sessões de depuração, você pode alterar Olá **o modo de depuração de aplicativo** como uma propriedade no hello **votação** projeto no Visual Studio.

toolook o que acontece no código hello, Olá concluir as etapas a seguir:
1. Olá abrir **VotesController.cs** arquivo e defina um ponto de interrupção da API da web hello **colocar** método (linha 47 -), você pode procurar arquivo Olá Olá Gerenciador de soluções do Visual Studio.

2. Olá abrir **VoteDataController.cs** arquivo e defina um ponto de interrupção na API de web **colocar** método (linha 50).

3. Voltar toohello navegador e clique em uma opção de votação ou adicionar uma nova opção de votação. Você atingiu o primeiro ponto de interrupção de saudação no controlador de api do Olá web front-end.
    
    1. Isso é onde Olá JavaScript no navegador Olá envia um controlador de API da web solicitação toohello no serviço de front-end de saudação.
    
    ![Adicionar Serviço de Front-end de Voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. Primeiro, construímos Olá URL toohello ReverseProxy para nosso serviço de back-end **(1)**.
    3. Em seguida, podemos enviar Olá HTTP PUT solicitação toohello ReverseProxy **(2)**.
    4. Finalmente hello retornamos resposta de saudação do cliente do hello serviço back-end toohello **(3)**.

4. Pressione **F5** toocontinue
    1. Agora você está no ponto de interrupção Olá no serviço de back-end de saudação.
    
    ![Adicionar Serviço de Back-End de Voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. Na primeira linha hello no método hello **(1)** estamos usando Olá `StateManager` tooget ou adicionar um dicionário confiável chamado `counts`.
    3. Todas as interações com valores em um dicionário confiável exigem uma transação e, portanto, o uso da instrução **(2)** cria essa transação.
    4. Transação Olá, é, em seguida, atualizar o valor de saudação de chave relevantes Olá Olá votar na opção e confirmações Olá operação **(3)**. Depois de confirmar Olá método retorna, Olá dados são atualizados no dicionário hello e replicados tooother nós no cluster de saudação. dados de saudação agora são armazenados com segurança no cluster hello e serviço de back-end de saudação pode falhar em nós de tooother, ainda com dados de saudação disponíveis.
5. Pressione **F5** toocontinue

Olá toostop depuração sessão, pressione **Shift + F5**.


## <a name="next-steps"></a>Próximas etapas
Nesta parte do tutorial do hello, você aprendeu como:

> [!div class="checklist"]
> * Criar um serviço de API Web do ASP.NET Core como um Reliable Services com estado
> * Criar um serviço de Aplicativo Web do ASP.NET Core como um serviço Web sem estado
> * Use Olá proxy reverso toocommunicate com o serviço de monitoração de estado Olá

Tutorial de Avançar de toohello avançado:
> [!div class="nextstepaction"]
> [Implantar Olá aplicativo tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md)
