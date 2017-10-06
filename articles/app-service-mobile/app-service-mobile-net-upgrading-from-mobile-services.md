---
title: "aaaUpgrade de tooAzure de serviços móveis do serviço de aplicativo"
description: "Saiba como tooeasily atualizar seu aplicativo de serviços móveis tooan aplicativo móvel do serviço de aplicativo"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 9c0ac353-afb6-462b-ab94-d91b8247322f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b75a1b824e8ef0d36c9053f2f19af051479f928
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-tooapp-service"></a>Atualizar seu tooApp existente de serviço do .NET do Azure Mobile Service
Serviço de aplicativo móvel é uma nova maneira toobuild aplicativos móveis usando o Microsoft Azure. mais, consulte toolearn [quais são os aplicativos móveis?].

Este tópico descreve como tooupgrade um aplicativo de back-end .NET de serviços móveis do Azure tooa novos aplicativos do aplicativo serviços móveis. Enquanto você executa esta atualização, o seu aplicativo de serviços móveis pode continuar toooperate.   Se você precisar tooupgrade um aplicativo de back-end node. js, consulte muito[atualizando seus serviços móveis de Node. js](app-service-mobile-node-backend-upgrading-from-mobile-services.md).

Quando um back-end móvel é atualizado tooAzure do serviço de aplicativo, ele tem acesso tooall recursos de serviço de aplicativo e são cobradas de acordo com muito[preços do serviço de aplicativo], não os serviços móveis de preços.

## <a name="migrate-vs-upgrade"></a>Migração vs. atualização
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Recomendamos a [execução de uma migração](app-service-mobile-migrating-from-mobile-services.md) antes de executar uma atualização. Dessa forma, você pode colocar as duas versões do seu aplicativo hello mesmo plano de serviço de aplicativo e incorrer em nenhum custo adicional.
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a>Aprimoramentos no SDK do servidor .NET de aplicativos móveis
Atualizando toohello novo [SDK de aplicativos móveis](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) fornece Olá benefícios a seguir:

* Mais flexibilidade em dependências do NuGet. Olá ambiente de hospedagem não fornece suas próprias versões dos pacotes do NuGet, então você pode usar versões compatíveis alternativas. No entanto, se houver novas bugfixes crítico ou toohello de atualizações de segurança móvel servidor SDK ou dependências, você deve atualizar manualmente seu serviço.
* Mais flexibilidade no hello SDK móvel. Explicitamente, você pode controlar quais recursos e rotas são configuradas, como autenticação, tabela APIs e Olá ponto de extremidade de registro de envio por push. mais, consulte toolearn [como toouse Olá SDK do servidor do .NET para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).
* Suporte para outros tipos de projeto do ASP.NET e rotas. Agora você pode hospedar controladores MVC e a API da Web no mesmo projeto de saudação do seu projeto móvel de back-end.
* Suporte para novos recursos de autenticação do serviço de aplicativo, que permite que você toouse uma configuração de autenticação comum em seus aplicativos web e móveis.

## <a name="overview"></a>Visão geral da atualização básica
Em muitos casos, a atualização será ser tão simple quanto alternar o servidor de aplicativos móveis novo toohello SDK e republicar seu código em uma nova instância de aplicativo móvel. Há, no entanto, alguns cenários que exigem alguma configuração adicional, como cenários avançados de autenticação e trabalhar com trabalhos agendados. Cada um deles é abordada em Olá seções mais tarde.

> [!TIP]
> É recomendável ler e entender o restante deste tópico Olá completamente antes de iniciar uma atualização. Tome nota de todos os recursos que você usar que são descritos abaixo.
>
>

cliente de serviços móveis Olá SDKs são **não** compatível com o servidor de aplicativos móveis novo Olá SDK. Continuidade de tooprovide de ordem de serviço para seu aplicativo, você não deve publicar site tooa de alterações no momento que atendem a clientes publicados. Em vez disso, você deve criar um novo aplicativo móvel que sirva como uma duplicata. Você pode colocar esse aplicativo em Olá mesmo serviço de aplicativo planejar tooavoid incorrer em custos financeiros adicionais.

