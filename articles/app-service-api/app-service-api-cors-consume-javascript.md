---
title: "aaaCORS suporte no serviço de aplicativo | Microsoft Docs"
description: "Saiba como toouse CORS dão suporte ao serviço de aplicativo do Azure do Azure."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a>Consumir um aplicativo de API do JavaScript usando CORS
Serviço de aplicativo oferece suporte interno para [compartilhamento de recursos entre origens (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), que permite que o JavaScript clientes entre toomake domínios chama tooAPIs que são hospedados em aplicativos de API. Serviço de aplicativo permite configurar CORS acesso tooyour API sem gravar qualquer código em sua API.

Este artigo contém duas seções:

* Olá [como tooconfigure CORS](#corsconfig) seção explica como geral tooconfigure CORS para qualquer aplicativo de API, aplicativo web ou aplicativo móvel. Ele se aplica igualmente tooall estruturas que são suportadas pelo serviço de aplicativo, incluindo .NET, Node.js e Java. 
* Começando com hello [continuar tutoriais de Introdução .NET de saudação](#tutorialstart) seção, artigo Olá é um tutorial que demonstra o suporte de CORS com base em que você fez [Olá primeiro aplicativos de API tutorial de Introdução ](app-service-api-dotnet-get-started.md). 

## <a id="corsconfig"></a>Como tooconfigure CORS no serviço de aplicativo do Azure
Você pode configurar CORS no hello portal do Azure ou usando [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) ferramentas.

#### <a name="configure-cors-in-hello-azure-portal"></a>Configurar CORS Olá portal do Azure
1. Em um navegador, vá toohello [portal do Azure](https://portal.azure.com/).
2. Clique em **serviços de aplicativos**e, em seguida, clique em nome de saudação do seu aplicativo de API.
   
    ![Selecione o aplicativo de API no portal](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. Em Olá **configurações** folha que abre toohello direito da saudação **aplicativo de API** folha, localizar Olá **API** seção e, em seguida, clique em **CORS**.
   
   ![Selecione CORS na folha configurações](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. Na caixa de texto de saudação digite Olá URL ou URLs que você deseja tooallow toocome de chamadas de JavaScript do.

    Por exemplo, se você implantou seu aplicativo web do JavaScript aplicativo tooa denominado todolistangular, digite "https://todolistangular.azurewebsites.net". Como alternativa, você pode inserir um toospecify de asterisco (*) que todos os domínios de origem são aceitos.


1. Clique em **Salvar**.
   
   ![Clique em Salvar](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Depois de clicar em **salvar**, aplicativo hello API aceitará JavaScript chamadas de saudação especificado URLs.

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a>Configurar CORS usando as ferramentas do Azure Resource Manager
Você também pode configurar o CORS para um aplicativo de API usando [modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) em ferramentas de linha de comando como [Azure PowerShell](/powershell/azureps-cmdlets-docs) e hello [CLI do Azure](../cli-install-nodejs.md). 

Para obter um exemplo de um modelo do Azure Resource Manager que define a propriedade CORS hello, abra Olá [arquivo azuredeploy.json no repositório de saudação aplicativo neste tutorial de exemplo](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Localize a seção de saudação do modelo de saudação que se parece com hello exemplo a seguir:

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <a id="tutorialstart"></a>Continuando o tutorial de Introdução .NET de saudação
Se você estiver seguindo Olá Node. js Java Introdução série ou para aplicativos de API, você ter concluído Olá obtendo série iniciada. Ignorar toohello [próximas etapas](#next-steps) seção toofind sugestões para aprender mais sobre aplicativos de API.

Olá restante deste artigo é uma continuação de saudação série de guia de Introdução .NET e presume que você concluiu com êxito [tutorial primeiro Olá](app-service-api-dotnet-get-started.md).

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a>Implantar Olá ToDoListAngular projeto tooa novo aplicativo web
Em [tutorial primeiro Olá](app-service-api-dotnet-get-started.md), você criou um aplicativo de camada intermediária API e um aplicativo de API de camada de dados. Neste tutorial você criar um aplicativo web do aplicativo de página única (SPA) esse aplicativo de camada intermediária API Olá chamadas. Para Olá SPA toowork tiver tooenable CORS na camada intermediária de saudação do aplicativo de API. 

Em Olá [aplicativo de amostra ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), projeto de ToDoListAngular Olá é um cliente AngularJS simples que chama o projeto de API da Web de ToDoListAPI de camada intermediária hello. Olá código JavaScript em Olá *app/scripts/todoListSvc.js* arquivo chama a API de saudação usando Olá HTTP AngularJS provedor. 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a>Criar um novo aplicativo web para o projeto de ToDoListAngular Olá
Olá procedimento toocreate um novo aplicativo web do serviço de aplicativo e implantar um projeto tooit é semelhante toowhat você viu para [criando e implantando um aplicativo de API no primeiro tutorial Olá nesta série](app-service-api-dotnet-get-started.md#createapiapp). Olá somente a diferença é que tipo de aplicativo hello é **aplicativo Web** em vez de **API App**.  Para capturas de tela de caixas de diálogo hello, consulte 

1. Em **Solution Explorer**, clique com botão direito Olá ToDoListAngular e, em seguida, clique em **publicar**.
2. Em Olá **perfil** guia da saudação **Publicar Web** assistente, clique em **serviço de aplicativo do Microsoft Azure**.
3. Em Olá **do serviço de aplicativo** caixa de diálogo, clique em **novo**.
4. Em Olá **hospedagem** guia da saudação **criar serviço de aplicativo** caixa de diálogo, digite um **nome do aplicativo Web** que é exclusivo no hello *azurewebsites.net* domínio. 
5. Escolha hello Azure **assinatura** toowork com desejado.
6. Em Olá **grupo de recursos** lista suspensa, escolha Olá mesmo grupo de recursos que você criou anteriormente.
7. Em Olá **plano do serviço de aplicativo** lista suspensa, escolha Olá mesmo plano que você criou anteriormente. 
8. Clique em **Criar**.
   
    Visual Studio cria um aplicativo da web de saudação, cria um perfil de publicação para ele e exibe o saudação **Conexão** etapa Olá **Publicar Web** assistente.
   
    Não clique **Publicar** ainda. Olá seção a seguir, você configura Olá novo aplicativo web e aplicativo toocall Olá API de camada intermediária que está em execução no serviço de aplicativo. 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a>Definir a URL de camada intermediária de saudação em configurações do aplicativo web
1. Vá toohello [portal do Azure](https://portal.azure.com/)e, em seguida, navegue toohello **aplicativo Web** folha para o aplicativo web de saudação que você criou o projeto do toohost Olá TodoListAngular (front-end).
2. Clique em **Configurações > Configurações do Aplicativo**.
3. Em Olá **configurações do aplicativo** seção, adicione o seguinte Olá chave e valor:
   
   | Chave | Valor | Exemplo |
   | --- | --- | --- |
   | toDoListAPIURL |https://{nome de aplicativo de API de tipo médio}.azurewebsites.net |https://todolistapi0121.azurewebsites.net |
4. Clique em **Salvar**.
   
    Quando o código de saudação é executado no Azure, esse valor substitui Olá localhost URL que está em Olá *Web. config* arquivo. 
   
    Olá código obtém o valor da configuração hello está em *cshtml*:
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    Olá código *todoListSvc.js* usa a configuração de saudação:
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a>Implantar Olá ToDoListAngular web projeto toohello novo aplicativo web
* No Visual Studio, no hello **Conexão** etapa Olá **Publicar Web** assistente, clique em **publicar**.
  
   Visual Studio implanta Olá ToDoListAngular projeto toohello novo aplicativo web e abre uma URL de toohello do navegador do aplicativo web de saudação. 

### <a name="test-hello-application-without-cors-enabled"></a>Testar o aplicativo hello sem CORS habilitado
1. Em seu navegador, ferramentas de desenvolvedor, abra a janela de Console de saudação.
2. Na janela de navegador Olá que exibe o saudação AngularJS UI, clique em Olá **tooDo lista** link.
   
    Olá código JavaScript tenta toocall Olá intermediária da camada de aplicativo de API, mas chamada hello falha porque front-end hello está sendo executado em um domínio diferente Olá volta final. janela de Console de ferramentas de desenvolvedor do navegador Olá mostra uma mensagem de erro entre origens.
   
    ![Mensagem de erro entre origens](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a>Configurar CORS para a camada intermediária de saudação do aplicativo de API
Nesta seção, você configurar Olá CORS no Azure para a camada intermediária de saudação do aplicativo de API ToDoListAPI. Essa configuração permitirá Olá camada intermediária aplicativo tooreceive JavaScript chamadas de API do aplicativo web hello que você criou para o projeto de ToDoListAngular hello.

1. Em um navegador, vá toohello [portal do Azure](https://portal.azure.com/).
2. Clique em **serviços de aplicativos**e, em seguida, clique em aplicativo hello API ToDoListAPI (camada intermediária).
   
    ![Selecione o aplicativo de API no portal](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. Em Olá **configurações** folha que abre toohello direito da saudação **aplicativo de API** folha, localizar Olá **API** seção e, em seguida, clique em **CORS**.
   
   ![Selecione CORS no portal](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. Na caixa de texto de saudação, insira a URL de saudação do aplicativo de web hello ToDoListAngular (front-end). Por exemplo, se você implantou o aplicativo hello ToDoListAngular projeto tooa web chamado todolistangular0121, permitir chamadas no URL Olá `https://todolistangular0121.azurewebsites.net`.
   
   Como alternativa, você pode inserir um toospecify de asterisco (*) que todos os domínios de origem são aceitos.
5. Clique em **Salvar**.
   
   ![Clique em Salvar](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Depois de clicar em **salvar**, aplicativo hello API aceitará JavaScript chamadas de saudação especificou a URL. Na captura de tela, aplicativo de API ToDoListAPI0223 Olá aceitará chamadas de cliente JavaScript do aplicativo de web ToDoListAngular hello.

### <a name="test-hello-application-with-cors-enabled"></a>Testar o aplicativo hello com CORS habilitado
* Abra um navegador toohello HTTPS URL do aplicativo web de saudação. 
  
    Este aplicativo de saudação do tempo permite exibir, adicionar, editar e excluir itens de tarefas pendentes. 
  
    ![página de lista de tooDo do aplicativo de exemplo](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a>CORS do Serviço de Aplicativo versus CORS da API Web
Em um projeto de API da Web, você pode instalar Olá [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) toospecify de pacote do NuGet no código que domínios sua API aceitará o JavaScript chama de.

O suporte a CORS da API Web é mais flexível do que o suporte a CORS do Serviço de Aplicativo. Por exemplo, você pode especificar no código diferentes origens aceitas para diferentes métodos de ação, enquanto para o CORS do Serviço de Aplicativo, você especifica um conjunto de origens aceitas para todos os métodos do aplicativo de API.

> [!NOTE]
> Não tente toouse CORS da API da Web e CORS de serviço de aplicativo em um aplicativo de API. O CORS do Serviço de Aplicativo terá a precedência e o CORS da API Web não funcionará. Por exemplo, se você habilitar um domínio de origem no serviço de aplicativo e habilitar todos os domínios de origem em seu código de API da Web, seu aplicativo de API do Azure só aceitará chamadas de domínio Olá especificado no Azure.
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a>Como tooenable CORS no código da API da Web
Olá etapas a seguir resumem processo Olá para habilitar o suporte de CORS da API da Web. Para saber mais, confira [Permitindo solicitações entre origens na API Web ASP.NET 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).

1. Em um projeto de API da Web, instale o hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) pacote NuGet.
2. Incluir um `config.EnableCors()` linha de código em Olá **registrar** método hello **WebApiConfig** classe, como no exemplo a seguir de saudação. 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. No controlador de API da Web, adicione um `using` instrução Olá `System.Web.Http.Cors` namespace e adicione Olá `EnableCors` métodos de ação toohello controlador tooindividual ou classe de atributo. Olá exemplo a seguir, o suporte de CORS aplica-se controlador todo toohello.
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a>Uso do Gerenciamento de API com Aplicativos de API
Se você usar o gerenciamento de API do Azure com um aplicativo de API, configure CORS no gerenciamento de API em vez de no aplicativo de API de saudação. Para obter mais informações, consulte Olá recursos a seguir:

* [Visão geral do Gerenciamento de API do Azure (vídeo: CORS começa em 12:10)](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [Políticas entre domínios de Gerenciamento de API](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a>Solucionar problemas
Caso você encontre um problema ao percorrer este tutorial, aqui estão algumas ideias para solução de problemas.

* Certifique-se de que você está usando a versão mais recente de saudação do hello [SDK do Azure para .NET para Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).
* Certifique-se de que você inseriu `https` Olá configuração CORS e certifique-se de que você está usando `https` toorun Olá web front-end aplicativo.
* Certifique-se de que você inseriu uma configuração de CORS saudação no aplicativo de API de camada intermediária hello, não no aplicativo da web front-end de saudação.
* Se você estiver configurando CORS no código do aplicativo e serviço de aplicativo do Azure, observe que configuração de CORS de serviço de aplicativo hello substituirá o que você está fazendo no código do aplicativo. 

toolearn mais sobre os recursos do Visual Studio que simplificam a solução de problemas, consulte [aplicativos de solução de problemas do serviço de aplicativo do Azure no Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você viu como tooenable CORS de serviço de aplicativo compatível para que o código JavaScript cliente possa chamar uma API em um domínio diferente. toolearn mais sobre aplicativos de API, ler Olá [tooauthentication de Introdução no serviço de aplicativo](../app-service/app-service-authentication-overview.md), e em seguida, acesse toohello [autenticação de usuário para aplicativos de API](app-service-api-dotnet-user-principal-auth.md) tutorial.

