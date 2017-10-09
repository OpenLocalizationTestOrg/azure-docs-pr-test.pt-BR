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
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="0778c-104">Notificações por push com delimitação geográfica com os Hubs de Notificação do Azure e o Bing Spatial Data</span><span class="sxs-lookup"><span data-stu-id="0778c-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="0778c-105">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="0778c-105">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="0778c-106">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="0778c-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0778c-107">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span><span class="sxs-lookup"><span data-stu-id="0778c-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="0778c-108">Neste tutorial, você aprenderá como toodeliver com base no local de enviar notificações por push com Hubs de notificação do Azure e dados espaciais do Bing, utilizado de dentro de um aplicativo de plataforma Universal do Windows.</span><span class="sxs-lookup"><span data-stu-id="0778c-108">In this tutorial, you will learn how toodeliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0778c-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0778c-109">Prerequisites</span></span>
<span data-ttu-id="0778c-110">Primeiramente, você precisa toomake-se de que você tenha todos os Olá software e serviço de pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="0778c-110">First and foremost, you need toomake sure that you have all hello software and service pre-requisites:</span></span>

* <span data-ttu-id="0778c-111">[Visual Studio 2015 Atualização 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) ou posterior (o [Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) também servirá).</span><span class="sxs-lookup"><span data-stu-id="0778c-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="0778c-112">Versão mais recente do hello [SDK do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0778c-112">Latest version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="0778c-113">[Conta do Centro de Desenvolvimento do Bing Mapas](https://www.bingmapsportal.com/) (você pode criá-la gratuitamente e associá-la à sua conta da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="0778c-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="0778c-114">Introdução</span><span class="sxs-lookup"><span data-stu-id="0778c-114">Getting Started</span></span>
<span data-ttu-id="0778c-115">Vamos começar criando o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="0778c-115">Let’s start by creating hello project.</span></span> <span data-ttu-id="0778c-116">No Visual Studio, inicie um novo projeto do tipo **Aplicativo em Branco (Universal do Windows)**.</span><span class="sxs-lookup"><span data-stu-id="0778c-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="0778c-117">Após a conclusão da criação do projeto hello, você deve ter equipamento Olá para o aplicativo hello em si.</span><span class="sxs-lookup"><span data-stu-id="0778c-117">Once hello project creation is complete, you should have hello harness for hello app itself.</span></span> <span data-ttu-id="0778c-118">Agora vamos configurar tudo para a infraestrutura do hello geográfico.</span><span class="sxs-lookup"><span data-stu-id="0778c-118">Now let’s set up everything for hello geo-fencing infrastructure.</span></span> <span data-ttu-id="0778c-119">Como estamos toouse contínuo que Bing serviços para este, há um ponto de extremidade de REST API público que nos permite tooquery quadros de local específico:</span><span class="sxs-lookup"><span data-stu-id="0778c-119">Because we are going toouse Bing services for this, there is a public REST API endpoint that allows us tooquery specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="0778c-120">Você precisará toospecify-lo funcionar Olá tooget parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="0778c-120">You will need toospecify hello following parameters tooget it working:</span></span>

* <span data-ttu-id="0778c-121">**ID da Fonte de Dados** e **Nome da Fonte de Dados** – na API do Bing Mapas, as fontes de dados contêm diversos metadados classificados, como locais e horas comerciais de operação.</span><span class="sxs-lookup"><span data-stu-id="0778c-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="0778c-122">Leia mais sobre isso aqui.</span><span class="sxs-lookup"><span data-stu-id="0778c-122">You can read more about those here.</span></span> 
* <span data-ttu-id="0778c-123">**Nome da entidade** – Olá entidade que você deseja toouse como um ponto de referência de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0778c-123">**Entity Name** – hello entity you want toouse as a reference point for hello notification.</span></span> 
* <span data-ttu-id="0778c-124">**Chave de API do Bing Maps** – chave Olá obtido anteriormente quando você criou a conta do Centro de desenvolvimento do Bing hello.</span><span class="sxs-lookup"><span data-stu-id="0778c-124">**Bing Maps API Key** – this is hello key that you obtained earlier when you created hello Bing Dev Center account.</span></span>

<span data-ttu-id="0778c-125">Vamos fazer uma análise aprofundada sobre instalação Olá para cada um dos elementos de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="0778c-125">Let’s do a deep-dive on hello setup for each of hello elements above.</span></span>

## <a name="setting-up-hello-data-source"></a><span data-ttu-id="0778c-126">Configurando a fonte de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="0778c-126">Setting up hello data source</span></span>
<span data-ttu-id="0778c-127">Você pode fazer isso no hello Centro de desenvolvimento do Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="0778c-127">You can do it in hello Bing Maps Dev Center.</span></span> <span data-ttu-id="0778c-128">Basta clicar no **fontes de dados** em Olá superior barra de navegação e selecione **gerenciar fontes de dados**.</span><span class="sxs-lookup"><span data-stu-id="0778c-128">Simply click on **Data sources** in hello top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="0778c-129">Se você não tenha trabalhado com a API do Bing Maps antes, provavelmente haverá qualquer fonte de dados presente, apenas você possa criar um novo clicando em dados de carregamento tooa fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="0778c-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data tooa data source.</span></span> <span data-ttu-id="0778c-130">Verifique se que você preencher todos os campos de saudação necessário:</span><span class="sxs-lookup"><span data-stu-id="0778c-130">Make sure you fill out all hello required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="0778c-131">Você deve estar se perguntando – o que é o arquivo de dados de saudação e o que deverá que ser carregados?</span><span class="sxs-lookup"><span data-stu-id="0778c-131">You might be wondering – what is hello data file and what should you be uploading?</span></span> <span data-ttu-id="0778c-132">Para fins de saudação desse teste, podemos usar apenas exemplo hello baseados em pipe que quadros uma área de concientizá de são Francisco hello:</span><span class="sxs-lookup"><span data-stu-id="0778c-132">For hello purposes of this test, we can just use hello sample pipe-based that frames an area of hello San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="0778c-133">Olá acima representa essa entidade:</span><span class="sxs-lookup"><span data-stu-id="0778c-133">hello above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="0778c-134">Simplesmente copie e cole a cadeia de caracteres hello acima em um novo arquivo e salve-o como **NotificationHubsGeofence.pipe**e carregá-lo no hello Centro de desenvolvimento do Bing.</span><span class="sxs-lookup"><span data-stu-id="0778c-134">Simply copy and paste hello string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in hello Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="0778c-135">Pode ser solicitado toospecify uma nova chave para Olá **chave mestra** que é diferente da saudação **chave de consulta**.</span><span class="sxs-lookup"><span data-stu-id="0778c-135">You might be prompted toospecify a new key for hello **Master Key** that is different from hello **Query Key**.</span></span> <span data-ttu-id="0778c-136">Basta crie uma nova chave por meio de saudação painel e atualização Olá página fonte de dados carregamento.</span><span class="sxs-lookup"><span data-stu-id="0778c-136">Simply create a new key through hello dashboard and refresh hello data source upload page.</span></span>
> 
> 

<span data-ttu-id="0778c-137">Depois que você carregar o arquivo de dados hello, você precisará toomake-se de que você publicar a fonte de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="0778c-137">Once you upload hello data file, you will need toomake sure that you publish hello data source.</span></span> 

<span data-ttu-id="0778c-138">Vá muito**gerenciar fontes de dados**, exatamente como fizemos acima, localize a fonte de dados na lista de saudação e clique em **publicar** em Olá **ações** coluna.</span><span class="sxs-lookup"><span data-stu-id="0778c-138">Go too**Manage Data Sources**, just like we did above, find your data source in hello list and click on **Publish** in hello **Actions** column.</span></span> <span data-ttu-id="0778c-139">Em um bit, você deverá ver sua fonte de dados em Olá **fontes de dados publicados** guia:</span><span class="sxs-lookup"><span data-stu-id="0778c-139">In a bit, you should see your data source in hello **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="0778c-140">Se você clicar em **editar**, você será capaz de toosee em um relance locais que introduzimos nele:</span><span class="sxs-lookup"><span data-stu-id="0778c-140">If you click **Edit**, you will be able toosee at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="0778c-141">Neste ponto, o portal de saudação não mostra Olá limites para geofence Olá que criamos – tudo o que é necessário é uma confirmação que é local Olá especificado no ambiente de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="0778c-141">At this point, hello portal does not show you hello boundaries for hello geofence that we created – all we need is a confirmation that hello location specified is in hello right vicinity.</span></span>

<span data-ttu-id="0778c-142">Agora você tem todos os requisitos de Olá Olá fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="0778c-142">Now you have all hello requirements for hello data source.</span></span> <span data-ttu-id="0778c-143">detalhes de saudação tooget na URL de solicitação de saudação para chamada hello API no hello Centro de desenvolvimento do Bing Maps, clique em **fontes de dados** e selecione **informações de fonte de dados**.</span><span class="sxs-lookup"><span data-stu-id="0778c-143">tooget hello details on hello request URL for hello API call, in hello Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="0778c-144">Olá **consulta URL** é o que estamos aqui.</span><span class="sxs-lookup"><span data-stu-id="0778c-144">hello **Query URL** is what we’re after here.</span></span> <span data-ttu-id="0778c-145">Este é o ponto de extremidade de saudação em relação ao qual podemos executar consultas toocheck se o dispositivo hello está dentro dos limites de saudação de um local ou não.</span><span class="sxs-lookup"><span data-stu-id="0778c-145">This is hello endpoint against which we can execute queries toocheck whether hello device is currently within hello boundaries of a location or not.</span></span> <span data-ttu-id="0778c-146">tooperform verificar isso, precisamos simplesmente tooexecute um GET chamar com relação à URL de consulta hello, com hello parâmetros acrescentados a seguir:</span><span class="sxs-lookup"><span data-stu-id="0778c-146">tooperform this check, we simply need tooexecute a GET call against hello query URL, with hello following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="0778c-147">Dessa forma você está especificando um ponto de destino que obtemos do dispositivo hello e Bing Maps executará automaticamente Olá cálculos toosee se ele está dentro geofence hello.</span><span class="sxs-lookup"><span data-stu-id="0778c-147">That way you're specifying a target point that we obtain from hello device and Bing Maps will automatically perform hello calculations toosee whether it is within hello geofence.</span></span> <span data-ttu-id="0778c-148">Quando você executa a solicitação de saudação por meio de um navegador (ou ondulação), você obterá padrão uma resposta JSON:</span><span class="sxs-lookup"><span data-stu-id="0778c-148">Once you execute hello request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="0778c-149">Essa resposta só acontece quando ponto Olá realmente é dentro Olá designado limites.</span><span class="sxs-lookup"><span data-stu-id="0778c-149">This response only happens when hello point is actually within hello designated boundaries.</span></span> <span data-ttu-id="0778c-150">Caso contrário, você obterá um bucket vazio de **resultados** :</span><span class="sxs-lookup"><span data-stu-id="0778c-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a><span data-ttu-id="0778c-151">Configuração de aplicativo de UWP hello</span><span class="sxs-lookup"><span data-stu-id="0778c-151">Setting up hello UWP application</span></span>
<span data-ttu-id="0778c-152">Agora que temos de fonte de dados de saudação pronto, podemos começar trabalhando Olá aplicativo UWP que são inicializados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0778c-152">Now that we have hello data source ready, we can start working on hello UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="0778c-153">Primeiro, devemos habilitar os serviços de localização para o nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0778c-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="0778c-154">toodo isso, clique duas vezes no `Package.appxmanifest` arquivo **Gerenciador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="0778c-154">toodo this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="0778c-155">Olá pacote Propriedades guia que acabou de abrir, clique em **recursos** e certifique-se de que você selecione **local**:</span><span class="sxs-lookup"><span data-stu-id="0778c-155">In hello package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="0778c-156">Como o recurso de local de saudação for declarado, crie uma nova pasta em sua solução chamada `Core`e adicione um novo arquivo dentro dele, chamado `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="0778c-156">As hello location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="0778c-157">Olá `LocationHelper` própria classe neste ponto é bem básica – tudo o que ele faz é processada local do usuário Olá tooobtain por meio da API do sistema de saudação:</span><span class="sxs-lookup"><span data-stu-id="0778c-157">hello `LocationHelper` class itself is fairly basic at this point – all it does is allow us tooobtain hello user location through hello system API:</span></span>

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

<span data-ttu-id="0778c-158">Você pode ler mais sobre como obter Olá local do usuário em aplicativos UWP em oficial Olá [documento MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span><span class="sxs-lookup"><span data-stu-id="0778c-158">You can read more about getting hello user’s location in UWP apps in hello official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="0778c-159">toocheck aquisição de local de saudação está funcionando, abra no lado do código de saudação da página principal (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="0778c-159">toocheck that hello location acquisition is actually working, open hello code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="0778c-160">Criar um novo manipulador de eventos Olá `Loaded` evento Olá `MainPage` construtor:</span><span class="sxs-lookup"><span data-stu-id="0778c-160">Create a new event handler for hello `Loaded` event in hello `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="0778c-161">implementação de Olá Olá do manipulador de eventos é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0778c-161">hello implementation of hello event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="0778c-162">Observe que é declarada manipulador hello como assíncronas porque `GetCurrentLocation` é possível aguardar e, portanto, requer toobe executado em um contexto assíncrono.</span><span class="sxs-lookup"><span data-stu-id="0778c-162">Notice that we declared hello handler as async because `GetCurrentLocation` is awaitable, and therefore requires toobe executed in an async context.</span></span> <span data-ttu-id="0778c-163">Além disso, como em determinadas circunstâncias, pode acabar com um local nulo (por exemplo, serviços de localização de saudação são desabilitados ou o aplicativo hello foi negado local de tooaccess permissões), é preciso toomake-se de que ela será manipulada corretamente com uma verificação de nula.</span><span class="sxs-lookup"><span data-stu-id="0778c-163">Also, because under certain circumstances we might end up with a null location (e.g. hello location services are disabled or hello application was denied permissions tooaccess location), we need toomake sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="0778c-164">Execute o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0778c-164">Run hello application.</span></span> <span data-ttu-id="0778c-165">Permita o acesso de localização:</span><span class="sxs-lookup"><span data-stu-id="0778c-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="0778c-166">Uma vez Olá inícios de aplicativos, você deve ser capaz de toosee Olá coordenadas no hello **saída** janela:</span><span class="sxs-lookup"><span data-stu-id="0778c-166">Once hello application launches, you should be able toosee hello coordinates in hello **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="0778c-167">Agora você sabe que funciona de aquisição local – sinta-se livre tooremove manipulador de eventos de teste de saudação para carregado porque é não usá-lo mais.</span><span class="sxs-lookup"><span data-stu-id="0778c-167">Now you know that location acquisition works – feel free tooremove hello test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="0778c-168">Olá próxima etapa é toocapture as alterações de localização.</span><span class="sxs-lookup"><span data-stu-id="0778c-168">hello next step is toocapture location changes.</span></span> <span data-ttu-id="0778c-169">Para fazer isso, vamos voltar toohello `LocationHelper` classe e adicione o manipulador de eventos Olá `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="0778c-169">For that, let’s go back toohello `LocationHelper` class and add hello event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="0778c-170">implementação de saudação mostrará as coordenadas de local de saudação na Olá **saída** janela:</span><span class="sxs-lookup"><span data-stu-id="0778c-170">hello implementation will show hello location coordinates in hello **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a><span data-ttu-id="0778c-171">Configuração de back-end de saudação</span><span class="sxs-lookup"><span data-stu-id="0778c-171">Setting up hello backend</span></span>
<span data-ttu-id="0778c-172">Baixar Olá [exemplo de back-end do .NET do GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="0778c-172">Download hello [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="0778c-173">Após a conclusão do download hello, abra Olá `NotifyUsers` pasta e subsequentemente – hello `NotifyUsers.sln` arquivo.</span><span class="sxs-lookup"><span data-stu-id="0778c-173">Once hello download completes, open hello `NotifyUsers` folder, and subsequently – hello `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="0778c-174">Saudação de conjunto `AppBackend` projeto como Olá **projeto de inicialização** e iniciá-lo.</span><span class="sxs-lookup"><span data-stu-id="0778c-174">Set hello `AppBackend` project as hello **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="0778c-175">Olá projeto já está configurado toosend push notificações tootarget dispositivos, portanto vamos precisar toodo somente duas coisas – alternar cadeia de caracteres de conexão à direita de Olá Olá hub de notificação e adicionar limite identificação toosend Olá notificação apenas quando hello usuário está dentro do geofence hello.</span><span class="sxs-lookup"><span data-stu-id="0778c-175">hello project is already configured toosend push notifications tootarget devices, so we’ll need toodo only two things – swap out hello right connection string for hello notification hub and add boundary identification toosend hello notification only when hello user is within hello geofence.</span></span>

<span data-ttu-id="0778c-176">cadeia de conexão tooconfigure hello, em Olá `Models` pasta abrir `Notifications.cs`.</span><span class="sxs-lookup"><span data-stu-id="0778c-176">tooconfigure hello connection string, in hello `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="0778c-177">Olá `NotificationHubClient.CreateClientFromConnectionString` função deve conter informações de saudação sobre seu hub de notificação que você pode obter Olá [Portal do Azure](https://portal.azure.com) (Examinar Olá **políticas de acesso** folha em  **Configurações de**).</span><span class="sxs-lookup"><span data-stu-id="0778c-177">hello `NotificationHubClient.CreateClientFromConnectionString` function should contain hello information about your notification hub that you can get in hello [Azure Portal](https://portal.azure.com) (look inside hello **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="0778c-178">Salve o arquivo de configuração atualizada do hello.</span><span class="sxs-lookup"><span data-stu-id="0778c-178">Save hello updated configuration file.</span></span>

<span data-ttu-id="0778c-179">Agora precisamos toocreate um modelo para Olá resultados de API do Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="0778c-179">Now we need toocreate a model for hello Bing Maps API result.</span></span> <span data-ttu-id="0778c-180">Olá toodo de maneira mais fácil que é o botão direito do mouse em hello `Models` pasta **adicionar** > **classe**.</span><span class="sxs-lookup"><span data-stu-id="0778c-180">hello easiest way toodo that is right-click on hello `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="0778c-181">Nomeie-o `GeofenceBoundary.cs`.</span><span class="sxs-lookup"><span data-stu-id="0778c-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="0778c-182">Depois, copie Olá JSON da resposta Olá API que abordamos na primeira seção do hello e no uso do Visual Studio **editar** > **Colar especial** > **colar JSON como Classes**.</span><span class="sxs-lookup"><span data-stu-id="0778c-182">Once done, copy hello JSON from hello API response that we discussed in hello first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="0778c-183">Dessa forma, podemos garantir que o objeto hello será desserializada exatamente como ele estivesse destinado.</span><span class="sxs-lookup"><span data-stu-id="0778c-183">That way we ensure that hello object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="0778c-184">O conjunto de classes resultante deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="0778c-184">Your resulting class set should resemble this:</span></span>

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

<span data-ttu-id="0778c-185">Em seguida, abra `Controllers` > `NotificationsController.cs`.</span><span class="sxs-lookup"><span data-stu-id="0778c-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="0778c-186">Precisamos tootweak Olá Post chamada tooaccount de latitude e longitude de destino hello.</span><span class="sxs-lookup"><span data-stu-id="0778c-186">We need tootweak hello Post call tooaccount for hello target longitude and latitude.</span></span> <span data-ttu-id="0778c-187">Para fazer isso, basta adicionar assinatura de função de toohello de duas cadeias de caracteres – `latitude` e `longitude`.</span><span class="sxs-lookup"><span data-stu-id="0778c-187">For that, simply add two strings toohello function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="0778c-188">Criar uma nova classe no projeto Olá chamado `ApiHelper.cs` – usaremos a ele interseções de limite do tooconnect tooBing toocheck ponto.</span><span class="sxs-lookup"><span data-stu-id="0778c-188">Create a new class within hello project called `ApiHelper.cs` – we’ll use it tooconnect tooBing toocheck point boundary intersections.</span></span> <span data-ttu-id="0778c-189">Implemente uma função `IsPointWithinBounds` , desta forma:</span><span class="sxs-lookup"><span data-stu-id="0778c-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

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
> <span data-ttu-id="0778c-190">Certifique-se de que toosubstitute Olá API ponto de extremidade com hello URL de consulta que você obteve anteriormente da saudação Centro de desenvolvimento do Bing (mesmo se aplica chave toohello API).</span><span class="sxs-lookup"><span data-stu-id="0778c-190">Make sure toosubstitute hello API endpoint with hello query URL that you obtained earlier from hello Bing Dev Center (same applies toohello API key).</span></span> 
> 
> 

<span data-ttu-id="0778c-191">Se houver consulta toohello de resultados, isso significa que Olá ponto especificado está dentro dos limites de saudação do geofence Olá, portanto retornamos `true`.</span><span class="sxs-lookup"><span data-stu-id="0778c-191">If there are results toohello query, that means that hello specified point is within hello boundaries of hello geofence, so we return `true`.</span></span> <span data-ttu-id="0778c-192">Se não houver nenhum resultado, Bing é informar que o ponto de saudação está fora do quadro de pesquisa Olá, portanto retornamos `false`.</span><span class="sxs-lookup"><span data-stu-id="0778c-192">If there are no results, Bing is telling us that hello point is outside hello lookup frame, so we return `false`.</span></span>

<span data-ttu-id="0778c-193">Em `NotificationsController.cs`, crie uma seleção antes de instrução de comutador hello:</span><span class="sxs-lookup"><span data-stu-id="0778c-193">Back in `NotificationsController.cs`, create a check right before hello switch statement:</span></span>

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

<span data-ttu-id="0778c-194">Dessa forma, notificação Olá é enviada apenas quando o ponto de saudação está dentro dos limites de saudação.</span><span class="sxs-lookup"><span data-stu-id="0778c-194">That way, hello notification is only sent when hello point is within hello boundaries.</span></span>

## <a name="testing-push-notifications-in-hello-uwp-app"></a><span data-ttu-id="0778c-195">Notificações por push de teste no aplicativo UWP Olá</span><span class="sxs-lookup"><span data-stu-id="0778c-195">Testing push notifications in hello UWP app</span></span>
<span data-ttu-id="0778c-196">Voltando toohello aplicativo UWP, é agora deve ser capaz de tootest notificações.</span><span class="sxs-lookup"><span data-stu-id="0778c-196">Going back toohello UWP app, we should now be able tootest notifications.</span></span> <span data-ttu-id="0778c-197">Dentro de saudação `LocationHelper` classe, crie uma nova função – `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="0778c-197">Within hello `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

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
> <span data-ttu-id="0778c-198">Trocar Olá `POST_URL` toohello local do seu aplicativo da web implantados criada na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="0778c-198">Swap hello `POST_URL` toohello location of your deployed web application that we created in hello previous section.</span></span> <span data-ttu-id="0778c-199">Por ora, é toorun Okey-lo localmente, mas, conforme você trabalha na implantação de uma versão pública, será necessário toohost-lo com um provedor externo.</span><span class="sxs-lookup"><span data-stu-id="0778c-199">For now, it’s OK toorun it locally, but as you work on deploying a public version, you will need toohost it with an external provider.</span></span>
> 
> 

<span data-ttu-id="0778c-200">Vamos agora Certifique-se de que é registrar o aplicativo UWP Olá para notificações por push.</span><span class="sxs-lookup"><span data-stu-id="0778c-200">Let’s now make sure that we register hello UWP app for push notifications.</span></span> <span data-ttu-id="0778c-201">No Visual Studio, clique em **projeto** > **armazenar** > **associar aplicativo store Olá**.</span><span class="sxs-lookup"><span data-stu-id="0778c-201">In Visual Studio, click on **Project** > **Store** > **Associate app with hello store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="0778c-202">Depois que você entrar na conta de desenvolvedor tooyour, certifique-se de selecionar um aplicativo existente ou crie um novo e associar o pacote de saudação a ele.</span><span class="sxs-lookup"><span data-stu-id="0778c-202">Once you sign in tooyour developer account, make sure you select an existing app or create a new one and associate hello package with it.</span></span> 

<span data-ttu-id="0778c-203">Vá toohello Dev Center e o aplicativo hello abertos que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="0778c-203">Go toohello Dev Center and open hello app that you just created.</span></span> <span data-ttu-id="0778c-204">Clique em **Serviços** > **Notificações por Push** > **Site dos Live Services**.</span><span class="sxs-lookup"><span data-stu-id="0778c-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="0778c-205">No site de hello, tome nota das Olá **segredo do aplicativo** e hello **SID do pacote**.</span><span class="sxs-lookup"><span data-stu-id="0778c-205">On hello site, take note of hello **Application Secret** and hello **Package SID**.</span></span> <span data-ttu-id="0778c-206">Você precisará tanto no hello Azure Portal – abra seu hub de notificação, clique em **configurações** > **Notification Services** > **do Windows (WNS)**e insira as informações de Olá nos campos Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="0778c-206">You will need both in hello Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter hello information in hello required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="0778c-207">Clique em **Save**.</span><span class="sxs-lookup"><span data-stu-id="0778c-207">Click on **Save**.</span></span>

<span data-ttu-id="0778c-208">Clique com o botão direito do mouse em **Referências** no **Gerenciador de Soluções** e selecione **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0778c-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="0778c-209">Precisaremos tooadd toohello uma referência **biblioteca gerenciada do barramento de serviço do Microsoft Azure** – simplesmente procurar `WindowsAzure.Messaging.Managed` e adicioná-lo tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="0778c-209">We will need tooadd a reference toohello **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it tooyour project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="0778c-210">Para fins de teste, podemos criar hello `MainPage_Loaded` novamente, o manipulador de eventos e adicionar esse tooit de trecho de código:</span><span class="sxs-lookup"><span data-stu-id="0778c-210">For testing purposes, we can create hello `MainPage_Loaded` event handler once again, and add this code snippet tooit:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="0778c-211">Olá acima registra o aplicativo hello com hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0778c-211">hello above registers hello app with hello notification hub.</span></span> <span data-ttu-id="0778c-212">Você está pronto toogo!</span><span class="sxs-lookup"><span data-stu-id="0778c-212">You are ready toogo!</span></span> 

<span data-ttu-id="0778c-213">Em `LocationHelper`, dentro de saudação `Geolocator_PositionChanged` manipulador, você pode adicionar uma parte do código de teste que colocarão forçada local hello dentro Olá geofence:</span><span class="sxs-lookup"><span data-stu-id="0778c-213">In `LocationHelper`, inside hello `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put hello location inside hello geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="0778c-214">Porque não está transmitindo coordenadas real de saudação (que não podem ser dentro dos limites de saudação momento Olá) e está usando valores de teste predefinidas, veremos uma notificação aparecem na atualização:</span><span class="sxs-lookup"><span data-stu-id="0778c-214">Because we are not passing hello real coordinates (which might not be within hello boundaries at hello moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="0778c-215">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="0778c-215">What’s next?</span></span>
<span data-ttu-id="0778c-216">Há algumas etapas que talvez você precise toofollow em adição toohello acima toomake se a solução hello está pronto para produção.</span><span class="sxs-lookup"><span data-stu-id="0778c-216">There are a couple of steps that you might need toofollow in addition toohello above toomake sure that hello solution is production-ready.</span></span>

<span data-ttu-id="0778c-217">Primeiramente, talvez seja necessário tooensure que geofences são dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="0778c-217">First and foremost, you might need tooensure that geofences are dynamic.</span></span> <span data-ttu-id="0778c-218">Isso exigirá algum trabalho adicional com hello API do Bing em limites nova de ordem toobe tooupload capaz de na fonte de dados existente do hello.</span><span class="sxs-lookup"><span data-stu-id="0778c-218">This will require some extra work with hello Bing API in order toobe able tooupload new boundaries within hello existing data source.</span></span> <span data-ttu-id="0778c-219">Consulte Olá [documentação da API de serviços de dados espaciais do Bing](https://msdn.microsoft.com/library/ff701734.aspx) para obter mais detalhes sobre o assunto de saudação.</span><span class="sxs-lookup"><span data-stu-id="0778c-219">Consult hello [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on hello subject.</span></span>

<span data-ttu-id="0778c-220">Segundo, que tooensure de trabalho que entrega Olá é feita participantes direito toohello, talvez você queira tootarget-los por meio de [marcação](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="0778c-220">Second, as you are working tooensure that hello delivery is done toohello right participants, you might want tootarget them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="0778c-221">solução de saudação mostrada acima descreve um cenário em que você pode ter uma ampla variedade de plataformas de destino, portanto não limitamos recursos de toosystem específicos de isolamento geográfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="0778c-221">hello solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit hello geofencing toosystem-specific capabilities.</span></span> <span data-ttu-id="0778c-222">Dito isso, Olá plataforma Universal do Windows oferece recursos muito[detectar geofences direito-de-prontos](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="0778c-222">That said, hello Universal Windows Platform offers capabilities too[detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="0778c-223">Para obter mais detalhes sobre os recursos de Hubs de Notificação, confira nosso [portal de documentação](https://azure.microsoft.com/documentation/services/notification-hubs/).</span><span class="sxs-lookup"><span data-stu-id="0778c-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