Em seguida, você terá duas versões do aplicativo hello: um que permanece Olá mesmo e serve aplicativos publicados no hello curinga e hello outros que você pode, em seguida, atualizar e destino com uma nova versão do cliente. Você pode mover e testar seu código no seu ritmo, mas você deve ter certeza de que as correções de bug que fazer obter tooboth aplicado. Depois que você acha que um número desejado de aplicativos de cliente da saudação wild atualizou a versão mais recente do toohello, você pode excluir o aplicativo migrado original de saudação se desejar.

estrutura de tópicos completa para o processo de atualização Olá Olá é o seguinte:

1. Criar um novo Aplicativo Móvel
2. Atualização Olá projeto toouse Olá SDKs do novo servidor
3. Lançar uma nova versão do aplicativo cliente
4. (Opcional) Excluir sua instância original migrada

## <a name="mobile-app-version"></a>Criando uma segunda instância do aplicativo
Olá, primeira etapa na atualização é toocreate recursos de aplicativo móvel de saudação que hospedarão a nova versão de saudação do seu aplicativo. Se você já migrou um serviço móvel existente, você desejará toocreate esta versão no hello mesmo plano de hospedagem. Olá abrir [portal do Azure] e navegue tooyour migrados do aplicativo. Anote Olá plano de serviço de aplicativo estiver em execução.

Em seguida, crie a segunda instância de aplicativo hello pelo seguinte Olá [instruções de criação de back-end .NET](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app). Quando solicitada tooselect você plano do serviço de aplicativo ou "plano de hospedagem" Escolha Olá plano do aplicativo migrado.

Você provavelmente desejará toouse Olá mesmo banco de dados e Hub de notificação como você fez nos serviços móveis. Você pode copiar esses valores abrindo [portal do Azure] e navegar em aplicativo original toohello, clique em **configurações** > **configurações de aplicativo**. Em **Cadeias de Conexão**, copie `MS_NotificationHubConnectionString` e `MS_TableConnectionString`. Navegue tooyour novo site de atualização e colá-los em, substituindo qualquer valor existente. Repita esse processo para quaisquer outras configurações de aplicativo exigidas por seu aplicativo. Se não usar um serviço migradas, você pode ler cadeias de caracteres de conexão e as configurações do aplicativo de saudação **configurar** guia da saudação seção de serviços móveis do hello [portal clássico do Azure].

Faça uma cópia do projeto do ASP.NET Olá para seu aplicativo e publicá-lo tooyour novo site. Usando uma cópia do seu aplicativo cliente atualizado com a nova URL a saudação, valide que tudo está funcionando conforme o esperado.

## <a name="updating-hello-server-project"></a>Atualizando o projeto do servidor de saudação
Aplicativos móveis fornece um novo [SDK de servidor de aplicativos móveis] que fornece grande parte da saudação mesma funcionalidade de tempo de execução de serviços móveis hello. Primeiro, você deve remover todos os pacotes de serviços móveis toohello de referências. No Gerenciador de pacotes do NuGet hello, procure `WindowsAzure.MobileServices.Backend`. A maioria dos aplicativos exibirá vários pacotes aqui, incluindo `WindowsAzure.MobileServices.Backend.Tables` e `WindowsAzure.MobileServices.Backend.Entity`. Nesse caso, começar com o pacote de saudação mais baixo na árvore de dependência hello, como `Entity`e removê-lo. Quando solicitado, não remova todos os pacotes dependentes. Repita este processo até remover o próprio `WindowsAzure.MobileServices.Backend`.

Neste momento, você terá um projeto que não faz referência a SDKs de Serviços Móveis.

Em seguida, você adicionará as referências Olá SDK de aplicativos móveis. Para esta atualização, a maioria dos desenvolvedores deseja toodownload e instalar Olá `Microsoft.Azure.Mobile.Server.Quickstart` do pacote, pois isso buscará em todo o conjunto necessário de saudação.

Haverá alguns erros de compilador resultantes de diferenças entre os SDKs Olá, mas essas são tooaddress fácil e são abordadas no restante desta seção hello.

### <a name="base-configuration"></a>Configuração base
Em seguida, em WebApiConfig.cs, você pode substituir:

        // Use this class tooset configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class tooset WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

por:

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> Se você desejar toolearn mais sobre Olá novo .NET SDK do servidor e como tooadd ou remover recursos de seu aplicativo, consulte Olá [como toouse Olá servidor .NET SDK] tópico.
>
>

