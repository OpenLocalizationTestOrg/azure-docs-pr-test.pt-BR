---
title: "notificações de push isolados aaaGeo com Hubs de notificação do Azure e dados espaciais Bing | Microsoft Docs"
description: "Neste tutorial, você aprenderá como toodeliver com base no local de enviar notificações por push com Hubs de notificação do Azure e dados espaciais do Bing."
services: notification-hubs
documentationcenter: windows
keywords: "notificação por push,notificação por push"
author: dend
manager: yuaxu
editor: dend
ms.assetid: f41beea1-0d62-4418-9ffc-c9d70607a1b7
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/31/2016
ms.author: dendeli
ms.openlocfilehash: d6efe473537f2159240c53e780741f12619c045d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a>Notificações por push com delimitação geográfica com os Hubs de Notificação do Azure e o Bing Spatial Data
> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).
> 
> 

Neste tutorial, você aprenderá como toodeliver com base no local de enviar notificações por push com Hubs de notificação do Azure e dados espaciais do Bing, utilizado de dentro de um aplicativo de plataforma Universal do Windows.

## <a name="prerequisites"></a>Pré-requisitos
Primeiramente, você precisa toomake-se de que você tenha todos os Olá software e serviço de pré-requisitos:

* [Visual Studio 2015 Atualização 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) ou posterior (o [Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) também servirá). 
* Versão mais recente do hello [SDK do Azure](https://azure.microsoft.com/downloads/). 
* [Conta do Centro de Desenvolvimento do Bing Mapas](https://www.bingmapsportal.com/) (você pode criá-la gratuitamente e associá-la à sua conta da Microsoft). 

## <a name="getting-started"></a>Introdução
Vamos começar criando o projeto de saudação. No Visual Studio, inicie um novo projeto do tipo **Aplicativo em Branco (Universal do Windows)**.

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

Após a conclusão da criação do projeto hello, você deve ter equipamento Olá para o aplicativo hello em si. Agora vamos configurar tudo para a infraestrutura do hello geográfico. Como estamos toouse contínuo que Bing serviços para este, há um ponto de extremidade de REST API público que nos permite tooquery quadros de local específico:

    http://spatial.virtualearth.net/REST/v1/data/

Você precisará toospecify-lo funcionar Olá tooget parâmetros a seguir:

* **ID da Fonte de Dados** e **Nome da Fonte de Dados** – na API do Bing Mapas, as fontes de dados contêm diversos metadados classificados, como locais e horas comerciais de operação. Leia mais sobre isso aqui. 
* **Nome da entidade** – Olá entidade que você deseja toouse como um ponto de referência de notificação de saudação. 
* **Chave de API do Bing Maps** – chave Olá obtido anteriormente quando você criou a conta do Centro de desenvolvimento do Bing hello.

Vamos fazer uma análise aprofundada sobre instalação Olá para cada um dos elementos de saudação acima.

## <a name="setting-up-hello-data-source"></a>Configurando a fonte de dados de saudação
Você pode fazer isso no hello Centro de desenvolvimento do Bing Maps. Basta clicar no **fontes de dados** em Olá superior barra de navegação e selecione **gerenciar fontes de dados**.

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

Se você não tenha trabalhado com a API do Bing Maps antes, provavelmente haverá qualquer fonte de dados presente, apenas você possa criar um novo clicando em dados de carregamento tooa fonte de dados. Verifique se que você preencher todos os campos de saudação necessário:

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

Você deve estar se perguntando – o que é o arquivo de dados de saudação e o que deverá que ser carregados? Para fins de saudação desse teste, podemos usar apenas exemplo hello baseados em pipe que quadros uma área de concientizá de são Francisco hello:

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

Olá acima representa essa entidade:

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

Simplesmente copie e cole a cadeia de caracteres hello acima em um novo arquivo e salve-o como **NotificationHubsGeofence.pipe**e carregá-lo no hello Centro de desenvolvimento do Bing.

> [!NOTE]
> Pode ser solicitado toospecify uma nova chave para Olá **chave mestra** que é diferente da saudação **chave de consulta**. Basta crie uma nova chave por meio de saudação painel e atualização Olá página fonte de dados carregamento.
> 
> 

Depois que você carregar o arquivo de dados hello, você precisará toomake-se de que você publicar a fonte de dados de saudação. 

Vá muito**gerenciar fontes de dados**, exatamente como fizemos acima, localize a fonte de dados na lista de saudação e clique em **publicar** em Olá **ações** coluna. Em um bit, você deverá ver sua fonte de dados em Olá **fontes de dados publicados** guia:

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

Se você clicar em **editar**, você será capaz de toosee em um relance locais que introduzimos nele:

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

Neste ponto, o portal de saudação não mostra Olá limites para geofence Olá que criamos – tudo o que é necessário é uma confirmação que é local Olá especificado no ambiente de saudação à direita.

Agora você tem todos os requisitos de Olá Olá fonte de dados. detalhes de saudação tooget na URL de solicitação de saudação para chamada hello API no hello Centro de desenvolvimento do Bing Maps, clique em **fontes de dados** e selecione **informações de fonte de dados**.

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

Olá **consulta URL** é o que estamos aqui. Este é o ponto de extremidade de saudação em relação ao qual podemos executar consultas toocheck se o dispositivo hello está dentro dos limites de saudação de um local ou não. tooperform verificar isso, precisamos simplesmente tooexecute um GET chamar com relação à URL de consulta hello, com hello parâmetros acrescentados a seguir:

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

Dessa forma você está especificando um ponto de destino que obtemos do dispositivo hello e Bing Maps executará automaticamente Olá cálculos toosee se ele está dentro geofence hello. Quando você executa a solicitação de saudação por meio de um navegador (ou ondulação), você obterá padrão uma resposta JSON:

![](./media/notification-hubs-geofence/bing-maps-json.png)

Essa resposta só acontece quando ponto Olá realmente é dentro Olá designado limites. Caso contrário, você obterá um bucket vazio de **resultados** :

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a>Configuração de aplicativo de UWP hello
Agora que temos de fonte de dados de saudação pronto, podemos começar trabalhando Olá aplicativo UWP que são inicializados anteriormente.

Primeiro, devemos habilitar os serviços de localização para o nosso aplicativo. toodo isso, clique duas vezes no `Package.appxmanifest` arquivo **Gerenciador de soluções**.

![](./media/notification-hubs-geofence/vs-package-manifest.png)

Olá pacote Propriedades guia que acabou de abrir, clique em **recursos** e certifique-se de que você selecione **local**:

![](./media/notification-hubs-geofence/vs-package-location.png)

Como o recurso de local de saudação for declarado, crie uma nova pasta em sua solução chamada `Core`e adicione um novo arquivo dentro dele, chamado `LocationHelper.cs`:

![](./media/notification-hubs-geofence/vs-location-helper.png)

Olá `LocationHelper` própria classe neste ponto é bem básica – tudo o que ele faz é processada local do usuário Olá tooobtain por meio da API do sistema de saudação:

    using System;
    using System.Threading.Tasks;
    using Windows.Devices.Geolocation;

    namespace NotificationHubs.Geofence.Core
    {
        public class LocationHelper
        {
            private static readonly uint AppDesiredAccuracyInMeters = 10;

            public async static Task<Geoposition> GetCurrentLocation()
            {
                var accessStatus = await Geolocator.RequestAccessAsync();
                switch (accessStatus)
                {
                    case GeolocationAccessStatus.Allowed:
                        {
                            Geolocator geolocator = new Geolocator { DesiredAccuracyInMeters = AppDesiredAccuracyInMeters };

                            return await geolocator.GetGeopositionAsync();
                        }
                    default:
                        {
                            return null;
                        }
                }
            }

        }
    }

Você pode ler mais sobre como obter Olá local do usuário em aplicativos UWP em oficial Olá [documento MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).

toocheck aquisição de local de saudação está funcionando, abra no lado do código de saudação da página principal (`MainPage.xaml.cs`). Criar um novo manipulador de eventos Olá `Loaded` evento Olá `MainPage` construtor:

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

implementação de Olá Olá do manipulador de eventos é o seguinte:

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

Observe que é declarada manipulador hello como assíncronas porque `GetCurrentLocation` é possível aguardar e, portanto, requer toobe executado em um contexto assíncrono. Além disso, como em determinadas circunstâncias, pode acabar com um local nulo (por exemplo, serviços de localização de saudação são desabilitados ou o aplicativo hello foi negado local de tooaccess permissões), é preciso toomake-se de que ela será manipulada corretamente com uma verificação de nula.

Execute o aplicativo hello. Permita o acesso de localização:

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

Uma vez Olá inícios de aplicativos, você deve ser capaz de toosee Olá coordenadas no hello **saída** janela:

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

Agora você sabe que funciona de aquisição local – sinta-se livre tooremove manipulador de eventos de teste de saudação para carregado porque é não usá-lo mais.

Olá próxima etapa é toocapture as alterações de localização. Para fazer isso, vamos voltar toohello `LocationHelper` classe e adicione o manipulador de eventos Olá `PositionChanged`:

    geolocator.PositionChanged += Geolocator_PositionChanged;

implementação de saudação mostrará as coordenadas de local de saudação na Olá **saída** janela:

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a>Configuração de back-end de saudação
Baixar Olá [exemplo de back-end do .NET do GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). Após a conclusão do download hello, abra Olá `NotifyUsers` pasta e subsequentemente – hello `NotifyUsers.sln` arquivo.

Saudação de conjunto `AppBackend` projeto como Olá **projeto de inicialização** e iniciá-lo.

![](./media/notification-hubs-geofence/vs-startup-project.png)

Olá projeto já está configurado toosend push notificações tootarget dispositivos, portanto vamos precisar toodo somente duas coisas – alternar cadeia de caracteres de conexão à direita de Olá Olá hub de notificação e adicionar limite identificação toosend Olá notificação apenas quando hello usuário está dentro do geofence hello.

cadeia de conexão tooconfigure hello, em Olá `Models` pasta abrir `Notifications.cs`. Olá `NotificationHubClient.CreateClientFromConnectionString` função deve conter informações de saudação sobre seu hub de notificação que você pode obter Olá [Portal do Azure](https://portal.azure.com) (Examinar Olá **políticas de acesso** folha em  **Configurações de**). Salve o arquivo de configuração atualizada do hello.

Agora precisamos toocreate um modelo para Olá resultados de API do Bing Maps. Olá toodo de maneira mais fácil que é o botão direito do mouse em hello `Models` pasta **adicionar** > **classe**. Nomeie-o `GeofenceBoundary.cs`. Depois, copie Olá JSON da resposta Olá API que abordamos na primeira seção do hello e no uso do Visual Studio **editar** > **Colar especial** > **colar JSON como Classes**. 

Dessa forma, podemos garantir que o objeto hello será desserializada exatamente como ele estivesse destinado. O conjunto de classes resultante deve ter esta aparência:

    namespace AppBackend.Models
    {
        public class Rootobject
        {
            public D d { get; set; }
        }

        public class D
        {
            public string __copyright { get; set; }
            public Result[] results { get; set; }
        }

        public class Result
        {
            public __Metadata __metadata { get; set; }
            public string EntityID { get; set; }
            public string Name { get; set; }
            public float Longitude { get; set; }
            public float Latitude { get; set; }
            public string Boundary { get; set; }
            public string Confidence { get; set; }
            public string Locality { get; set; }
            public string AddressLine { get; set; }
            public string AdminDistrict { get; set; }
            public string CountryRegion { get; set; }
            public string PostalCode { get; set; }
        }

        public class __Metadata
        {
            public string uri { get; set; }
        }
    }

Em seguida, abra `Controllers` > `NotificationsController.cs`. Precisamos tootweak Olá Post chamada tooaccount de latitude e longitude de destino hello. Para fazer isso, basta adicionar assinatura de função de toohello de duas cadeias de caracteres – `latitude` e `longitude`.

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

Criar uma nova classe no projeto Olá chamado `ApiHelper.cs` – usaremos a ele interseções de limite do tooconnect tooBing toocheck ponto. Implemente uma função `IsPointWithinBounds` , desta forma:

    public class ApiHelper
    {
        public static readonly string ApiEndpoint = "{YOUR_QUERY_ENDPOINT}?spatialFilter=intersects(%27POINT%20({0}%20{1})%27)&$format=json&key={2}";
        public static readonly string ApiKey = "{YOUR_API_KEY}";

        public static bool IsPointWithinBounds(string longitude,string latitude)
        {
            var json = new WebClient().DownloadString(string.Format(ApiEndpoint, longitude, latitude, ApiKey));
            var result = JsonConvert.DeserializeObject<Rootobject>(json);
            if (result.d.results != null && result.d.results.Count() > 0)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    }

> [!NOTE]
> Certifique-se de que toosubstitute Olá API ponto de extremidade com hello URL de consulta que você obteve anteriormente da saudação Centro de desenvolvimento do Bing (mesmo se aplica chave toohello API). 
> 
> 

Se houver consulta toohello de resultados, isso significa que Olá ponto especificado está dentro dos limites de saudação do geofence Olá, portanto retornamos `true`. Se não houver nenhum resultado, Bing é informar que o ponto de saudação está fora do quadro de pesquisa Olá, portanto retornamos `false`.

Em `NotificationsController.cs`, crie uma seleção antes de instrução de comutador hello:

    if (ApiHelper.IsPointWithinBounds(longitude, latitude))
    {
        switch (pns.ToLower())
        {
            case "wns":
                //// Windows 8.1 / Windows Phone 8.1
                var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                // Windows 10 specific Action Center support
                toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                break;
        }
    }

Dessa forma, notificação Olá é enviada apenas quando o ponto de saudação está dentro dos limites de saudação.

## <a name="testing-push-notifications-in-hello-uwp-app"></a>Notificações por push de teste no aplicativo UWP Olá
Voltando toohello aplicativo UWP, é agora deve ser capaz de tootest notificações. Dentro de saudação `LocationHelper` classe, crie uma nova função – `SendLocationToBackend`:

    public static async Task SendLocationToBackend(string pns, string userTag, string message, string latitude, string longitude)
    {
        var POST_URL = "http://localhost:8741/api/notifications?pns=" +
            pns + "&to_tag=" + userTag + "&latitude=" + latitude + "&longitude=" + longitude;

        using (var httpClient = new HttpClient())
        {
            try
            {
                await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                    System.Text.Encoding.UTF8, "application/json"));
            }
            catch (Exception ex)
            {
                Debug.WriteLine(ex.Message);
            }
        }
    }

> [!NOTE]
> Trocar Olá `POST_URL` toohello local do seu aplicativo da web implantados criada na seção anterior hello. Por ora, é toorun Okey-lo localmente, mas, conforme você trabalha na implantação de uma versão pública, será necessário toohost-lo com um provedor externo.
> 
> 

Vamos agora Certifique-se de que é registrar o aplicativo UWP Olá para notificações por push. No Visual Studio, clique em **projeto** > **armazenar** > **associar aplicativo store Olá**.

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

Depois que você entrar na conta de desenvolvedor tooyour, certifique-se de selecionar um aplicativo existente ou crie um novo e associar o pacote de saudação a ele. 

Vá toohello Dev Center e o aplicativo hello abertos que você acabou de criar. Clique em **Serviços** > **Notificações por Push** > **Site dos Live Services**.

![](./media/notification-hubs-geofence/ms-live-services.png)

No site de hello, tome nota das Olá **segredo do aplicativo** e hello **SID do pacote**. Você precisará tanto no hello Azure Portal – abra seu hub de notificação, clique em **configurações** > **Notification Services** > **do Windows (WNS)**e insira as informações de Olá nos campos Olá necessário.

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

Clique em **Save**.

Clique com o botão direito do mouse em **Referências** no **Gerenciador de Soluções** e selecione **Gerenciar Pacotes NuGet**. Precisaremos tooadd toohello uma referência **biblioteca gerenciada do barramento de serviço do Microsoft Azure** – simplesmente procurar `WindowsAzure.Messaging.Managed` e adicioná-lo tooyour projeto.

![](./media/notification-hubs-geofence/vs-nuget.png)

Para fins de teste, podemos criar hello `MainPage_Loaded` novamente, o manipulador de eventos e adicionar esse tooit de trecho de código:

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

Olá acima registra o aplicativo hello com hub de notificação de saudação. Você está pronto toogo! 

Em `LocationHelper`, dentro de saudação `Geolocator_PositionChanged` manipulador, você pode adicionar uma parte do código de teste que colocarão forçada local hello dentro Olá geofence:

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

Porque não está transmitindo coordenadas real de saudação (que não podem ser dentro dos limites de saudação momento Olá) e está usando valores de teste predefinidas, veremos uma notificação aparecem na atualização:

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a>O que vem a seguir?
Há algumas etapas que talvez você precise toofollow em adição toohello acima toomake se a solução hello está pronto para produção.

Primeiramente, talvez seja necessário tooensure que geofences são dinâmicos. Isso exigirá algum trabalho adicional com hello API do Bing em limites nova de ordem toobe tooupload capaz de na fonte de dados existente do hello. Consulte Olá [documentação da API de serviços de dados espaciais do Bing](https://msdn.microsoft.com/library/ff701734.aspx) para obter mais detalhes sobre o assunto de saudação.

Segundo, que tooensure de trabalho que entrega Olá é feita participantes direito toohello, talvez você queira tootarget-los por meio de [marcação](notification-hubs-tags-segment-push-message.md).

solução de saudação mostrada acima descreve um cenário em que você pode ter uma ampla variedade de plataformas de destino, portanto não limitamos recursos de toosystem específicos de isolamento geográfico de saudação. Dito isso, Olá plataforma Universal do Windows oferece recursos muito[detectar geofences direito-de-prontos](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).

Para obter mais detalhes sobre os recursos de Hubs de Notificação, confira nosso [portal de documentação](https://azure.microsoft.com/documentation/services/notification-hubs/).

