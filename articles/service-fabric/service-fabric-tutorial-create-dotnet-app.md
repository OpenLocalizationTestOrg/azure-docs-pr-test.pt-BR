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
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="aea52-103">Criar e implantar um aplicativo com um serviço de front-end de API Web do ASP.NET Core e um serviço de back-end com estado</span><span class="sxs-lookup"><span data-stu-id="aea52-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="aea52-104">Este tutorial é a primeira parte de uma série.</span><span class="sxs-lookup"><span data-stu-id="aea52-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="aea52-105">Você aprenderá como toocreate um aplicativo de malha do serviço do Azure com o início de uma API da Web do ASP.NET Core terminar e um serviço de back-end com monitoração de estado toostore seus dados.</span><span class="sxs-lookup"><span data-stu-id="aea52-105">You will learn how toocreate an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service toostore your data.</span></span> <span data-ttu-id="aea52-106">Quando você terminar, você tiver um aplicativo votação com um front-end para que salva os resultados de votação em um serviço de back-end com monitoração de estado no cluster de saudação de web do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="aea52-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span> <span data-ttu-id="aea52-107">Se você não quiser toomanually criar hello votação de aplicativo, você pode [baixar o código-fonte Olá](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) Olá concluída aplicativo e pular muito[percorrer Olá votação de aplicativo de exemplo](#walkthrough_anchor).</span><span class="sxs-lookup"><span data-stu-id="aea52-107">If you don't want toomanually create hello voting application, you can [download hello source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for hello completed application and skip ahead too[Walk through hello voting sample application](#walkthrough_anchor).</span></span>