Se seu aplicativo usar saudação recursos de autenticação, você também precisará tooregister um owin. Nesse caso, você deve mover Olá acima código de configuração para uma nova classe de inicialização OWIN.

1. Adicionar pacote de NuGet Olá `Microsoft.Owin.Host.SystemWeb` se ele não ainda esteja incluído em seu projeto.
2. No Visual Studio, clique com o botão direito do mouse em seu projeto e selecione **Adicionar** -> **Novo Item**. Selecione **Web** -> **Geral** -> **Classe de inicialização OWIN**.
3. Mover Olá acima código MobileAppConfiguration de `WebApiConfig.Register()` toohello `Configuration()` método de sua nova classe de inicialização.

Verifique se Olá `Configuration()` método termina com:

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

Há alterações adicionais tooauthentication relacionados que são abordados na seção de autenticação completa Olá abaixo.

### <a name="working-with-data"></a>Trabalhando com dados
Nos serviços móveis, nome de aplicativo móvel Olá servidos como nome do esquema padrão Olá na instalação do Entity Framework hello.

tooensure tiver Olá mesmo esquema que está sendo referenciado como antes, use Olá tooset esquema Olá Olá DbContext para seu aplicativo a seguir:

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

Verifique se que você tem MS_MobileServiceName definida se você Olá acima. Você pode fornecer outro nome de esquema se o seu aplicativo o tiver personalizado anteriormente.

### <a name="system-properties"></a>Propriedades do Sistema
#### <a name="naming"></a>Nomenclatura
No servidor de serviços móveis do Azure Olá SDK, as propriedades do sistema sempre contêm um sublinhado duplo (`__`) prefixo para propriedades de saudação:

* __createdAt
* __updatedAt
* __deleted
* __version

cliente de serviços móveis Olá SDKs tem uma lógica especial para analisar as propriedades do sistema neste formato.

Aplicativos móveis do Azure, propriedades do sistema não tem um especial Formatar e ter Olá nomes a seguir:

* createdAt
* updatedAt
* deleted
* version

Olá, aplicativos móveis cliente SDKs use Olá novos nomes do sistema propriedades, para que nenhuma alteração é necessária tooclient código. No entanto, se você estiver diretamente fazer REST chama o serviço de tooyour, em seguida, você deve alterar suas consultas.

#### <a name="local-store"></a>Armazenamento local
Olá alterações toohello nomes de propriedades do sistema significam que um banco de dados local de sincronização offline para serviços móveis não é compatível com aplicativos móveis. Se possível, evite Atualizando aplicativos de cliente de serviços móveis tooMobile que aplicativos até após as alterações pendentes foram enviados toohello server. Em seguida, aplicativo atualizado Olá deve usar um novo nome de arquivo de banco de dados.

Se um aplicativo cliente é atualizado de serviços móveis tooMobile aplicativos enquanto houver alterações offline pendentes na fila de operação hello, banco de dados de sistema Olá deve ser atualizada toouse Olá novos nomes de coluna. No iOS, isso pode ser feito usando nomes de coluna migrações leve toochange hello. No Android e hello gerenciado cliente .NET, você deve gravar toorename personalizado do SQL Olá colunas para as tabelas de objeto de dados.

No iOS, você deve alterar o esquema de dados principal para seu dados a seguir entidades toomatch hello. Observe que Olá propriedades `createdAt`, `updatedAt` e `version` não tem mais um `ms_` prefixo:

| Atributo | Tipo | Observação |
| --- | --- | --- |
| ID |Cadeia de caracteres, marcadas como obrigatórias |chave primária no repositório remoto |
| createdAt |Data |propriedade do sistema toocreatedAt mapas (opcional) |
| updatedAt |Data |propriedade do sistema tooupdatedAt mapas (opcional) |
| version |Cadeia de caracteres |conflitos de toodetect usado (opcional), tooversion de mapas |

#### <a name="querying-system-properties"></a>Consultando propriedades do sistema
Serviços móveis do Azure, as propriedades do sistema não são enviadas por padrão, mas apenas quando forem solicitados usando a cadeia de caracteres de consulta Olá `__systemProperties`. Por outro lado, no sistema de aplicativos do Azure Mobile propriedades são **sempre selecionado** desde que eles fazem parte do modelo de objeto do hello servidor SDK.

