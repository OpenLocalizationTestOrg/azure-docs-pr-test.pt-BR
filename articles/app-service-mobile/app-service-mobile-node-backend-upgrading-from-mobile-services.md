---
title: "aaaUpgrade de serviços móveis tooAzure do serviço de aplicativo - Node. js"
description: "Saiba como tooeasily atualizar seu aplicativo de serviços móveis tooan aplicativo móvel do serviço de aplicativo"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a>Atualizar seu tooApp de Node.js do Azure Mobile Service serviço existente
Serviço de aplicativo móvel é uma nova maneira toobuild aplicativos móveis usando o Microsoft Azure. mais, consulte toolearn [quais são os aplicativos móveis?].

Este tópico descreve como tooupgrade um aplicativo de back-end node. js existente de serviços móveis do Azure tooa novos aplicativos do aplicativo serviços móveis. Enquanto você executa esta atualização, o seu aplicativo de serviços móveis pode continuar toooperate.  Se você precisar tooupgrade um aplicativo de back-end node. js, consulte muito[atualizando seus serviços móveis de .NET](app-service-mobile-net-upgrading-from-mobile-services.md).

Quando um back-end móvel é atualizado tooAzure do serviço de aplicativo, ele tem acesso tooall recursos de serviço de aplicativo e são cobradas de acordo com muito[preços do serviço de aplicativo], não os serviços móveis de preços.