![Diagrama de aplicativo](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="aea52-109">Na parte de saudação série, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="aea52-109">In part one of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aea52-110">Criar um serviço de API Web do ASP.NET Core como um Reliable Services com estado</span><span class="sxs-lookup"><span data-stu-id="aea52-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="aea52-111">Criar um serviço de Aplicativo Web do ASP.NET Core como um serviço Web sem estado</span><span class="sxs-lookup"><span data-stu-id="aea52-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="aea52-112">Use Olá proxy reverso toocommunicate com o serviço de monitoração de estado Olá</span><span class="sxs-lookup"><span data-stu-id="aea52-112">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="aea52-113">Nesta série de tutoriais, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="aea52-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="aea52-114">Criar um aplicativo do Service Fabric .NET</span><span class="sxs-lookup"><span data-stu-id="aea52-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="aea52-115">Implantar aplicativos de saudação tooa cluster remoto</span><span class="sxs-lookup"><span data-stu-id="aea52-115">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="aea52-116">Configurar CI/CD usando o Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="aea52-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="aea52-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aea52-117">Prerequisites</span></span>
<span data-ttu-id="aea52-118">Antes de começar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="aea52-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="aea52-119">Se você não tem uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="aea52-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="aea52-120">[Instalar o Visual Studio de 2017](https://www.visualstudio.com/) e instalar Olá **desenvolvimento do Azure** e **desenvolvimento ASP.NET e web** cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="aea52-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="aea52-121">Instalar Olá SDK do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="aea52-121">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="aea52-122">Criar um serviço de API Web ASP.NET como um serviço confiável</span><span class="sxs-lookup"><span data-stu-id="aea52-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="aea52-123">Primeiro, crie Olá web front-end de saudação votação de aplicativo usando o ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="aea52-123">First, create hello web front-end of hello voting application using ASP.NET Core.</span></span> <span data-ttu-id="aea52-124">ASP.NET Core é uma estrutura de desenvolvimento de web leve e várias plataformas, você pode usar a interface da web modernos toocreate e APIs da web.</span><span class="sxs-lookup"><span data-stu-id="aea52-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> <span data-ttu-id="aea52-125">tooget uma compreensão completa de como o ASP.NET Core se integra com o Service Fabric, é altamente recomendável ler Olá [ASP.NET Core em serviços confiável do serviço do Fabric](service-fabric-reliable-services-communication-aspnetcore.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="aea52-125">tooget a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through hello [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="aea52-126">Por enquanto, você pode seguir este tutorial tooget iniciado rapidamente.</span><span class="sxs-lookup"><span data-stu-id="aea52-126">For now, you can follow this tutorial tooget started quickly.</span></span> <span data-ttu-id="aea52-127">toolearn mais sobre o ASP.NET Core, consulte Olá [documentação do ASP.NET Core](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="aea52-127">toolearn more about ASP.NET Core, see hello [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="aea52-128">Este tutorial baseia-se a saudação [ASP.NET Core ferramentas para Visual Studio de 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="aea52-128">This tutorial is based on hello [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="aea52-129">ferramentas do .NET Core Olá para Visual Studio 2015 não estão sendo atualizadas.</span><span class="sxs-lookup"><span data-stu-id="aea52-129">hello .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="aea52-130">Inicie o Visual Studio como um **administrador**.</span><span class="sxs-lookup"><span data-stu-id="aea52-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="aea52-131">Crie um projeto com **Arquivo**->**Novo**->**Projeto**</span><span class="sxs-lookup"><span data-stu-id="aea52-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="aea52-132">Em Olá **novo projeto** caixa de diálogo, escolha **nuvem > aplicativo de malha do serviço**.</span><span class="sxs-lookup"><span data-stu-id="aea52-132">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="aea52-133">Nome do aplicativo hello **votação** e pressione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="aea52-133">Name hello application **Voting** and press **OK**.</span></span>

   ![Caixa de diálogo Novo projeto no Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="aea52-135">Em Olá **novo serviço do Service Fabric** escolha **sem monitoração de estado do ASP.NET Core**e o nome do seu serviço **VotingWeb**.</span><span class="sxs-lookup"><span data-stu-id="aea52-135">On hello **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![Escolhendo um serviço web ASP.NET na caixa de diálogo Olá de novo serviço](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="aea52-137">próxima página de saudação fornece um conjunto de ASP.NET Core modelos de projeto.</span><span class="sxs-lookup"><span data-stu-id="aea52-137">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="aea52-138">Para este tutorial, escolha **Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="aea52-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![Escolha o tipo de projeto do ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="aea52-140">O Visual Studio cria um aplicativo e um projeto de serviço e os exibe no Gerenciador de Soluções.</span><span class="sxs-lookup"><span data-stu-id="aea52-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![Gerenciador de Soluções após a criação de aplicativo com serviço da API Web do ASP.NET Core]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a><span data-ttu-id="aea52-142">Adicionar serviço do AngularJS toohello VotingWeb</span><span class="sxs-lookup"><span data-stu-id="aea52-142">Add AngularJS toohello VotingWeb service</span></span>
<span data-ttu-id="aea52-143">Adicionar [AngularJS](http://angularjs.org/) tooyour service usando internas Olá [Bower suporte](/aspnet/core/client-side/bower).</span><span class="sxs-lookup"><span data-stu-id="aea52-143">Add [AngularJS](http://angularjs.org/) tooyour service using hello built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="aea52-144">Abra *bower.json* e adicione entradas para angular e inicialização angular e depois salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="aea52-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

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
<span data-ttu-id="aea52-145">Após salvar Olá *bower. JSON* arquivo, Angular é instalado em seu projeto *wwwroot/lib* pasta.</span><span class="sxs-lookup"><span data-stu-id="aea52-145">Upon saving hello *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="aea52-146">Além disso, ele é listado em Olá *dependências/Bower* pasta.</span><span class="sxs-lookup"><span data-stu-id="aea52-146">Additionally, it is listed within hello *Dependencies/Bower* folder.</span></span>

### <a name="update-hello-sitejs-file"></a><span data-ttu-id="aea52-147">Atualizar o arquivo de site.js Olá</span><span class="sxs-lookup"><span data-stu-id="aea52-147">Update hello site.js file</span></span>
<span data-ttu-id="aea52-148">Olá abrir *wwwroot/js/site.js* arquivo.</span><span class="sxs-lookup"><span data-stu-id="aea52-148">Open hello *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="aea52-149">Substitua o seu conteúdo com hello JavaScript usados por modos de exibição saudação inicial:</span><span class="sxs-lookup"><span data-stu-id="aea52-149">Replace its contents with hello JavaScript used by hello Home views:</span></span>

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

### <a name="update-hello-indexcshtml-file"></a><span data-ttu-id="aea52-150">Atualizar Olá cshtml arquivo</span><span class="sxs-lookup"><span data-stu-id="aea52-150">Update hello Index.cshtml file</span></span>
<span data-ttu-id="aea52-151">Olá abrir *Views/Home/Index.cshtml* arquivo, controlador de Home toohello Olá exibição específico.</span><span class="sxs-lookup"><span data-stu-id="aea52-151">Open hello *Views/Home/Index.cshtml* file, hello view specific toohello Home controller.</span></span>  <span data-ttu-id="aea52-152">Substitua o seu conteúdo com os seguintes hello e salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="aea52-152">Replace its contents with hello following, then save your changes.</span></span>

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

### <a name="update-hello-layoutcshtml-file"></a><span data-ttu-id="aea52-153">Atualizar o arquivo de layout. cshtml Olá</span><span class="sxs-lookup"><span data-stu-id="aea52-153">Update hello _Layout.cshtml file</span></span>
<span data-ttu-id="aea52-154">Olá abrir *Views/Shared/_Layout.cshtml* arquivo, o layout padrão de saudação do aplicativo do ASP.NET hello.</span><span class="sxs-lookup"><span data-stu-id="aea52-154">Open hello *Views/Shared/_Layout.cshtml* file, hello default layout for hello ASP.NET app.</span></span>  <span data-ttu-id="aea52-155">Substitua o seu conteúdo com os seguintes hello e salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="aea52-155">Replace its contents with hello following, then save your changes.</span></span>

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

### <a name="update-hello-votingwebcs-file"></a><span data-ttu-id="aea52-156">Atualizar o arquivo de VotingWeb.cs Olá</span><span class="sxs-lookup"><span data-stu-id="aea52-156">Update hello VotingWeb.cs file</span></span>
<span data-ttu-id="aea52-157">Olá abrir *VotingWeb.cs* arquivo, que cria Olá ASP.NET Core WebHost dentro Olá serviço sem monitoração de estado usando Olá WebListener web server.</span><span class="sxs-lookup"><span data-stu-id="aea52-157">Open hello *VotingWeb.cs* file, which creates hello ASP.NET Core WebHost inside hello stateless service using hello WebListener web server.</span></span>  <span data-ttu-id="aea52-158">Adicionar Olá `using System.Net.Http;` toohello diretiva superior do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="aea52-158">Add hello `using System.Net.Http;` directive toohello top of hello file.</span></span>  <span data-ttu-id="aea52-159">Substituir saudação `CreateServiceInstanceListeners()` funcionar com o seguinte hello e salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="aea52-159">Replace hello `CreateServiceInstanceListeners()` function with hello following, then save your changes.</span></span>

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

### <a name="add-hello-votescontrollercs-file"></a><span data-ttu-id="aea52-160">Adicionar arquivo de VotesController.cs Olá</span><span class="sxs-lookup"><span data-stu-id="aea52-160">Add hello VotesController.cs file</span></span>
<span data-ttu-id="aea52-161">Adicione um controlador que define as ações de votação.</span><span class="sxs-lookup"><span data-stu-id="aea52-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="aea52-162">Clique duas vezes em hello **controladores** pasta, selecione **Adicionar -> novo item -> classe**.</span><span class="sxs-lookup"><span data-stu-id="aea52-162">Right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="aea52-163">Nome de arquivo hello "VotesController.cs" e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="aea52-163">Name hello file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="aea52-164">Substitua o conteúdo do arquivo hello pelo seguinte hello e salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="aea52-164">Replace hello file contents with hello following, then save your changes.</span></span>  <span data-ttu-id="aea52-165">Posteriormente, [arquivo de atualização de VotesController.cs Olá](#updatevotecontroller_anchor), esse arquivo será modificado tooread e gravar dados de votação de serviço de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="aea52-165">Later, in [Update hello VotesController.cs file](#updatevotecontroller_anchor), this file will be modified tooread and write voting data from hello back-end service.</span></span>  <span data-ttu-id="aea52-166">Por enquanto, controlador Olá retorna a exibição de toohello de dados de cadeia de caracteres estática.</span><span class="sxs-lookup"><span data-stu-id="aea52-166">For now, hello controller returns static string data toohello view.</span></span>

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



### <a name="deploy-and-run-hello-application-locally"></a><span data-ttu-id="aea52-167">Implantar e executar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="aea52-167">Deploy and run hello application locally</span></span>
<span data-ttu-id="aea52-168">Você pode prosseguir e executar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="aea52-168">You can now go ahead and run hello application.</span></span> <span data-ttu-id="aea52-169">No Visual Studio, pressione `F5` toodeploy aplicativo de saudação para depuração.</span><span class="sxs-lookup"><span data-stu-id="aea52-169">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span> <span data-ttu-id="aea52-170">O `F5` falhará se você não abriu anteriormente o Visual Studio como **administrador**.</span><span class="sxs-lookup"><span data-stu-id="aea52-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="aea52-171">Olá a primeira vez que você executar e implanta o aplicativo hello localmente, o Visual Studio cria um cluster local para depuração.</span><span class="sxs-lookup"><span data-stu-id="aea52-171">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="aea52-172">A criação do cluster pode demorar um pouco.</span><span class="sxs-lookup"><span data-stu-id="aea52-172">Cluster creation may take some time.</span></span> <span data-ttu-id="aea52-173">status de criação de cluster Olá é exibido na janela de saída do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="aea52-173">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="aea52-174">Neste ponto, seu aplicativo Web deve parecer com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="aea52-174">At this point, your web app should look like this:</span></span>

![Front-end do ASP.NET Core](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="aea52-176">toostop depuração aplicativo hello, volte tooVisual Studio e pressione **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="aea52-176">toostop debugging hello application, go back tooVisual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-tooyour-application"></a><span data-ttu-id="aea52-177">Adicionar um aplicativo do serviço de back-end com monitoração de estado tooyour</span><span class="sxs-lookup"><span data-stu-id="aea52-177">Add a stateful back-end service tooyour application</span></span>
<span data-ttu-id="aea52-178">Agora que temos um serviço de API da Web ASP.NET em execução em nosso aplicativo, vamos em frente e adicione alguns dados de um serviço confiável com monitoração de estado toostore em nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aea52-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service toostore some data in our application.</span></span>

<span data-ttu-id="aea52-179">Serviço de malha permite tooconsistently e armazenar com segurança seus dados diretamente dentro de seu serviço usando coleções confiáveis.</span><span class="sxs-lookup"><span data-stu-id="aea52-179">Service Fabric allows you tooconsistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="aea52-180">Coleções confiáveis são um conjunto de classes de coleção altamente disponível e confiável que são familiar tooanyone que usou c# coleções.</span><span class="sxs-lookup"><span data-stu-id="aea52-180">Reliable collections are a set of highly available and reliable collection classes that are familiar tooanyone who has used C# collections.</span></span>

<span data-ttu-id="aea52-181">Neste tutorial, você cria um serviço que armazena um valor de contador em uma coleção confiável.</span><span class="sxs-lookup"><span data-stu-id="aea52-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="aea52-182">No Gerenciador de soluções, clique com botão direito **serviços** dentro Olá projeto de aplicativo e escolha **Adicionar > novo serviço do Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="aea52-182">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Adicionando um novo aplicativo de serviço tooan existente](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="aea52-184">Em Olá **novo serviço do Service Fabric** caixa de diálogo, escolha **com monitoração de estado ASP.NET Core**e o serviço de nomes de saudação **VotingData** e pressione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="aea52-184">In hello **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name hello service **VotingData** and press **OK**.</span></span>

    ![Caixa de diálogo Novo serviço no Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="aea52-186">Depois de criar seu projeto de serviço, você terá dois serviços em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aea52-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="aea52-187">Enquanto você continua toobuild seu aplicativo, você pode adicionar mais serviços em Olá mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="aea52-187">As you continue toobuild your application, you can add more services in hello same way.</span></span> <span data-ttu-id="aea52-188">Cada um pode seu próprio controle de versão e ser atualizado de forma independente.</span><span class="sxs-lookup"><span data-stu-id="aea52-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="aea52-189">próxima página de saudação fornece um conjunto de ASP.NET Core modelos de projeto.</span><span class="sxs-lookup"><span data-stu-id="aea52-189">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="aea52-190">Neste tutorial, escolhemos **API Web**.</span><span class="sxs-lookup"><span data-stu-id="aea52-190">For this tutorial, choose **Web API**.</span></span>

    ![Escolha o tipo de projeto do ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="aea52-192">O Visual Studio cria um projeto de serviço e o exibe no Gerenciador de Soluções.</span><span class="sxs-lookup"><span data-stu-id="aea52-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Gerenciador de Soluções](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a><span data-ttu-id="aea52-194">Adicionar arquivo de VoteDataController.cs Olá</span><span class="sxs-lookup"><span data-stu-id="aea52-194">Add hello VoteDataController.cs file</span></span>

<span data-ttu-id="aea52-195">Em Olá **VotingData** projeto com o botão direito em Olá **controladores** pasta, selecione **Adicionar -> novo item -> classe**.</span><span class="sxs-lookup"><span data-stu-id="aea52-195">In hello **VotingData** project right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="aea52-196">Nome de arquivo hello "VoteDataController.cs" e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="aea52-196">Name hello file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="aea52-197">Substitua o conteúdo do arquivo hello pelo seguinte hello e salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="aea52-197">Replace hello file contents with hello following, then save your changes.</span></span>

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


## <a name="connect-hello-services"></a><span data-ttu-id="aea52-198">Conectar os serviços de saudação</span><span class="sxs-lookup"><span data-stu-id="aea52-198">Connect hello services</span></span>
<span data-ttu-id="aea52-199">A próxima etapa, vamos conectar Olá dois serviços e fazer Olá Web front-end do aplicativo obter e definir informações do serviço de back-end de saudação de votação.</span><span class="sxs-lookup"><span data-stu-id="aea52-199">In this next step, we will connect hello two services and make hello front-end Web application get and set voting information from hello back-end service.</span></span>

<span data-ttu-id="aea52-200">O Service Fabric fornece total flexibilidade na comunicação com Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="aea52-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="aea52-201">Em um único aplicativo, você pode ter serviços que sejam acessíveis por meio de TCP.</span><span class="sxs-lookup"><span data-stu-id="aea52-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="aea52-202">Outros serviços que podem ser acessados por meio de uma API REST de HTTP e ainda outros serviços podem estar acessíveis por meio de soquetes da Web.</span><span class="sxs-lookup"><span data-stu-id="aea52-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="aea52-203">Para obter informações sobre opções de saudação disponíveis e compensações de saudação envolvidas, consulte [se comunicar com serviços](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="aea52-203">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="aea52-204">Neste tutorial, usamos a [API Web ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="aea52-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a><span data-ttu-id="aea52-205">Atualizar o arquivo de VotesController.cs Olá</span><span class="sxs-lookup"><span data-stu-id="aea52-205">Update hello VotesController.cs file</span></span>
<span data-ttu-id="aea52-206">Em Olá **VotingWeb** projeto, abra Olá *Controllers/VotesController.cs* arquivo.</span><span class="sxs-lookup"><span data-stu-id="aea52-206">In hello **VotingWeb** project, open hello *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="aea52-207">Substituir saudação `VotesController` classe conteúdo de definição com a seguinte hello e salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="aea52-207">Replace hello `VotesController` class definition contents with hello following, then save your changes.</span></span>

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

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="aea52-208">Percorrer Olá votação de aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="aea52-208">Walk through hello voting sample application</span></span>
<span data-ttu-id="aea52-209">Olá votação aplicativo consiste em dois serviços:</span><span class="sxs-lookup"><span data-stu-id="aea52-209">hello voting application consists of two services:</span></span>
- <span data-ttu-id="aea52-210">(VotingWeb) de serviço front-end da Web – ASP.NET Core um serviço front-end, que serve a página da web de saudação e expõe web toocommunicate APIs com serviço de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="aea52-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="aea52-211">Serviço de back-end (VotingData)-um núcleo de ASP.NET web service, que expõe um voto de saudação do API toostore resulta em um dicionário confiável persistidos no disco.</span><span class="sxs-lookup"><span data-stu-id="aea52-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![Diagrama de aplicativo](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="aea52-213">Quando você vota em Olá Olá do aplicativo a seguir podem ocorrer eventos:</span><span class="sxs-lookup"><span data-stu-id="aea52-213">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="aea52-214">Um JavaScript envia Olá voto solicitação toohello API da web no serviço de front-end de web hello como uma solicitação HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="aea52-214">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="aea52-215">serviço de front-end de web Hello usa um proxy toolocate e encaminhar a um serviço de back-end de toohello de solicitação HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="aea52-215">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="aea52-216">serviço de back-end Olá leva a solicitação de entrada hello e repositórios Olá atualizado resultam em um dicionário confiável, que obtém toomultiple replicado nós no cluster hello e mantidos em disco.</span><span class="sxs-lookup"><span data-stu-id="aea52-216">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="aea52-217">Dados do aplicativo hello todos os são armazenados no cluster hello, portanto, nenhum banco de dados é necessária.</span><span class="sxs-lookup"><span data-stu-id="aea52-217">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="aea52-218">Depuração no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aea52-218">Debug in Visual Studio</span></span>
<span data-ttu-id="aea52-219">Ao depurar o aplicativo no Visual Studio, você usa um cluster de desenvolvimento local do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="aea52-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="aea52-220">Você tem Olá opção tooadjust seu cenário de tooyour experiência de depuração.</span><span class="sxs-lookup"><span data-stu-id="aea52-220">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="aea52-221">Neste aplicativo, armazenamos dados em nosso serviço de back-end, usando um dicionário confiável.</span><span class="sxs-lookup"><span data-stu-id="aea52-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="aea52-222">Visual Studio remove o aplicativo hello por padrão quando você interrompe o depurador hello.</span><span class="sxs-lookup"><span data-stu-id="aea52-222">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="aea52-223">Remover o aplicativo hello faz com que dados Olá Olá back-end tooalso serviço ser removido.</span><span class="sxs-lookup"><span data-stu-id="aea52-223">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="aea52-224">dados de saudação toopersist entre as sessões de depuração, você pode alterar Olá **o modo de depuração de aplicativo** como uma propriedade no hello **votação** projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aea52-224">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="aea52-225">toolook o que acontece no código hello, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="aea52-225">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="aea52-226">Olá abrir **VotesController.cs** arquivo e defina um ponto de interrupção da API da web hello **colocar** método (linha 47 -), você pode procurar arquivo Olá Olá Gerenciador de soluções do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aea52-226">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="aea52-227">Olá abrir **VoteDataController.cs** arquivo e defina um ponto de interrupção na API de web **colocar** método (linha 50).</span><span class="sxs-lookup"><span data-stu-id="aea52-227">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="aea52-228">Voltar toohello navegador e clique em uma opção de votação ou adicionar uma nova opção de votação.</span><span class="sxs-lookup"><span data-stu-id="aea52-228">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="aea52-229">Você atingiu o primeiro ponto de interrupção de saudação no controlador de api do Olá web front-end.</span><span class="sxs-lookup"><span data-stu-id="aea52-229">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="aea52-230">Isso é onde Olá JavaScript no navegador Olá envia um controlador de API da web solicitação toohello no serviço de front-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="aea52-230">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![Adicionar Serviço de Front-end de Voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="aea52-232">Primeiro, construímos Olá URL toohello ReverseProxy para nosso serviço de back-end **(1)**.</span><span class="sxs-lookup"><span data-stu-id="aea52-232">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="aea52-233">Em seguida, podemos enviar Olá HTTP PUT solicitação toohello ReverseProxy **(2)**.</span><span class="sxs-lookup"><span data-stu-id="aea52-233">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="aea52-234">Finalmente hello retornamos resposta de saudação do cliente do hello serviço back-end toohello **(3)**.</span><span class="sxs-lookup"><span data-stu-id="aea52-234">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="aea52-235">Pressione **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="aea52-235">Press **F5** toocontinue</span></span>
    1. <span data-ttu-id="aea52-236">Agora você está no ponto de interrupção Olá no serviço de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="aea52-236">You are now at hello break point in hello back-end service.</span></span>
    
    ![Adicionar Serviço de Back-End de Voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="aea52-238">Na primeira linha hello no método hello **(1)** estamos usando Olá `StateManager` tooget ou adicionar um dicionário confiável chamado `counts`.</span><span class="sxs-lookup"><span data-stu-id="aea52-238">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="aea52-239">Todas as interações com valores em um dicionário confiável exigem uma transação e, portanto, o uso da instrução **(2)** cria essa transação.</span><span class="sxs-lookup"><span data-stu-id="aea52-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="aea52-240">Transação Olá, é, em seguida, atualizar o valor de saudação de chave relevantes Olá Olá votar na opção e confirmações Olá operação **(3)**.</span><span class="sxs-lookup"><span data-stu-id="aea52-240">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="aea52-241">Depois de confirmar Olá método retorna, Olá dados são atualizados no dicionário hello e replicados tooother nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="aea52-241">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="aea52-242">dados de saudação agora são armazenados com segurança no cluster hello e serviço de back-end de saudação pode falhar em nós de tooother, ainda com dados de saudação disponíveis.</span><span class="sxs-lookup"><span data-stu-id="aea52-242">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="aea52-243">Pressione **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="aea52-243">Press **F5** toocontinue</span></span>

<span data-ttu-id="aea52-244">Olá toostop depuração sessão, pressione **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="aea52-244">toostop hello debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="aea52-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aea52-245">Next steps</span></span>
<span data-ttu-id="aea52-246">Nesta parte do tutorial do hello, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="aea52-246">In this part of hello tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aea52-247">Criar um serviço de API Web do ASP.NET Core como um Reliable Services com estado</span><span class="sxs-lookup"><span data-stu-id="aea52-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="aea52-248">Criar um serviço de Aplicativo Web do ASP.NET Core como um serviço Web sem estado</span><span class="sxs-lookup"><span data-stu-id="aea52-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="aea52-249">Use Olá proxy reverso toocommunicate com o serviço de monitoração de estado Olá</span><span class="sxs-lookup"><span data-stu-id="aea52-249">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="aea52-250">Tutorial de Avançar de toohello avançado:</span><span class="sxs-lookup"><span data-stu-id="aea52-250">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="aea52-251">Implantar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="aea52-251">Deploy hello application tooAzure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