Essa alteração afeta principalmente as implementações personalizadas dos gerenciadores de domínio, como extensões de `MappedEntityDomainManager`. Nos serviços móveis, se um cliente nunca solicita as propriedades de sistema, é possível toouse um `MappedEntityDomainManager` que realmente não mapear todas as propriedades. No entanto, nos Aplicativos Móveis do Azure, essas propriedades não mapeadas causarão um erro em consultas GET.

Olá problema de saudação de tooresolve de maneira mais fácil é toomodify seu DTOs para que eles herdam do `ITableData` em vez de `EntityData`. Em seguida, adicione Olá `[NotMapped]` atributo toohello campos que devem ser omitidos.

Por exemplo, o seguinte Olá define `TodoItem` sem propriedades de sistema:

    using System.ComponentModel.DataAnnotations.Schema;

    public class TodoItem : ITableData
    {
        public string Text { get; set; }

        public bool Complete { get; set; }

        public string Id { get; set; }

        [NotMapped]
        public DateTimeOffset? CreatedAt { get; set; }

        [NotMapped]
        public DateTimeOffset? UpdatedAt { get; set; }

        [NotMapped]
        public bool Deleted { get; set; }

        [NotMapped]
        public byte[] Version { get; set; }
    }

Observação: se você obtiver erros `NotMapped`, adicione uma referência assembly toohello `System.ComponentModel.DataAnnotations`.

### <a name="cors"></a>CORS
Serviços móveis incluído um suporte para CORS encapsulando Olá solução ASP.NET CORS. Essa camada encapsulamento foi removido toogive desenvolvedor de hello mais controle, para que você possa aproveitar diretamente [suporte do ASP.NET CORS](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).

principais áreas de preocupação se usando CORS Hello são que Olá `eTag` e `Location` cabeçalhos devem ter permissão para que Olá cliente SDKs toowork corretamente.

### <a name="push-notifications"></a>Notificações por Push
Para enviar por push, o item Olá principal pode ser ausente do SDK do servidor de saudação é classe de PushRegistrationHandler hello. Registros são tratados de forma ligeiramente diferente em aplicativos móveis, e registros sem marca registros são habilitados por padrão. Gerenciar as marcas pode ser feito por meio de APIs personalizados. Consulte Olá [registrar-se para marcas](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) instruções para obter mais informações.

### <a name="scheduled-jobs"></a>Trabalhos agendados
Trabalhos agendados não estão incorporados em aplicativos móveis, então todos os trabalhos existentes que você tem em seu back-end .NET precisará toobe atualizado individualmente. Uma opção é toocreate agendado [trabalho Web] no site de código do aplicativo móvel hello. Você também pode configurar um controlador que contém o código de trabalho e configurar Olá [Agendador do Azure] toohit esse ponto de extremidade na agenda Olá esperado.

### <a name="miscellaneous-changes"></a>Alterações diversas
Todos os ApiControllers que serão consumidos por um cliente móvel agora deve ter Olá `[MobileAppController]` atributo. Isso não está mais incluído por padrão para que outros toogo ApiControllers afetado por Olá formatadores móveis.

Olá `ApiServices` objeto não fizer parte de saudação SDK. tooaccess configurações de aplicativo móvel, você pode usar o seguinte hello:

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

Da mesma forma, o log agora é obtido usando a gravação de rastreamento ASP.NET padrão hello:

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <a name="authentication"></a>Considerações sobre autenticação
componentes de autenticação Olá dos serviços móveis agora foram movidos para o recurso de autenticação/autorização do serviço de aplicativo hello. Você pode aprender sobre como habilitar isso para o seu site por leitura Olá [aplicativo móvel do adicionar autenticação tooyour](app-service-mobile-ios-get-started-users.md) tópico.

Para alguns provedores, como Google, Facebook e AAD, você deve estar registro existente do tooleverage capaz de saudação do seu aplicativo de cópia. Você simplesmente precisa portal do provedor de identidade toohello toonavigate e adicionar um novo registro de toohello de URL de redirecionamento. Configure autenticação/autorização do serviço de aplicativo com ID de saudação do cliente e o segredo.