## <a name="migrate-vs-upgrade"></a>Migração vs. atualização
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Recomendamos a [execução de uma migração](app-service-mobile-migrating-from-mobile-services.md) antes de executar uma atualização. Dessa forma, você pode colocar as duas versões do seu aplicativo hello mesmo plano de serviço de aplicativo e incorrer em nenhum custo adicional.
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a>Aprimoramentos no SDK do servidor Node.js de Aplicativos Móveis
Atualizando toohello novo [SDK de aplicativos móveis](https://www.npmjs.com/package/azure-mobile-apps) fornece muitas melhorias, incluindo:

* Com base em Olá [Express framework](http://expressjs.com/en/index.html), novo nó SDK hello é leve e projetado tookeep backup com novas versões de nó, como eles surgem. Você pode personalizar o comportamento do aplicativo hello com middleware Express.
* Melhorias significativas de desempenho em comparação com toohello SDK dos serviços móveis.
* Agora você pode hospedar um site junto com seu back-end móvel; da mesma forma, é fácil tooadd Olá SDK do Azure Mobile tooany express.v4 aplicativo existente.
* Criado para o desenvolvimento local e de plataforma cruzada, Olá SDK de aplicativos móveis pode ser desenvolvido e executado localmente em plataformas Windows, Linux e OSX. Agora é fácil toouse comuns técnicas de nó desenvolvimento como execução [recusar](https://mochajs.org/) testes toodeployment anterior.

## <a name="overview"></a>Visão geral da atualização básica
tooaid atualizar um Node. js back-end, o serviço de aplicativo do Azure fornece um pacote de compatibilidade.  Após a atualização, você terá um site niew que pode ser implantado tooa novo site de serviço de aplicativo.

cliente de serviços móveis Olá SDKs são **não** compatível com o servidor de aplicativos móveis novo Olá SDK. Continuidade de tooprovide de ordem de serviço para seu aplicativo, você não deve publicar site tooa de alterações no momento que atendem a clientes publicados. Em vez disso, você deve criar um novo aplicativo móvel que sirva como uma duplicata. Você pode colocar esse aplicativo em Olá mesmo serviço de aplicativo planejar tooavoid incorrer em custos financeiros adicionais.

Em seguida, você terá duas versões do aplicativo hello: que permanece Olá mesmo serve aplicativos publicados solta hello e outras que você pode, em seguida, atualizar e destino com um novo cliente de versão. Você pode mover e testar seu código no seu ritmo, mas você deve ter certeza de que as correções de bug que fazer obter tooboth aplicado. Depois que você acha que um número desejado de aplicativos de cliente externo atualizou a versão mais recente do toohello, você pode excluir o aplicativo migrado original de saudação se desejar. Ele não incorre em custos monetários adicionais, se hospedado no mesmo serviço de aplicativo planejar como seu aplicativo móvel de saudação.

estrutura de tópicos completa para o processo de atualização Olá Olá é o seguinte:

1. Baixar seu Serviço Móvel do Azure (migrado) atual.
2. Converter Olá projeto tooan aplicativo móvel do Azure usando o pacote de compatibilidade de saudação.
3. Corrigir quaisquer diferenças (como configurações de autenticação).
4. Implantar o tooa de projeto de aplicativo do Azure Mobile convertido novo serviço de aplicativo.
5. Libere uma nova versão do seu aplicativo cliente que use Olá novo aplicativo móvel.
6. (Opcional) Excluir seu aplicativo de serviço móvel migrado original.

A exclusão pode ocorrer quando você não vê nenhum tráfego no serviço móvel migrado original.

## <a name="install-npm-package"></a>Instalar os pré-requisitos de saudação
Você deve instalar o [Node] em seu computador local.  Você também deve instalar o pacote de compatibilidade de saudação.  Depois que o nó estiver instalado, você pode executar Olá comando a seguir de um cmd novo ou o prompt do PowerShell:

```npm i -g azure-mobile-apps-compatibility```

## <a name="obtain-ams-scripts"></a> Obter os scripts dos Serviços Móveis do Azure
* Faça logon no toohello [Portal do Azure].
* Usando **Todos os Recursos** ou **Serviços de Aplicativos**, encontre seu site de Serviços Móveis.
* No site de saudação, clique em **ferramentas** -> **Kudu** -> **vá** site de Kudu Olá tooopen.
* Clique em **Console depuração** -> **PowerShell** tooopen console de depuração de saudação.
* Navegue muito`site/wwwroot/App_Data/config` clicando em cada diretório por sua vez
* Clique em download de saudação ícone toohello próximo `scripts` directory.

Isso fará o download scripts Olá em formato ZIP.  Criar um novo diretório em seu computador local e descompacte Olá `scripts.ZIP` arquivo no diretório de saudação.  Isso criará um diretório `scripts` .

## <a name="scaffold-app"></a>Scaffold Olá novos aplicativos do Azure Mobile back-end
Saudação de execução a seguir de comando de diretório Olá que contém o diretório de scripts de saudação:

```scaffold-mobile-app scripts out```

Isso criará um back-end do Azure Mobile aplicativos scaffolding Olá `out` directory.  Embora não seja necessário, é uma saudação de toocheck boa ideia `out` diretório em um repositório de código de origem de sua escolha.

## <a name="deploy-ama-app"></a> Implantar seu back-end de Aplicativos Móveis do Azure
Durante a implantação, você precisará a seguir Olá toodo:

1. Criar um novo aplicativo móvel no hello [Portal do Azure].
2. Executar Olá `createViews.sql` script em seu banco de dados conectado.
3. Link Olá banco de dados vinculado tooyour serviço móvel tooyour novo serviço de aplicativo.
4. Link de quaisquer outros recursos (como Hubs de notificação) toohello novo serviço de aplicativo.
5. Implante Olá gerado código tooyour novo site.

### <a name="create-a-new-mobile-app"></a>Criar um novo Aplicativo Móvel
1. Faça logon em Olá [Portal do Azure].
2. Clique em **+NOVO** > **Web + Móvel** > **Aplicativo Móvel**, então forneça um nome para o back-end do Aplicativo Móvel.
3. Para Olá **grupo de recursos**, selecione um grupo de recursos existente ou criar um novo (usando Olá o mesmo nome de seu aplicativo).

    Você pode selecionar outro plano de Serviço de Aplicativo ou criar um novo. Para obter mais informações sobre planos de serviços de aplicativos e como toocreate um novo plano em um preço diferente de camada e no local desejado, consulte [visão geral detalhada de planos de serviço de aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Para Olá **plano de serviço de aplicativo**, plano de padrão de saudação (em hello [camada padrão](https://azure.microsoft.com/pricing/details/app-service/)) está selecionado. Você também pode selecionar um plano diferente ou [criar um novo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). configurações do plano do serviço de aplicativo Hello determinam Olá [local, recursos, custo e os recursos de computação](https://azure.microsoft.com/pricing/details/app-service/) associados ao seu aplicativo.

    Depois de decidir plano hello, clique em **criar**. Isso cria um back-end de aplicativo móvel hello.

### <a name="run-createviewssql"></a>Executar CreateViews.SQL
aplicativo de scaffolding Olá contém um arquivo chamado `createViews.sql`.  Esse script deve ser executado no banco de dados de destino.  cadeia de caracteres de conexão de saudação do banco de dados de destino de saudação pode ser obtida seu serviço móvel migrado Olá **configurações** folha sob **cadeias de caracteres de Conexão**.  Ela é chamada de `MS_TableConnectionString`.

Você pode executar esse script no SQL Server Management Studio ou no Visual Studio.

### <a name="link-hello-database-tooyour-app-service"></a>Saudação de link tooyour de banco de dados do serviço de aplicativo
Saudação de link existente tooyour de banco de dados do serviço de aplicativo:

* Em Olá [Portal do Azure], abra o serviço de aplicativo.
* Selecione **Todas as Configurações** -> **Conexões de Dados**.
* Clique em **+ Adicionar**.
* No hello lista suspensa, selecione **banco de dados SQL**
* Em **Banco de Dados SQL**, selecione o banco de dados existente, clique em **Selecionar**.
* Em **cadeia de caracteres de Conexão**, digite Olá username e password para banco de dados de saudação e clique em **Okey**.
* Em Olá **adicionar conexões de dados** folha, clique em **Okey**.

saudação de nome de usuário e senha podem ser encontradas visualizando hello cadeia de caracteres de Conexão para o banco de dados de destino Olá no seu serviço móvel migrados.

### <a name="set-up-authentication"></a>Configurar a autenticação
Aplicativos móveis do Azure permite a autenticação do Active Directory do Azure, Facebook, Google, Microsoft e Twitter tooconfigure no serviço de saudação.  Autenticação personalizada será necessário toobe desenvolvido separadamente.  Consulte Olá [conceitos de autenticação] documentação e [autenticação Quickstart] documentação para obter mais informações.  

## <a name="updating-clients"></a>Atualizar clientes móveis
Quando você tiver um back-end do Aplicativo Móvel operacional, poderá trabalhar em uma nova versão de seu aplicativo cliente para consumi-lo. Aplicativos móveis também inclui uma nova versão do cliente Olá SDKs e atualização do servidor toohello semelhante acima, você precisará tooremove todas as referências toohello Mobile Services SDKs antes de instalar as versões de aplicativos móveis.

Uma das principais alterações Olá entre versões de saudação é que construtores de saudação não exigem uma chave de aplicativo.
Você agora simplesmente passar na URL de saudação do seu aplicativo móvel. Por exemplo, em clientes do .NET hello, Olá `MobileServiceClient` construtor agora é:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

Você pode ler sobre como instalar Olá novos SDKs e usando a nova estrutura de saudação por meio de links de saudação abaixo:

* [Android versão 2.2 ou posterior](app-service-mobile-android-how-to-use-client-library.md)
* [iOS versão 3.0.0 ou posterior](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) versão 2.0.0 ou posterior](app-service-mobile-dotnet-how-to-use-client-library.md)
* [Apache Cordova versão 2.0 ou posterior](app-service-mobile-cordova-how-to-use-client-library.md)

Se seu aplicativo usar notificações por push, tome nota da saudação instruções de registro específico para cada plataforma, como Houve algumas alterações também.

Quando você tiver Olá nova versão do cliente pronto, experimente-o em seu projeto de servidor atualizado. Após validar que ele funciona, você pode liberar uma nova versão do seu aplicativo toocustomers. Eventualmente, depois que os clientes tiveram uma chance tooreceive essas atualizações, você pode excluir a versão de serviços móveis de saudação do seu aplicativo. Neste ponto, você tiver atualizado tooan aplicativo móvel do serviço de aplicativo usando o servidor de aplicativos móveis mais recente Olá SDK.

<!-- URLs. -->

[Portal do Azure]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[quais são os aplicativos móveis?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[preços do serviço de aplicativo]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[conceitos de autenticação]: ../app-service/app-service-authentication-overview.md
[autenticação Quickstart]: app-service-mobile-auth.md

[Portal do Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