### <a name="controller-action-authorization"></a>Autorização de ação do controlador
Todas as instâncias de saudação `[AuthorizeLevel(AuthorizationLevel.User)]` atributo agora deve ser alterado toouse Olá padrão ASP.NET `[Authorize]` atributo. Além disso, controladores são agora anônimos por padrão, como em outros aplicativos ASP.NET.
Se você estiver usando uma saudação em outras opções de AuthorizeLevel, como administrador ou aplicativo, observe que eles são excluídos. Em vez disso, você pode configurar AuthorizationFilters para segredos compartilhados ou configurar um chamadas de serviço a serviço tooenable da entidade de serviço do AAD com segurança.

### <a name="getting-additional-user-information"></a>Obtendo informações adicionais do usuário
Você pode obter informações de usuário adicionais, incluindo tokens de acesso por meio de saudação `GetAppServiceIdentityAsync()` método:

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

Além disso, se seu aplicativo tem dependências no usuário IDs, como armazená-las em um banco de dados, é importante toonote que Olá IDs de usuário entre os serviços móveis e aplicativos móveis do aplicativo de serviço são diferentes. Você ainda pode obter Olá ID de usuário de serviços móveis, embora. Todas as subclasses de ProviderCredentials Olá têm uma propriedade de ID de usuário. Para continuar do exemplo hello antes:

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

Se seu aplicativo aceita todas as dependências IDs de usuário, é importante que você aproveite Olá mesmo registro com um provedor de identidade se possível. As IDs de usuário são registro toohello normalmente no escopo do aplicativo que foi usado, portanto, apresentando um novo registro pode criar problemas com usuários tootheir dados correspondentes.

### <a name="custom-authentication"></a>Autenticação personalizada
Se seu aplicativo estiver usando uma solução de autenticação personalizada, você desejará toomake-se de que o site atualizado Olá tem acesso toohello sistema. Siga as instruções de novo de saudação de autenticação personalizada no hello [visão geral do SDK do .NET server] toointegrate sua solução. Observe que componentes de autenticação personalizada Olá ainda estão na visualização.

## <a name="updating-clients"></a>Atualizando de clientes
Quando você tiver um back-end do Aplicativo Móvel operacional, poderá trabalhar em uma nova versão de seu aplicativo cliente para consumi-lo. Aplicativos móveis também inclui uma nova versão do cliente Olá SDKs e atualização do servidor toohello semelhante acima, você precisará tooremove todas as referências toohello Mobile Services SDKs antes de instalar versões de aplicativos móveis hello.

Uma das principais alterações Olá entre versões de saudação é que construtores de saudação não exigem uma chave de aplicativo. Você agora simplesmente passar na URL de saudação do seu aplicativo móvel. Por exemplo, em clientes do .NET hello, Olá `MobileServiceClient` construtor agora é:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of hello Mobile App
        );

Você pode ler sobre como instalar Olá novos SDKs e usando a nova estrutura de saudação por meio de links de saudação abaixo:

* [iOS versão 3.0.0 ou posterior](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) versão 2.0.0 ou posterior](app-service-mobile-dotnet-how-to-use-client-library.md)

Se seu aplicativo usar notificações por push, tome nota da saudação instruções de registro específico para cada plataforma, como Houve algumas alterações também.

Quando você tiver Olá nova versão do cliente pronto, experimente-o em seu projeto de servidor atualizado. Após validar que ele funciona, você pode liberar uma nova versão do seu aplicativo toocustomers. Eventualmente, depois que os clientes tiveram uma chance tooreceive essas atualizações, você pode excluir a versão de serviços móveis de saudação do seu aplicativo. Neste ponto, você tiver atualizado tooan aplicativo móvel do serviço de aplicativo usando o servidor de aplicativos móveis mais recente Olá SDK.

<!-- URLs. -->

[portal do Azure]: https://portal.azure.com/
[portal clássico do Azure]: https://manage.windowsazure.com/
[quais são os aplicativos móveis?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[SDK de servidor de aplicativos móveis]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Agendador do Azure]: /en-us/documentation/services/scheduler/
[trabalho Web]: ../app-service-web/websites-webjobs-resources.md
[como toouse Olá servidor .NET SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[preços do serviço de aplicativo]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[visão geral do SDK do .NET server]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
